---
title: "Go언어에서 확장 가능한 워커 풀을 구축하는 방법을 단계별로 안내하는 Concurrent Processing 마스터하기"
description: ""
coverImage: "/assets/img/2024-05-27-MasteringConcurrentProcessingAStep-by-StepGuidetoBuildingaScalableWorkerPoolinGo_0.png"
date: 2024-05-27 19:52
ogImage:
  url: /assets/img/2024-05-27-MasteringConcurrentProcessingAStep-by-StepGuidetoBuildingaScalableWorkerPoolinGo_0.png
tag: Tech
originalTitle: "Mastering Concurrent Processing: A Step-by-Step Guide to Building a Scalable Worker Pool in Go"
link: "https://medium.com/@souravchoudhary0306/mastering-concurrent-processing-a-step-by-step-guide-to-building-a-scalable-worker-pool-in-go-54093074c612"
---

**10,000개의 요청을 초당 처리해요!**

🤝 LinkedIn에서 저와 연결해요. 확장 가능한 시스템을 만들어봐요.

이 블로그 포스트에서는 Go를 사용하여 확장 가능한 워커 풀을 구축해볼 거에요. 이 구현은 요청의 대량을 처리하기 위해 워커 풀을 효율적으로 관리하며, 부하에 따라 워커 수를 동적으로 확장합니다. 잠재적인 함정에 대해 논하고, 그것들을 피하는 방법에 대해 알아볼 거에요.

# 개요

<div class="content-ad"></div>

우리는 다음과 같은 기능을 갖춘 작업자 풀을 생성할 것입니다:

- 부하에 따라 작업자 수를 동적으로 조절합니다.
- 요청을 타임아웃 및 재시도 메커니즘으로 처리합니다.
- 작업자를 우아하게 종료합니다.

다음은 완전한 코드와 각 부분에 대한 설명 및 문서화가 제공됩니다.

![Mastering Concurrent Processing: A Step-by-Step Guide to Building a Scalable Worker Pool in Go](/assets/img/2024-05-27-MasteringConcurrentProcessingAStep-by-StepGuidetoBuildingaScalableWorkerPoolinGo_0.png)

<div class="content-ad"></div>

# 디스패처

디스패처는 작업자를 관리하고 들어오는 요청을 분배하는 역할을 합니다. 현재 부하에 따라 동적으로 작업자를 추가하거나 제거하며 모든 작업자들을 원활하게 종료합니다.

- AddWorker: 풀에 새 작업자를 추가하고 작업자 수를 증가시킵니다. 작업자는 요청 처리를 시작하기 위해 실행됩니다.
- RemoveWorker: 최소 필요한 작업자보다 많은 경우 풀에서 작업자를 제거합니다. 작업자는 stopCh 채널을 통해 중지되도록 신호를 보냅니다.
- ScaleWorkers: 부하에 따라 작업자 수를 동적으로 조정합니다. 부하가 임계값을 초과하고 최대 허용 작업자보다 작은 경우 새 작업자가 추가됩니다. 부하가 임계값 아래이고 최소 필요한 작업자보다 많은 경우 작업자가 제거됩니다.
- LaunchWorker: 작업자를 시작하고 작업자 수를 증가시킵니다. 일반적으로 초기 작업자 세트에 사용됩니다.
- MakeRequest: 입력 채널에 요청을 추가합니다. 채널이 가득 찬 경우 요청은 삭제되고 메시지가 기록됩니다.
- Stop: 모든 작업자를 원활하게 중지합니다. 모든 작업자가 현재 요청 처리를 완료할 때까지 기다립니다. 제한 시간에 도달하면 모든 작업자를 강제로 중지합니다.

# 작업자

<div class="content-ad"></div>

**Worker 구조체는 요청을 처리하는 작업자를 나타냅니다. 각 작업자는 자신만의 고루틴에서 실행되며 채널에서 수신된 들어오는 요청을 청취합니다.**

- **LaunchWorker**: 작업자를 별도의 고루틴으로 실행합니다. 작업자는 입력 채널이 닫히거나 정지 신호를 받을 때까지 들어오는 요청을 처리합니다.
- **processRequest**: 개별 요청을 처리합니다. 에러가 발생하거나 요청 시간이 초과되었을 경우 최대 지정된 재시도 횟수까지 요청을 다시 시도합니다.

**코드**

```go
// struct.go

package workerpool

import "time"

// Request는 작업자에 의해 처리될 요청을 나타냅니다.
type Request struct {
    Handler    RequestHandler
    Type       int
    Data       interface{}
    Timeout    time.Duration // 요청의 제한 시간
    Retries    int           // 재시도 횟수
    MaxRetries int           // 최대 재시도 횟수
}

// RequestHandler는 요청을 처리하는 함수 유형을 정의합니다.
type RequestHandler func(interface{}) error
```

