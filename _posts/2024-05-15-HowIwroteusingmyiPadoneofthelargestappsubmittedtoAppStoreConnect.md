---
title: "아이패드를 사용하여 App Store Connect에 제출된 최대 규모의 앱 중 하나를 작성했어요"
description: ""
coverImage: "/assets/img/2024-05-15-HowIwroteusingmyiPadoneofthelargestappsubmittedtoAppStoreConnect_0.png"
date: 2024-05-15 12:00
ogImage:
  url: /assets/img/2024-05-15-HowIwroteusingmyiPadoneofthelargestappsubmittedtoAppStoreConnect_0.png
tag: Tech
originalTitle: "How I wrote, using my iPad, one of the largest app submitted to App Store Connect"
link: "https://medium.com/@crsohr/how-i-wrote-using-my-ipad-one-of-the-largest-app-submitted-to-app-store-connect-b91fc98ab179"
---

이야기한 내용은 iPad에서 작성한 앱에 관한 것입니다. 약 1MB의 소스 코드를 갖고 있어서 아마도 애플에 제출된 가장 큰 소스 코드 중 하나일 것입니다. 처음 보았을 때 그 앱은 컴퓨터에서 만들어진 것이 아닌 것을 보여주지 않습니다. 앱은 어떤 앱이어야 하는 것처럼 보이며 느껴집니다. 간단히 말하면, 책을 썼다면 해리 포터의 첫 두권, “해리 포터와 마법사의 돌”과 “해리 포터와 비밀의 방”보다 약간 더 많은 캐릭터들을 포함하고 있을 것입니다.

![image](/assets/img/2024-05-15-HowIwroteusingmyiPadoneofthelargestappsubmittedtoAppStoreConnect_0.png)

이 여정은 즐겁기도 했지만 정직하게 말하자면 그 길에는 많은 울타리도 있었습니다. Swift Playgrounds는 가끔 제한이 있을 때가 있고, 그럴 때는 당신만의 방법을 찾아야 할 것입니다.

이 기사에서는 버전 컨트롤 시스템 사용, 번들에서 파일 편집하는 것과 같은 iPad의 고급 사용 사례들에 공통적인 어려움을 그냥 넘어뛰며, Mac 사용이 여전히 필요할 수 있는 이유에 대해 알아보겠습니다.

![How I wrote using my iPad - one of the largest apps submitted to App Store Connect](/assets/img/2024-05-15-HowIwroteusingmyiPadoneofthelargestappsubmittedtoAppStoreConnect_1.png)

바로 코딩과 관련된 주제도 다루게 될 거에요. 컴파일 시간을 단축하는 법, 하드웨어 가속 계산을 사용하는 법, UI에서 접근할 수 없는 설정을 변경하는 법 등을 다룰 예정이에요.

소프트웨어 개발자가 아니더라도 흥미로운 내용일 것 같아요. 플랫폼의 일부 한계를 강조하며 사용자가 이를 해결하는 방법과, 희망적으로는 iPad가 앞으로 얼마나 더 나아질지를 보여주기 때문이에요.

# iPad가 (거의) 새로운 Mac이 되려나요?

2020년, 나는 첫 번째 Medium 기사를 쓰게 되었는데, 의외로 빠르게 인기를 끌었습니다. 기사 내용은 'iPad가 새로운 맥이 되다'였어요. 그때는 확실이 이상한 시기였지요. 여러 이유로 세상이 이상하게 변했죠. 여유로운 시간을 가지고 iPad에서 웹사이트를 디자인했어요. 스케치부터 디자인, 프로그래밍, 그리고 배포까지, 모두 iPad로 해냈답니다. iPad 경험이 정말 좋았고, 그 이후부터 특별한 연결을 느끼기 시작했어요.

과거를 떠나 2024년으로 시간을 돌려봅시다. 세상은 계속 변화하고 있었죠. iPad은 계속 발전해왔고, 특히 iPadOS 16 릴리스로 소프트웨어가 점점 더 좋아지고 있었어요. 그럼 현재 소식은 어떨까요?

# 스위프트 플레이그라운드, XCode Mini 또는 XCode Air라고도 불린다

