```java
package com.br;

import java.io.BufferedReader;
import java.io.DataOutputStream;
import java.io.File;
import java.io.FileOutputStream;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.OutputStream;
import java.net.HttpURLConnection;
import java.net.URL;
import java.net.URLEncoder;
import java.util.Date;

public class Tts {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
        try {        
	    Date currentDate = new Date();
  	    SimpleDateFormat saveFileDate = new SimpleDateFormat("yyyyMMddhhmmssSSS");	
	    
            String text = "<speak> 형돈이가 랩을한다 호옹 홍 홍~ 지용이가 랩을한다 호옹 호옹 호우. </speak>"; 	//xml 형태
            String apiURL = "https://kakaoi-newtone-openapi.kakao.com/v1/synthesize";		//api url
            URL url = new URL(apiURL);
            HttpURLConnection con = (HttpURLConnection)url.openConnection();
            con.setRequestMethod("POST");
            con.setRequestProperty("Content-Type", "application/xml");		// kakao api 가이드 참고
            con.setRequestProperty("Authorization", "KakaoAK {API_KEY}");	// KakaoAK뒤로 공백후 api key 값
            // post request
            String postParams = text;
            con.setDoOutput(true);
            DataOutputStream wr = new DataOutputStream(con.getOutputStream());
            //wr.writeBytes(postParams);
            wr.write(postParams.getBytes("utf-8"));
            wr.flush();
            wr.close();
            con.connect();
            int responseCode = con.getResponseCode();
            
            System.out.println("1:"+con.getResponseCode());
            System.out.println("2:"+con.getResponseMessage());
            
            BufferedReader br;
            if(responseCode==200) { // 정상 호출
                InputStream is = con.getInputStream();
                int read = 0;
                byte[] bytes = new byte[1024];
                // 현재 날짜 이름으로 mp3 파일 생성
                String saveFileName = saveFileDate.format(currentDate);
                File f = new File("E:\\"+saveFileName + ".mp3");
                f.createNewFile();
                OutputStream outputStream = new FileOutputStream(f);
                while ((read =is.read(bytes)) != -1) {
                    outputStream.write(bytes, 0, read);
                }
                is.close();
            } else {  // 에러 발생
                br = new BufferedReader(new InputStreamReader(con.getErrorStream()));
                String inputLine;
                StringBuffer response = new StringBuffer();
                while ((inputLine = br.readLine()) != null) {
                    response.append(inputLine);
                }
                br.close();
                System.out.println(response.toString());
            }
        } catch (Exception e) {
            e.printStackTrace();
        }



	}

}

```
