# Kakao_Text_to_speecch

### 음성 -> REST-API -> 음성 합성하기 = TTS (Request 참고)

[카카오 API 문서 확인] : (https://developers.kakao.com/docs/latest/ko/voice/rest-api#text-to-speech)

- 설명 : 음성 내용을 ```request``` 하고 ```Response```로 ```Code 200```을 받는다면 ```.mp3``` 음성파일로 지정한 경로에 다운로드

<hr>


### 음성안내 팝업 사용의 예시 이미지
![121434134134](https://user-images.githubusercontent.com/73927761/144533734-88a66b0d-839a-431e-ba65-5c66e3ac9bee.png)


1. Json으로 필요한 값을 받아서 팝업창에서 사용 
2. 안내팝업을 종료해도 설정한 시간에 따라 다시 재등장
3. setTimeInterval을 사용하여 설정한 시간마다 안내내용의 변경 유무를 파악함
4. 안내팝업이 재등장시 창이 여러개로 겹치지 않도록 현재 팝업창을 닫고 다시 띄우는 형태
5. <audio>태그로 autoplay를 사용하여 팝업 등장시 자동으로 내용을 읽어줌.

<hr>
  
### Json 내용
<!--![41131313](https://user-images.githubusercontent.com/73927761/144533923-355f456f-30e0-4690-9aa9-ac362b323dba.png) -->