<div class="content-ad"></div>


### interface.go

```go
package workerpool

import "context"

// WorkerLauncher는 워커를 실행하기 위한 인터페이스입니다.
type WorkerLauncher interface {
 LaunchWorker(in chan Request, stopCh chan struct{})
}

// Dispatcher는 워커 풀을 관리하기 위한 인터페이스입니다.
type Dispatcher interface {
 AddWorker(w WorkerLauncher)
 RemoveWorker(minWorkers int)
 LaunchWorker(id int, w WorkerLauncher)
 ScaleWorkers(minWorkers, maxWorkers, loadThreshold int)
 MakeRequest(Request)
 Stop(ctx context.Context)
}
```

### worker.go

```go
package workerpool

import (
 "context"
 "fmt"
 "sync"
 "time"
)

// Worker는 요청을 처리하는 워커를 나타냅니다.
type Worker struct {
 Id         int
 Wg         *sync.WaitGroup
 ReqHandler map[int]RequestHandler
}

// LaunchWorker는 워커를 실행하여 들어오는 요청을 처리합니다.
// 이는 별도의 고루틴에서 실행되며, 입력 채널에서 들어오는 요청을 지속적으로 수신합니다.
// 워커는 입력 채널이 닫히거나 중지 신호를 받으면 정상적으로 종료됩니다.
func (w *Worker) LaunchWorker(in chan Request, stopCh chan struct{}) {
 go func() {
  defer w.Wg.Done()
  for {
   select {
   case msg, open := <-in:
    if !open {
     // 채널이 닫히면 처리를 중지하고 반환합니다.
     fmt.Println("워커 중지:", w.Id)
     return
    }
    w.processRequest(msg)
    time.Sleep(1 * time.Microsecond) // 밀리초 단위의 작은 지연
   case <-stopCh:
    fmt.Println("워커 중지:", w.Id)
    return
   }
  }
 }()
}

// processRequest는 하나의 요청을 처리합니다.
func (w *Worker) processRequest(msg Request) {
 fmt.Printf("워커 %d가 요청 처리 중: %v\n", w.Id, msg)
 var handler RequestHandler
 var ok bool
 if handler, ok = w.ReqHandler[msg.Type]; !ok {
  fmt.Println("핸들러가 구현되지 않았습니다: 워커ID:", w.Id)
 } else {
  if msg.Timeout == 0 {
   msg.Timeout = time.Duration(10 * time.Millisecond) // 기본 타임아웃
  }
  for attempt := 0; attempt <= msg.MaxRetries; attempt++ {
   var err error
   done := make(chan struct{})
   ctx, cancel := context.WithTimeout(context.Background(), msg.Timeout)
   defer cancel()

   go func() {
    err = handler(msg.Data)
    close(done)
   }()

   select {
   case <-done:
    if err == nil {
     return // 성공적으로 처리
    }
    fmt.Printf("워커 %d: 요청 처리 중 오류: %v\n", w.Id, err)
   case <-ctx.Done():
    fmt.Printf("워커 %d: 요청 처리 시간 초과: %v\n", w.Id, msg.Data)
   }
   fmt.Printf("워커 %d: 요청 %v에 대한 재시도 %d\n", w.Id, attempt, msg.Data)
  }
  fmt.Printf("워커 %d: %d번 재시도 후 요청 %v 처리 실패\n", w.Id, msg.MaxRetries, msg.Data)
 }
}
```

### dispatcher.go