WWDC 2021에서 애플이 Swift Playgrounds 4를 출시했습니다. 이는 개발자들이 iPad에서 직접 Swift를 사용하고 앱을 앱스토어에 출시할 수 있는 새로운 방법입니다.

아이패드에서 앱 프로그래밍을 시작한 순간이에요. 이전에는 Swift 코드로 놀았지만, 본격적인 프로젝트에서는 사용해본 적이 없었죠. 솔직히 말하자면, Swift Playgrounds를 사용하는 것은 즐겁습니다. 에디터에 입력한 모든 내용이 즉시 앱 미리보기 창에 반영되는 패러다임이 매력적이에요.

![image](https://miro.medium.com/v2/resize:fit:1400/1*GpCT9hqXNw9Ihan0J9MTsw.gif)

하지만 Swift Playgrounds에는 기본 기능이 있긴 하지만, 완벽한 XCode의 많은 기능이 빠져 있어요. 디버거도 없고, 프로파일러도 없고, 추가할 수 있는 엔터티들의 제한된 하위 집합이 있어요(예를 들어 푸시 알림 지원이나 WeatherKit 엔터티가 없습니다). Apple Watch 지원이 없고, 어떠한 종류의 확장기능도 없으므로 WidgetKit 지원도 없어요... 나중에 이에 대해 좀 더 얘기할게요. 이런 제한 사항 중 일부는 해결 방법을 찾을 수 있지만, 어떤 것들은 그렇지 않아요. 필요하다면, Swift Playgrounds Pro(아니, XCode를) 사용해야 해요.

# 예상치 못한 앱 제작 여정에서의 시작

제가 맡은것은 타입 1 당뇨병이에요. 이는 많은 추측을 필요로 합니다: 몇 그램의 탄수화물을 섭취했는지, 몇 단위의 인슐린이 필요한지. 이를 모두 저장하고, 과거 사건 및 현재 혈당 추세를 기반으로 예측하는 기능이 있는 앱을 만드는 것이 아이디어입니다.

(해당 앱의 구체적인 사항과 이 글 범위를 벗어나는 이유로, 아직 공개하지 않았습니다. 제가 확실하지 않은 부분이 있는데요 - 이것이 의료 앱으로 분류되거나 상점 제한 내에 들어가는지요. 그러나 사용하는 기반이 공개되어 있습니다. [참고: https://github.com/open-gluck], 그리고 iOS, iPadOS, watchOS 및 tvOS용으로 사용 가능한 모든 위젯을 지원하는 동반 앱을 전체 공개했습니다.)

## 나쁜 부분을 포함한 좋고 나쁜 점

Swift Playgrounds는 명백히 재미있는 사이드 프로젝트를 위해 설계되었습니다. 어떤 종류의 개발 경험이 있고 Swift를 배우려는 의지가 있다면, 설정이나 옵션이 여러 개 있어서 혼란스러울 필요가 없기 때문에 좋습니다. Swift를 이미 알고 있고 XCode가 복잡한 점을 알고 있더라도, Swift Playgrounds는 옵션이 없다는 것은 신비로운 오류를 해결할 필요가 없다는 것이므로 편안한 경험이 될 수 있습니다 (해당 경험을 한 적이 있다면 알 것입니다).

한편 인터페이스는 중대형 프로젝트를 고려하지 않은 것으로 보입니다(4.1 버전에서 이 부분이 크게 개선되었습니다, 자세한 내용은 아래에서 확인하세요). Swift 파일이 많은 경우, 주변을 이동하는 것이 최상의 경우에도 혼란스러울 수 있습니다.

![Image](https://miro.medium.com/v2/resize:fit:1366/1*Tjcp67dUaeLrgni3UuHypQ.gif)

## Swift Package Manager

좋은 소식입니다, Swift Playgrounds는 SPM 패키지를 사용할 수 있습니다. 이는 써드파티 패키지를 프로젝트에 쉽게 추가할 수 있다는 것을 의미합니다 (또는 제 경우에는 일부 공통적인 요소를 공유할 수 있음을 의미합니다).

안타깝게도, XCode에서와 같은 유연성을 완전히 누리실 수는 없어요. 기본적으로 패키지를 다음 주요 릴리스까지만 추적할 수 있고, 그게 전부에요. 브랜치를 추적할 수도 있지만, 그럼 "업데이트" 명령이 이상하게 작동을 멈출 거에요.

![이미지](/assets/img/2024-05-15-HowIwroteusingmyiPadoneofthelargestappsubmittedtoAppStoreConnect_2.png)

또 다른 안타까운 소식은, 가장 기본적인 Swift 소스 코드만을 제공하는 패키지만 추가할 수 있다는 거에요. 미리 빌드된 이진 파일을 다운로드하거나 코드를 컴파일하거나 멋진 기능을 하는 것들은 작동하지 않을 거에요. Firebase를 Playground에 추가하려고 했다면 그 생각을 그만두는 게 좋을 거에요.

![이미지](/assets/img/2024-05-15-HowIwroteusingmyiPadoneofthelargestappsubmittedtoAppStoreConnect_3.png)

그러나 잘 작동되면 아주 좋습니다. linting 및 패키징을 위한 GitHub Actions가 포함된 GitHub 저장소와 결합된 SPM 패키지는 일반 Xcode 프로젝트와 플레이그라운드 간에 코드를 공유하는 경우 유용한 강력한 도구 중 하나입니다.

## Git이 해결책

정직하게 말하면, iPad에서의 Swift 경험은 작업을 추적하는 데 도움이 되는 Working Copy와 같은 도구 없이는 같지 않을 것입니다. Anders Borum의 이 멋진 앱을 정말 좋아하는데요, 이 앱은 iPad에 Git을 가져다주는 데 도움을 줍니다.

Swift Playgrounds의 좋은 점은 모든 파일을 Files 앱에 저장한다는 것입니다. 그런 다음, Working Copy에 외부 디렉토리에 대한 링크를 지정할 수 있습니다. 이것은 다른 앱을 혼란스럽게 만들지 않기 위해 여기 작업 중인 디렉토리를 버전으로 관리하도록 지시하는 방법입니다만, 다른 파일(.git 디렉토리와 같은)을 여기에 두지 말아 주세요."

![HowIwroteusingmyiPadoneofthelargestappsubmittedtoAppStoreConnect_4.png](/assets/img/2024-05-15-HowIwroteusingmyiPadoneofthelargestappsubmittedtoAppStoreConnect_4.png)

Here we go! You now have the power of git on your iPad. You can tweak your playground, stash away things that aren't quite working out, branch out effortlessly, revert changes, create pull requests, and even review them on GitHub.

## Editing the hidden but valuable files in the playground bundle

And here's a neat trick: playgrounds come in bundles, so you can't peek inside them using the Files app. However, Working Copy will gladly display the bundle's contents, allowing you to add, edit, and manage individual files to your heart's content.

That's super helpful because it allows you to access and modify otherwise hidden files. For example, whenever you submit your app to the App Store, you'll be prompted to indicate if your app utilizes non-exempt encryption. By storing a plist file in the main directory of your bundle, you'll save yourself a lot of time in the future; otherwise, you'd have to manually check a box on the App Store platform for each release.

![How I wrote using my iPad one of the largest app submitted to App Store Connect](/assets/img/2024-05-15-HowIwroteusingmyiPadoneofthelargestappsubmittedtoAppStoreConnect_5.png)

It's important to note that this functionality isn't specific to Working Copy. You could achieve the same using other tools like a text editor (such as iVim) and navigating the bundle as a directory. The user-friendly interface of Working Copy simply makes the process much smoother. It would be fantastic if the Files app on iOS were to offer a "Show Package Contents" command similar to what's available on macOS.

# Swift Playgrounds Improves, One Feature at a Time

Swift Playgrounds 팀은 활발하지 않지만 최근 매우 인상적인 새로운 기능을 제공했습니다. 미디어에서 크게 주목받지는 않았지만, 이러한 기능 중 하나가 아마도 다음 iPadOS 출시 계획의 일환일 것으로 예상됩니다.

작은 변화 중 하나로 이제 Package.swift 파일을 편집할 필요 없이 최소 iOS 버전을 편집할 수 있습니다.

![이미지](/assets/img/2024-05-15-HowIwroteusingmyiPadoneofthelargestappsubmittedtoAppStoreConnect_6.png)

놀랍게도, 이제 Playgrounds 앱에서 빠른 작업을 할 수 있습니다. Command+Shift+A를 누르면 더 많은 작업을 수행할 수 있는 팝오버 메뉴가 표시되며, 해당 작업의 키보드 단축키도 표시됩니다.

이건 정말 흥미로운 이야기인 것 같네요. Quick Actions를 어디서나 사용할 수 있다니 정말 좋네요. 이 기능은 다른 앱들에서도 유용하게 쓰일 수 있고, Command 키를 누르면 나타나는 별로 쓸모 없는 팝오버를 대체할 수도 있겠네요. iPadOS의 다음 버전에 대한 전조일지도 모르겠네요...

Quick Actions과 함께 추가된 멋진 개선 사항 중 하나는 파일을 빠르게 열 수 있는 기능입니다. 코드가 점점 커지는데, 저에겐 명백히 삶을 바꿀 수 있는 기능이죠. Command+Shift+O를 누르면 팝오버가 즉시 나타납니다.

화면에 표시된 파일과 기호들을 보셨을지도 모르겠어요. 제게는 기호가 작동하지 않아요. 아마도 이것이 수정될 것인지, 아니면 기능이 너무 빨리 도입된 것인지는 잘 모르겠어요.

기호에 관해 얘기하자면, 자동완성 기능도 개선되었답니다. 이제 좋은 시각으로 기호 목록을 얻을 수 있어요.

![이미지](/assets/img/2024-05-15-HowIwroteusingmyiPadoneofthelargestappsubmittedtoAppStoreConnect_9.png)

# 스위프트 플레이그라운드 경험 향상하기

이제 스위프트 플레이그라운드를 더 잘 활용하기 위한 팁과 힌트를 알아보겠습니다.

## Package.json 편집

아이패드에서 플레이그라운드를 편집하기 위해 애플이 UI를 간소화했지만, 여전히 도구 체인은 macOS와 대부분 동일합니다 (두 세계를 통합한 ARM 덕분입니다). 이는 Mac에서 작동하는 대부분의 트릭이 아이패드에서도 작동한다는 뜻입니다.

예를 들어, 여기에 제 Package.json 파일이 있습니다. 손으로 편집하지 말라는 주석은 무시해주세요 (형식을 지키면 괜찮고, 변경 사항은 보존될 것입니다).

```json
// swift-tools-version: 5.7

// WARNING:
// This file is automatically generated.
// Do not edit it by hand because the contents will be replaced.

import PackageDescription
import AppleProductTypes

let package = Package(
name: "Diably",
platforms: [
.iOS("17.0")
],
products: [
.iOSApplication(
name: "Diably",
targets: ["AppModule"],
bundleIdentifier: "com.fc865c1a-c3d9-40a5-8dde-19d154d8ba90.diably",
teamIdentifier: "AAAAAAAAAA",
displayVersion: "2.23.6",
bundleVersion: "52",
appIcon: .asset("AppIcon"),
accentColor: .presetColor(.green),
supportedDeviceFamilies: [
.phone
],
supportedInterfaceOrientations: [
.portrait
],
additionalInfoPlistContentFilePath: "TrackerInfo.plist"
)
],
dependencies: [
.package(url: "https://github.com/open-gluck/OG.git", "1.0.90"..<"2.0.0")
],
targets: [
.executableTarget(
name: "AppModule",
dependencies: [
.product(name: "OG", package: "OG"),
.product(name: "OGUI", package: "OG")
],
path: ".",
resources: [
.process("Resources")
],
swiftSettings: [
.unsafeFlags(["-Xfrontend", "-strict-concurrency=complete", "-Xfrontend", "-warn-long-function-bodies=200", "-Xfrontend", "-warn-long-expression-type-checking=200"])
]
)
]
)

```

Let's start by addressing the obstacles: you cannot grant your app entitlements that the UI does not support.

Previously, modifying this file was the sole method to adjust the minimum iOS version supported by a playground. This value was hardcoded to the latest version supported by Swift Playgrounds at the time your project was created. Fortunately, it is now exposed as a setting in the UI.

There are other intriguing changes you can implement here. For instance, utilize the `additionalInfoPlistContentFilePath` property to add properties to your plist. This can be used to store confidential information or configuration data for the App Store approval procedure.

또 하나의 멋진 속성은 swiftSettings 플래그인데, Swift 컴파일러에 플래그를 전달할 수 있게 해줍니다. 이에 대한 자세한 내용은 아래 섹션에서 확인해보세요.

## Swift 컴파일 플래그 변경

저는 swiftSettings 플래그를 사용하여 컴파일러에 두가지 주요 작업을 요청하고 있어요:

- async/await를 사용한 동시 코드 사용에 관한 발견된 모든 경고를 제공해주세요,
- 내 코드가 왜 느려이 컴파일되고 있는지 찾아주실 수 있나요?

솔직히 말해서, 동시성에 대한 경고가 기본적으로 활성화되어 있을 것으로 기대했습니다. 사용자들이 디버거 없는 기기에서 충돌로 이어질 수 있는 나쁜 코드를 작성하게 하는 이유를 이해하지 못합니다.

## 증분 및 전체 빌드 최적화 방법

컴파일 시간에 대해, Playgrounds를 사용할 때 주요 고통 중 하나가 컴파일 속도입니다. 컴파일에 많은 전력이 필요하며, iPad에는 선풍기가 없고, 맥북과 비교할 때 배터리 용량이 매우 작습니다. 외출 중 앱 작업에 집중할 때, 배터리가 가장 길게 몇 시간밖에 가지 않을 것을 압니다.

그래서 코드가 가능한 빨리 컴파일되도록 실제로 확인하는 것이 중요합니다. 이를 위해, Swift Playgrounds가 앱을 두 가지 방법으로 컴파일한다는 것을 이해해야 합니다.

- 프로젝트를 처음으로 열 때 완전한 컴파일;
- 파일을 변경할 때 점진적으로 컴파일합니다.

이 방법들은 서로 다른 최적화 기술을 포함하고 있습니다. 완전한 컴파일을 사용하면 어떤 파일은 빠르게 컴파일 될 수 있지만, 증분 컴파일을 사용하면 시간이 오래 걸릴 수도 있습니다 (스위프트 컴파일러의 많은 버그 중 하나이지만, 시간이 지남에 따라 개선됩니다).

개발자로서 우리는 할 수 있는 일이 많지 않습니다. 컴파일 시간을 단축하는 가장 효율적인 방법 중 하나는 변수가 어떻게 타입되었는지에 대한 컴파일러에 맥락을 제공하는 것입니다. 그리고 경고를 통해 알림을 받는 한 가지 방법은 스위프트 컴파일러에 플래그를 추가하여 개선이 필요한 부분을 알려주는 것입니다.

이것이 warn-long-fonction-bodies와 warn-long-expression-type-checking의 목적이며, 아래 구성에 해당합니다:

.unsafeFlags(["-Xfrontend", "-strict-concurrency=complete", "-Xfrontend", "-warn-long-function-bodies=200", "-Xfrontend", "-warn-long-expression-type-checking=200"])

## 재부팅해 보셨나요?

때때로 Swift 컴파일러가 멈춰있을 때가 있습니다. 맥에서는 캐시를 정리하고 다시 빌드할 수 있지만, 아쉽게도 iPad에는 그런 기능이 없죠.

한 가지 생명을 구할 수 있는 꿀팁은 어딘가에 빈 줄을 추가하거나 제거하는 것입니다. 그렇게 하면 현재 파일의 증분 빌드가 즉시 트리거됩니다. 예를 들어 빠르게 몇 가지 변경을 했다가 빠트린 부분이 있을 때 유용하죠.

하지만 때로는 현재 파일을 다시 컴파일하는 것 이상이 필요할 때가 있습니다. 완전한 깨끗한 빌드가 필요합니다. 제 생각에는 플레이그라운드를 닫고 다시 열면 플레이그라운드의 전체 빌드가 트리거되지만 여전히 일부 컴파일 데이터가 캐시되는 것으로 보입니다.

그러나 플레이그라운드 앱을 종료하고 다시 열면 캐시가 지워지고 다른 증분 빌드를 사용하는 데 발생하는 버그가 해결됩니다.

마지막으로 한 가지 특이점: Swift Playgrounds는 기기에서 빌드에 서명하고 실제로 앱을 로컬에서 실행하기 위해 어떤 종류의 비공개 API를 사용하고 있다고 합니다. 이 프로세스에 가끔 버그가 있을 수도 있습니다. 앱을 전혀 시작할 수 없거나 뭔가 분명히 이상할 때는 기본 트릭을 사용하세요:

- 플레이그라운드 닫기
- 플레이그라운드 종료
- iPad 재시작

## 로깅

아이패드 개발 경험 중 빠져 있는 것 중 하나는 콘솔 앱입니다. 솔직히 말해서, 이에 대한 완벽한 해결책은 제가 가지고 있지 않습니다. 지금까지 제 선택은 로깅을 위해 사용하는 사용자 정의 클래스를 만들고, 그런 다음 앱 내에 로그를 표시하는 UI를 두어 필요 시 텍스트 편집기에서 자세히 검사할 수 있도록 '공유' 버튼을 넣는 것이었습니다.

![image](/assets/img/2024-05-15-HowIwroteusingmyiPadoneofthelargestappsubmittedtoAppStoreConnect_10.png)

산업 표준 수준은 아니지만 일을 해냅니다. 언젠가는 아이패드에 대해 더 나은 디버깅 지원이 되길 바라며 기대하고 있습니다.

## Advanced Frameworks 사용, Accelerate나 Charts 같은

아이패드에서 작업 중이면 우리는 Apple의 고급 프레임워크인 훌륭한 Swift Charts 프레임워크와 같은 고급 프레임워크에 접근할 수 없다는 뜻은 아닙니다.

앱을 작성하기 시작할 때, XCode에 특화된 것처럼 Swift Charts를 사용하는 것을 처음에는 즉시 생각하지 않았습니다. 물론 -- 그리고 희망적으로 -- XCode에 특화되어 있지 않아, 앱에 멋진 기능을 추가하는 좋은 방법이 됩니다.

![image](/assets/img/2024-05-15-HowIwroteusingmyiPadoneofthelargestappsubmittedtoAppStoreConnect_11.png)

더 좋은 점은 가속화(Accelerate)와 같은 저수준 프레임워크를 사용하여 그렇지 않을 경우 CPU 집약적인 코드의 속도를 높일 수 있다는 것입니다. 아마도 이것은 특별한 사례겠지만, 적어도 애플이 문을 열었다는 점에 기쁘게 생각합니다.

안전하지 않은 포인터, 하드웨어 가속 벡터 메트릭스? iPad로부터 모두 가능할까요? 가능합니다!

![이미지](/assets/img/2024-05-15-HowIwroteusingmyiPadoneofthelargestappsubmittedtoAppStoreConnect_12.png)

## 그럼... 아직 XCode 없이 만들 수 있을까요?

지금 문제는 이런 건데, iPad에서 실제로 진정한 발전을 이룰만큼 충분히 능력이 있는 걸까?

그래 답변하고 싶지만, 정말로 대답해야 하는 것은 아마 예, 어느 정도, 그리고 예, 하지만 우리가 해야 할까?

iPad를 A부터 Z까지 사용하는 것은 분명히 멋진 것입니다. 하지만 현실에서는 I에서 D까지일 것이거나, iPad Pro를 사용하고 있다면 I에서 O까지로 바뀔 것입니다. 몇 년전에는 상상조차 할 수 없었던 많은 것들이 지금은 가능해졌습니다. 그리고 반면에, 아직 부족한 부분이 많습니다.

iPad의 미래가 아직도 앞에 놓여 있어 보입니다. 안타깝게도 iPad 하드웨어는 점점 더 엄청난 것으로 발전하고 있지만, 소프트웨어는 계속해서 뒤쳐지고 있는 것 같습니다.

질문으로 돌아와서, 내가 앱을 개발하는 데 XCode를 사용했는지 궁금하신 거죠?

솔직히 말씀드리자면, 네, 사용했습니다. 하지만 여러분이 예상한 이유와는 조금 다를 수도 있어요. 어느 순간, 앱의 특정 부분의 성능을 향상시키려고 시도했었죠. 로그를 사용해 보았지만, 결과적으로 프로파일러를 이길 수는 없었습니다.

또 다른 시점에는, 내 코드가 예상대로 작동하지 않았고, 그 이유를 알 수 없었습니다. 더 많은 로그를 사용하다가 답을 찾을 수 없었어요. 다시 한 번 Mac을 사용했고, 디버거의 도움으로 무엇이 문제인지 바로 알 수 있었죠.

하지만 이상한 일이 일어났어요. Mac을 사용할 때, 코드를 작성하는 경험이... 그렇게 즐겁지 않았습니다. iPad에서의 Swift Playgrounds가 멋있고 깔끔했던 걸 좋아했어요—정말, iPad에서는 다른 생각 모드로 넣어주는 만큼 많은 것을 빼 주는 느낌이었어요. Mac에서 코딩하는 건 전통적인 작업 같았죠. 하지만 iPad에서 코딩하는 건 그 자체로 전혀 다른 경험이었어요. iPad에서 코딩하는 게 정말 신비로운 것이 있다고 느꼈죠.

참 멋진 비법이죠: Swift Playgrounds 앱은 iCloud에 플레이그라운드를 저장합니다. 이는 여러 기기, 맥과 아이패드에서 코드를 동기화하는 것이 쉽다는 것을 의미합니다. 프로젝트를 닫고 한 번에 하나의 기기에서만 열기만 하면 됩니다. XCode가 내부 파일을 변경하여 iOS가 충돌이 발생했다고 오해할 수 있으니 주의하세요.

# 다음 단계

이 기사를 쓸 당시, iPad Pro M4가 막 발표되었습니다. 거짓말 안 하고, 저는 이미 한 대를 예약했고 새 하드웨어의 성능 향상에 대해 보고하기를 고대하고 있습니다.

이전에 언급했던 바와 같이, 프로젝트가 커지면 컴파일 속도가 점점 느려집니다. 전체 컴파일에는 약 20~25초가 걸립니다.

새로운 iPad Pro에는 성능이 50% 빠르다고 하는 칩이 탑재되어 있어서, 단지 10초 정도 확보해도 인상적일 것 같아요. 두 배의 RAM 용량과 최대 CPU/GPU 코어 수를 활용하려면 적어도 1TB 저장 용량이 장착된 iPad Pro를 구매해야 한다는 것을 명심하세요.

제 iPad을 사용하여 앱을 개발하는 것은 전혀 생각하지 않았는데, 재미있기도 해서 즐기게 된 일이었어요.

저에게 있어 Swift Playgrounds의 최고 장점은 명확해요. 목적이 없어도 돼요. 그냥 재미있는 걸 해보고 어떤 결과가 나올지 보는 거죠.

하지만 쉬운 여정이었다는 건 아니에요. Swift나 개발에 대해 사전 지식이 없는 사람은 아마도 여러 문제와 함정을 마주할 것이고, "오, 재밌겠다"에서 금방 "이제 어떻게 해야 하나"로 넘어갈 거에요. 더 진보된 사용 사례에도 이는 사실이에요. 진보된 Swift Playgrounds 사용자 커뮤니티는 정말 작아요. 그래서 아마 (아직까지?) 플레이그라운드를 사용하는 프로젝트가 팀에서 인기를 얻을 가능성은 거의 없을 거에요.

하지만, Apple은 그겻을 바꿀 수 있는 힘이 있습니다. 단기적으로는, Swift Playgrounds에 지속적으로 작은 업데이트를 발표함으로써 도로를 제거함으로써 새로운 사용 사례가 더욱 즐거워지고 이 플랫폼의 사용자가 증가하는 것을 야기할 것입니다.

중장기적으로는, Swift Playgrounds의 도구 및 성능을 개선함으로써. 디버거? 더 나은 콘솔? 프로파일러? XCode와의 통합?

그리고, 장기적으로 - 비록 아직도 미진할 것 같지만 - iPad에 XCode가 마침내 등장하는 미래를 상상해볼 수는 없을까요?

이 이야기는 iPad에서 작성되었습니다. 그리고 디즈니 크루즈 중에도 작성되었으므로, 제 스크린샷에 숨겨진 미키쥬들을 모두 용서해 주세요.

자세히 읽어주셔서 감사합니다! 아이패드를 진지하게 활용하고 계신가요? 혹은 관심이 있으신가요? 이에 대한 여러분의 의견을 듣고 싶어요! 만약 이 아이디어에 관심이 있다면, 반가워하는 응원을 부탁드립니다!