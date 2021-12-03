# Kakao_Text_to_speecch

### 음성 -> REST-API -> 음성 합성하기 = TTS (Request 참고)

[카카오 API 문서 확인] : (https://developers.kakao.com/docs/latest/ko/voice/rest-api#text-to-speech)

- 설명 : 음성 내용을 ```request``` 하고 ```Response```로 ```Code 200```을 받는다면 ```.mp3``` 음성파일로 지정한 경로에 다운로드




### 음성안내 팝업 사용의 예시 이미지
![ddddddddddd](https://user-images.githubusercontent.com/73927761/144531475-2fac1629-66ed-4239-b404-dcf98824c04a.png)

1. Json으로 필요한 값을 받아서 팝업창에서 사용 
2. 안내팝업을 종료해도 설정한 시간에 따라 다시 재등장
3. setTimeInterval을 사용하여 설정한 시간마다 안내내용의 변경 유무를 파악함
4. 안내팝업이 재등장시 창이 여러개로 겹치지 않도록 현재 팝업창을 닫고 다시 띄우는 형태
5. <audio>태그로 autoplay를 사용하여 팝업 등장시 자동으로 내용을 읽어줌.