```go
package workerpool

import (
 "context"
 "fmt"
 "sync"
 "time"
)

// ReqHandler는 요청 타입별로 매핑된 핸들러 맵입니다.
var ReqHandler = map[int]RequestHandler{
 1: func(data interface{}) error {
  return nil
 },
}

// dispatcher는 워커 풀을 관리하고 들어오는 요청을 워커들 사이에 분배하는 역할을 합니다.
type dispatcher struct {
 inCh        chan Request
 wg          *sync.WaitGroup
 mu          sync.Mutex
 workerCount int
 stopCh      chan struct{} // 워커에 중지 신호를 보내기 위한 채널
}

// AddWorker는 새로운 워커를 풀에 추가하고 워커 수를 증가시킵니다.
func (d *dispatcher) AddWorker(w WorkerLauncher) {
 d.mu.Lock()
 defer d.mu.Unlock()
 d.workerCount++
 d.wg.Add(1)
 w.LaunchWorker(d.inCh, d.stopCh)
}

// RemoveWorker는 워커 수가 minWorkers보다 큰 경우 워커를 풀에서 제거합니다.
func (d *dispatcher) RemoveWorker(minWorkers int) {
 d.mu.Lock()
 defer d.mu.Unlock()
 if d.workerCount > minWorkers {
  d.workerCount--
  d.stopCh <- struct{}{} // 워커에 중지 신호 전송
 }
}

// ScaleWorkers는 현재 부하에 따라 워커 수를 동적으로 조정합니다.
func (d *dispatcher) ScaleWorkers(minWorkers, maxWorkers, loadThreshold int) {
 ticker := time.NewTicker(time.Microsecond)
 defer ticker.Stop()

 for range ticker.C {
  load := len(d.inCh) // 현재 부하는 채널에 대기 중인 요청 수
  if load > loadThreshold && d.workerCount < maxWorkers {
   fmt.Println("스케일링 트리거")
   newWorker := &Worker{
    Wg:         d.wg,
    Id:         d.workerCount,
    ReqHandler: ReqHandler,
   }
   d.AddWorker(newWorker)
  } else if load < 0.75*loadThreshold && d.workerCount > minWorkers {
   fmt.Println("축소 트리거")
   d.RemoveWorker(minWorkers)
  }
 }
}

// LaunchWorker는 워커를 시작하고 워커 수를 증가시킵니다.
func (d *dispatcher) LaunchWorker(id int, w WorkerLauncher) {
 w.LaunchWorker(d.inCh, d.stopCh) // 중지 채널을 워커에 전달
 d.mu.Lock()
 d.workerCount++
 d.mu.Unlock()
}

// MakeRequest는 요청을 입력 채널에 추가하거나 채널이 가득 찬 경우 삭제합니다.
func (d *dispatcher) MakeRequest(r Request) {
 select {
 case d.inCh <- r:
 default:
  // 채널이 가득 찬 경우 처리
  fmt.Println("요청 채널이 가득 찼습니다. 요청 삭제됨.")
  // 다른 조치를 취하기 전에 로깅, 요청 버퍼링 또는 다른 조치를 취할 수 있습니다.
 }
}

// Stop는 모든 워커를 정상적으로 종료하고 처리가 완료될 때까지 기다립니다.
func (d *dispatcher) Stop(ctx context.Context) {
 fmt.Println("\n중지 호출됨")
 close(d.inCh) // 더 이상 요청을 보내지 않음을 알리기 위해 입력 채널 닫기
 done := make(chan struct{})

 go func() {
  d.wg.Wait() // 모든 워커가 종료될 때까지 대기
  close(done)
 }()

 select {
 case <-done:
  fmt.Println("모든 워커가 정상적으로 중지됨")
 case <-ctx.Done():
  fmt.Println("시간 초과, 강제 종료")
  // 시간 초과 시 모든 워커 강제 종료
  for i := 0; i < d.workerCount; i++ {
   d.stopCh <- struct{}{}
  }
 }

 d.wg.Wait()
}

// NewDispatcher는 버퍼링된 채널과 웨이트 그룹이 있는 새로운 디스패처를 생성합니다.
func NewDispatcher(b int, wg *sync.WaitGroup, maxWorkers int) Dispatcher {
 return &dispatcher{
  inCh:   make(chan Request, b),
  wg:     wg,
  stopCh: make(chan struct{}, maxWorkers), // 블로킹을 방지하기 위한 버퍼링된 채널
 }
}
```

### main.go

```go
package main

import (
 "context"
 "fmt"
 "runtime"
 "sync"
 "time"
 wp "workerpool/workerpool"
)



<div class="content-ad"></div>

# 메인

주요 기능은 디스패처와 워커를 초기화하고 작업을 보내며, 디스패처를 원활하게 종료합니다.

- GOMAXPROCS를 사용 가능한 CPU 수로 설정합니다.
- 디스패처를 초기화하고 초기 워커 집합을 시작합니다.
- 디스패처에 요청을 보냅니다.
- 타임아웃을 설정하여 디스패처를 원활하게 종료합니다.

우리는 컨텍스트 타임아웃, 버퍼 크기, 최소/최대 워커와 같은 매개변수를 조정하여 초당 요청(RPS)을 최대화하고 애플리케이션 성능을 향상시킬 것입니다.

<div class="content-ad"></div>

Stay tuned for practical insights and real-world examples!

If you've read up till now, I hope you enjoyed this article. If you did, please show your support by giving it a clap, as it helps me stay motivated to assist the community.

Feel free to leave a comment if you noticed any discrepancies in this article or if you have any questions related to the content.

Thank you for your time.

<div class="content-ad"></div>

마음에 드시는 사람들과 언제든 연락하세요! LinkedIn에 연결해보는 건 어떠세요? 🤝
```
