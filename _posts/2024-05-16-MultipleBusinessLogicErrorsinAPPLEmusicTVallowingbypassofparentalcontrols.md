---
title: "애플 뮤직 TV에서 부모 관리 기능 우회 가능한 비즈니스 논리 오류 다수 발견"
description: ""
coverImage: "/assets/img/2024-05-16-MultipleBusinessLogicErrorsinAPPLEmusicTVallowingbypassofparentalcontrols_0.png"
date: 2024-05-16 09:31
ogImage: 
  url: /assets/img/2024-05-16-MultipleBusinessLogicErrorsinAPPLEmusicTVallowingbypassofparentalcontrols_0.png
tag: Tech
originalTitle: "Multiple Business Logic Errors in APPLE music TV allowing bypass of parental controls"
link: "https://medium.com/@sam0-0/multiple-business-logic-errors-in-apple-music-tv-allowing-bypass-of-parental-controls-0d870d4870c5"
---


안녕하세요 테크 열정이 가득한 여러분! 소중한 시간을 낭비하지 않고 함께 글을 시작해봅시다!

요즘 Apple은 부모 관리 기능을 사용하여 어린이나 십대가 부적절한 콘텐츠에 접근하는 것을 막고 있어요. 이 기능을 부모만 알고 있는 핀을 사용하여 부적절한 콘텐츠에 접근할 수 있어요. 그래서 어떤 간단한 방법이라도 있는 걸까요? 다른 사람들이 쉽게 할 수 있는 만큼 간단한 방법이 있는데요, 저는 부모 관리 기능을 우회하는 여러 가지 방법을 찾아보았어요. 한 번 알아보도록 할깅요!

- 부모 관리 설정을 연결하면 우회할 수 있어요!

제가 발견한 로직 흐름을 확인해보세요. Apple music 웹사이트에서 부모 관리 잠금을 걸면 music.apple.com에서만 콘텐츠를 제한하는데요. 만약 어린이나 십대가 부적절한 콘텐츠를 잠금하려는 부모라고 상상해봅시다. 단지 부모 잠금을 걸고 끝나는 줄 알았지만, Apple에서는 그렇지 않습니다. 만약 부모가 music.apple.com에 부모 잠금을 건다면, 이 웹사이트의 콘텐츠만 제한하고, 이건 대부분의 사용자들과 심지어 저도 모르죠. 그래서 이제 어린이는 Apple music/tv 애플리케이션을 사용하여 Apple music 웹사이트에 부모 관리가 적용되어 있어도 부적절한 콘텐츠를 볼 수 있어요. 그래서 저는 14-3-24일에 같은 문제를 Apple에 신고했고 하루 후에 '의도한 대로 작동하고 있다'는 회신을 받았답니다. 이번에는 그들이 맞았어요! Apple의 웹페이지에 '이 콘텐츠 제한은 Apple TV 및 웹의 Apple Music에 적용됩니다. 다른 기기에서의 재생은 제한되지 않습니다'라는 문구를 놓친 걸로 보이네요.



![Image](/assets/img/2024-05-16-MultipleBusinessLogicErrorsinAPPLEmusicTVallowingbypassofparentalcontrols_0.png)

Hey there!

Let's chat a bit about an interesting discovery related to Apple Music's parental controls. It seems that Apple is utilizing different controls for the Apple Music app and the Apple Music web version, both operating independently. Here's the catch: setting parental controls on the Apple Music website (music.apple.com) doesn't apply those controls on the Apple Music app. 

When exploring ways to bypass these parental controls through the mobile app, I initially hit a dead end. However, upon closer investigation of the traffic flow within Apple Music, a fascinating observation came to light. Adjusting settings in the Apple Music app also impacts the Apple Music website. This could potentially allow a teen to alter the music settings through the app without requiring any authentication. 

So, even if parental controls are enabled on the Apple Music website, a child could simply launch the Apple Music app, tweak the settings, and potentially access inappropriate content. This contradicts Apple's claim that content restrictions only apply to Apple TV and Apple Music on the web. 

After compiling a detailed report to share with Apple, I encountered an unexpected issue while trying to create a proof-of-concept video. The changes made in the Apple Music app didn't seem to reflect on the Apple Music website. Did I miss something or was it just a hiccup in the flow of things? Quite a disappointment, right?

Stay tuned for more intriguing insights!



3. 이제 제목을 명확하게 해보죠: “이 내용 제한은 웹 상의 Apple TV와 Apple Music에 적용됩니다. 다른 장치에서는 재생을 제한하지 않습니다.”

