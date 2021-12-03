```javascript

<script>

  //영어 페이지로 이동(한글->영어로)
  function engPage() {
	  window.location.href = '/front/use_kiosk/shuttle/shuttle_eng.do';
  }
  
  //popup창 닫기
  function closePopup() {
	  document.getElementById('popup1').style.display="none";
	  $('#popup1').html(" ");
  }
  
  //popup창 InnerHTML 사용해서 띄우기 & 음성재생
  function popupWindow(description, customerService, audioPath){
	// #popup1 를 display none => block 으로 바꾸기
	   document.getElementById('popup1').style.display="block"; 
	$('#popup1').append(
			'<div class="popup__header">'					
			+'<h2><span>셔틀버스 운행상황</span></h2>'
			+'</div>'
			
			+'<div class="popup__contents">'
			+'<strong>' + description + '</strong>'
			+'<p>'+ customerService +'</p>'
			+'</div>'
			
			+'<div class="popup__close">'
			+'<button type="button" class="close" onclick="closePopup()"></button>'
			+'</div>'
			+'<div class="audioMessage"><audio id="ttsPlayer" autoplay> <source src="/'+ audioPath +'"></audio></div>'
		
	  );//append
  }
  
  // 전역변수에 담아서 안내 내용 변경 유뮤 확인용
  var temdesc= "";
  // 전역변수로 popup창 일정시간 후 재등장 하도록 하기 위해 사용
  var countTime = 0;
  
  //
  function getCurrentDateTime(){
	  	  
	  $.ajax({
		  url : "/front/use_kiosk/tts/date/jsonObject.do", // 보낼 controller 
		  type : "GET",
		  contentType: "application/json",
	  		
		  success : function(data) {		  	
			  // console.log(data); //json object 확인용			  
			  var description = data.dateObject[0].description;
			  var customerService = data.dateObject[0].customerService;
			  var audioPath = data.dateObject[0].filePath;
			  
			  //.mp4 음성파일 경로 쪼갠후 필요한 부분만 결합
			  var splitPath = audioPath.split('/');
			  audioPath = splitPath[6] + "/" + splitPath[7];
			  
			  if(temdesc != description){
				  popupWindow(description, customerService, audioPath);
				  
			  } else{
				 countTime += 1;
				 //countTime이 10을 넘어가면 팝업창 다시 뜸
				 if(countTime >10){
					 closePopup();
					 countTime = 0;
					 popupWindow(description, customerService, audioPath);
					 
				 }
			  }
			  temdesc = description; //현재값과 과거값 비교용
		  },
		  
		  error : function(data) {
			  console.log("fail");
		  }
	  });
	
  }
 
  // 1초마다 안내방송 유무 체크
   setInterval(getCurrentDateTime, 1000); 

  </script>
```
