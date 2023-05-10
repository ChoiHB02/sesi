# 개요 
 
 - Unity 프로젝트 안에 구글 애드몹 미디에이션을 붙이기

--- 

<aside>
 
⚠️ 작성시기 2023년 05월

</aside>

--- 
<aside>
  
⚠️ Visual Studio 2022, Unity 2022.1.24f1, Google Cloud, Firebase, GooglePlay Console에서 진행되었습니다.

</aside>

--- 


소스트리
'git clone https://sesiprojectoregon@bitbucket.org/projectoregon/mytestbase.git'


# 목차

1. 광고 메디에이션(ADS Scene) <br>
2. 리더보드, 업적, 랭킹 등(GameService Scene) <br>
3. 파이어베이스 로그인 및 푸시, 결제(Login Scene) <br>
4. 구글 시트 파싱 (Parsing Scene) <br>
5. 구글 클라우드 JSON 세이브로드 (SaveLoad Scene) <br>
6. 오류 정리 <br>



<br><br><br>
# 0 타이틀 씬
처음 시작을 했을 때는 타이틀 씬이 가장 먼저 보일 것이다.
[사진]

여기서 원하는 기능을 실험하거나 테스트할 수 있다.


# 1 광고 메디에이션(ADS Scene) <br>

광고 메디에이션을 등록시키려면 밑에 있는 설명서를 참고한다.
[광고 메디에이션](https://github.com/SesisoftTFT/Schedule/blob/main/Mediation.md)



# 2 리더보드, 업적, 랭킹 등(GameService Scene)<br>

먼저 현재 GooglePlayGamesPlugin 플러그인이 설치가 되어 있다. 현재는 로그인 문제로 인해 play-games-plugin-for-unity-10.14버전을 사용하고 있다.<br>
하지만 잘 되던 것이 갑자기 오류가 날 경우 업데이트 문제일 수 도 있으니 GooglePlayGames 폴더를 삭제하고 따로 플러그인을 임포트 해줘야한다.<br><br>

플러그인 문제가 없거나 마무리 했으면 웹에서 세팅을 해줘야한다.<br>

[구글 콘솔 개발자](https://play.google.com/console/u/0/developers)<br>

먼저 위에 있는 사이트에 들어가서 로그인을 해준다.<br>


[사진 GameService2] <br>


그리고 앱 만들기 버튼을 눌러서 리더보드와 업적 같은 설정을 해줄 앱을 만들어준다.<br><br>
앱 설정은 나중에 바꿀 수 있으니 대충 빠르게 만들어준다.<br><br>


[사진 GameService1] <br>

그리고 Play 게임즈 서비스를 통해서 리더보드나 업적을 설정해줘야하는데<br>
만약 보이지 않는다면, 위의 검색창을 통해서 Play 게임즈 서비스를 복붙한후 들어가면 활성화를 할 수 있다.<br><br>

[사진 GameService3]<br>

그리고 사용자 인증 정보 추가를 눌러서 OAuth 클라이언트를 추가를 해줘야 한다.

[사진 GameService4]<br>

이제 구글 플레이 콘솔과 클라우드를 연동 시켜야 되는데 먼저 위의 사진에서 가르키고 있는 링크로 간다.
그러면 구글 클라우드로 이동하게 되는데 구글 클라우드를 로그인하거나 가입을 해야한다.


[사진 GameService5]<br>

클라우드에 성공적으로 들어왔으면 위의 사진을 보고 '사용자 인증 정보'로 이동한다.

[사진 GameService6]<br>

구글 플레이 콘솔에서 요구하는 것은 OAuth 클라이언트였다 그러니 OAuth 클라이언트 ID를 만들어준다.<br>
애플리케이션 유형은 'Android'로 설정하고 패키지 이름과 SHA-1 인증서 디지털 지문을 해줘야하는데<br>


[사진 GameService7]<br>

유저키와 CMD로 SHA-1 인증서를 뽑아내야하기 때문에 방법은 아래의 링크를 따라한다.<br>
https://cafe.naver.com/sesisoftdev/25 <br>

만약 파이어베이스와 동시에 사용하고 싶다면,<br>
파이어베이스(https://firebase.google.com/?hl=ko&authuser=0)는 SHA-256 인증서 코드로 바꿔주고 클라우드는 SHA-1 인증서 코드를 사용하면 된다.<br>
자세한건 https://cafe.naver.com/sesisoftdev/26 를 살펴보도록 하자.<br>

[사진 GameService8]<br>

이제 구글 플레이 콘솔에 들어가서 OAuth 클라이언트 새로고침을 한다면 아까 만들었던 클라이언트의 이름이 뜨게 될 겁니다. <br>
그럼 업적과 리더보드, 이벤트를 만들 준비가 되었습니다.<br>


[사진 GameService9]<br>

이렇게 업적과 리더보드, 이벤트를 각각 만들어줬으면<br>


[사진 GameService10]<br>

업적, 이벤트, 리더보드, 설정 창들 중 어디든 리소스 보기가 있고 다 똑같으니 리소스 보기를 눌러서 <br>
코드를 복사해준다.

[사진 GameService11]<br>

그런 다음 위의 사진에 있는 경로에 따라서 Android Setup에 들어가 주게 되면 <br>

[사진 GameService11]<br>

위에 같은 하나 창이 뜨게 되는데 순서대로 1은 아까 복사한 리소스 코드를 붙여넣고 2는 아까 만들었던 OAuth 클라이언트에서 클라이언트 ID를 갖고 온다.<br>
물론 Google play console이나 Google Cloud에 똑같은게 있으니 둘 중 하나를 찾아서 붙이기를 하고 마지막으로 Setup 버튼을 누르면 GPGSIds라는 스크립트가 생기게 된다.<br>

이것을 기반으로 코드를 수정하거나 추가하면 된다.<br>

===========================================================================================================


# 3 파이어베이스 로그인 및 푸시, 결제(Login Scene)<br>

현재 이 씬에서는 게스트 로그인, 구글 로그인, 인앱 결제, 로그인 토큰 저장의 기능이 들어있다.
지금은 google-services 파일이 작성자의 것으로 되어 있기 때문에 
자신의 유저키를 바꾸고 파이어베이스 사이트에서 유저키의 SHA-1을 넣어서 새로운 google-services 파일을 넣어야
바뀔 것이다.

그 부분은 [파이어베이스 깃허브](https://github.com/SesisoftTFT/Schedule/blob/main/FireBase%20%EA%B8%B0%EB%8A%A5%EC%9D%B8%20Auth,%20Message%20SDK%EB%A5%BC%20%EC%B6%94%EA%B0%80%ED%95%98%EC%97%AC%20%ED%99%9C%EC%84%B1%ED%99%94.md) 를 참고하도록 하자



# 4 구글 시트 파싱 (Parsing Scene)<br>



# 5 구글 클라우드 JSON 세이브로드 (SaveLoad Scene)<br>



# 6 오류 정리 <br>