음악.apple.com에서는 예상대로 작동하고 있는 것 같습니다. 사용자에게는 음악.apple.com에서만 제한된 내용을 제공한다는 라인이 표시되어 있기 때문입니다. 이제 Apple Music 응용 프로그램에서의 가정용 장치 흐름을 확인해 보았습니다. Apple Music 앱에 적용된 가정용 제어 설정이 오직 앱 내에서만 콘텐츠를 제한한다는 정보나 라인이 없습니다. 그러므로 부모로서는 가정용 제어를 설정하고 간단히 당신의 자녀가 제한된 콘텐츠에 액세스할 수 없을 거라고 생각할 것입니다. 앱에서는 작동하지만 웹에서 작동하지 않는다는 경고가 없습니다. 자녀는 웹 Apple Music에 접속하여 제한된 콘텐츠를 볼 수 있습니다. [간단한 우회 방법이군요]! 이제 어떡해요? 애플은 단순한 라인으로 제보를 거절했으므로 이제 그들에게 제보할 수 있습니다. 그리고 놀랍게도 이에 대한 답변을 받았는데, [엄청난 실망]:

[여기 이름] tarafından kaydedilen iyi bir POC videosu varsa göz atmak isterseniz: [YouTube 동영상 링크]

<div>
[동영상 이미지]
</div>



그들이 그것을 피드백으로 신고하라고 요청하네요! 정말요?

4. 동일한 공격 흐름에 또 다른 버그가 추가되었네요 😵

이제 근본적인 원인을 명확히 찾았고 재현 단계도 매우 간단해 보여요. 이제 한 번 살펴봅시다. 가정에서 부모가 Apple Music 앱의 자녀 관리 설정을 활성화했다고 가정해 봅시다. 그리고 십대 아이가 제한된 콘텐츠를 보고 싶어한다면, 애플리케이션에서 로그아웃한 후 다시 로그인하면 부모 관리 설정이 앱에서 사라지게 되는군요. 비슷한 방법으로, 아이는 Apple Music 애플리케이션을 제거하고 다시 설치하거나 단순히 설정에서 앱 데이터를 지우는 것으로 부모 관리 설정을 제거할 수 있어요. 이제 다시 새로운 버그처럼 보이네요. 그렇죠? 이러한 버그의 근본 원인은 Apple Music 애플리케이션이 클라이언트 측 확인을 사용하여 사용자가 음란 콘텐츠를 볼 수 있는지 여부를 확인하려고 한다는 점입니다. 다음은 그 흐름이에요:

![피드백 이미지](/assets/img/2024-05-16-MultipleBusinessLogicErrorsinAPPLEmusicTVallowingbypassofparentalcontrols_2.png)



이 문제의 근본 원인은 앱이 클라이언트 측에서 부모 관리 설정을 TRUE 또는 FALSE 조건으로만 확인하기 때문에 로그아웃한 다음 다시 로그인하면 매우 쉽게 우회할 수 있다는 것입니다.

이에 대해 애플에 적절한 공격 시나리오와 함께 제보한 결과를 살펴봤습니다. 그들의 응답은 이랬어요:

![Multiple Business Logic Errors in APPLE music TV allowing bypass of parental controls](/assets/img/2024-05-16-MultipleBusinessLogicErrorsinAPPLEmusicTVallowingbypassofparentalcontrols_3.png) 

그들은 이를 애플에 피드백으로 제보해야 한다고 지속적으로 말했습니다. 정말 응답을 기대 안 했어요. 애플, 왜 그래요? 😥 제가 정말 많은 시간을 투자한 후에 이런 결정을 받아서 정말 실망스럽습니다! 애플의 이 결정에 동의하지 않습니다. 여러분은 어떻게 생각하시나요? 여러분이 애플의 이 결정에 대한 의견을 남겨주셔도 좋습니다. 애플이 그것이 피드백이 아니라 버그라는 것을 알 수 있도록! 😂



그리고 멋진 얘기도 하더라구요! 애플에 따르면 "부모 관제는 보안 기능이 아니에요" 뭔가 쿨하죠! 😂

![이미지](/assets/img/2024-05-16-MultipleBusinessLogicErrorsinAPPLEmusicTVallowingbypassofparentalcontrols_4.png)

마지막으로, 이 문제를 그대로 내버려두고 공개적으로 공개해 모두가 알 수 있도록 하기로 했습니다!

타임라인:



**[보고서]**  
▪ 초기 발견 보고: 14/3/24  
▪ WAI로 거부됨: 14/3/24  
▪ 작동 중인 버그 보고: 16/3/24  
▪ 피드백으로 보고하도록 요청됨: 16/3/24  

보고서 내용을 Markdown 형식으로 바꿔봤어요. 😉



한 가지 더 버그 신고를 했는데, 이번에는 다른 루트 원인이었어요: 18/4/24

반려되었는데, 피드백으로 신고하라고 하셨어요: 19/4/24

공개 일자: 14/5/24

트위터[X]에서 제 소식을 팔로우할 수 있어요: __Sam0_0, 여기서 더 많은 글을 올릴 거에요!



감사합니다!