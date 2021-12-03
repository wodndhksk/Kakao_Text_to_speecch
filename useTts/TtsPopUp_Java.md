```java

/**
	 * 실시간 안내 팝업
	 * @param fullDateTime
	 * @return
	 * @throws Exception 
	 */
	@RequestMapping(value=MENU_ROOT_URL+"tts/date/jsonObject.do" ,  method = RequestMethod.GET)	
	@ResponseBody
	public Map<String, Object> videoJSONList(HttpServletRequest req, HttpServletResponse res /*, @RequestBody Map<String,String> fullDateTime*/) { //throws Exception{	
	try {
		Map<String, Object> addParam = new HashMap<>();
		addParam.put("CONTENT_TYPE", CONTENT_TYPE);
		
		Map<String, Object> jsonSubObject = new HashMap<String, Object>();
    		//json형태로 ttsVo객체를 뿌려준다.
		jsonSubObject.put("dateObject", _ttsDao.selectTts(addParam));

		return jsonSubObject;	
    
	}catch(Exception e){
		e.printStackTrace();
	}
	return null;
}

```
