```xml
<!-- 선택한 날짜 사이에 있는 값 select (ex start_date = 2021-12-01 , end_date = 2021-12-30 일때 현재(NOW())날짜가 시작시간과 종료시간 사이값일시 select) -->
<select id="selectTts" parameterType="java.util.HashMap" resultType="TtsVo">
		SELECT TTS_TITLE, DESCRIPTION, FILE_PATH, CUSTOMER_SERVICE FROM tb_tts
		WHERE 
			NOW() <![CDATA[>]]> start_date AND NOW() <![CDATA[<]]> end_date
		
		ORDER BY TTS_SEQ DESC
		
	</select>
  
```
