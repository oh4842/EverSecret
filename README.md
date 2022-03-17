# EverSecret

## Android / Spring / Tomcat / Mysql

### **--목적--**

  + 최근 직장인들과 대학생들을 위한 'Blind', '에브리타임' 등의 익명 커뮤니티가 인기를 끌고 있다.
  + 조사 중 초·중·고 학생들을 위한 익명 커뮤니티가 있었으면 좋겠다라는 생각에서 프로젝트를 진행했다.

### **--개발환경--**

  + **IDE** : Android Studio, Eclipse
  + **Frond-End** : Android / Java
  + **Back-End** : JSP / Spring Framework 4.3
  + **DB** : MySql

### **--기대효과--**

  + 초·중·고 학생들을 위한 익명 커뮤니티가 생김으로 전혀 얼굴도 몰랐던 다른 반, 학교 친구와도 교류가 가능할 것으로 보인다.
  + 학교폭력과 같은 고발들을 익명으로 함으로써 다른 사람들의 도움을 받을 수 있다.
  + 부모님, 선생님에게 말하기 힘든 고민거리를 이야기 함으로써 소통의 장으로 될 수 있다.

### **--주요 내용--**

  + 익명 커뮤니티 구성을 위해 먼저 회원가입과 로그인이 필요함.
  + DB 정보를 받아올 수 있는 서버를 JSP + Spring FrameWork 4.3을 이용하여 구현한다.
  + DB는 MySql을 사용하며 Spring FrameWork와 Mybatis를 이용하여 매핑한다.
  + DB에 회원정보를 받지만 익명 게시판 등에서는 해당 회원의 닉네임을 노출시키지 않는다.
  + 안드로이드 기본 디자인은 UI나 접근성이 떨어져서 포토샾을 이용하여 커스텀 바, 탭, 버튼 디자인 등을 구현한다.

### **--DB 구조도--**

  + --Member Table--


  ![member_table](https://user-images.githubusercontent.com/32236195/127333519-5332c8ca-fb14-4b20-aa32-f3a58b457f97.png)

---

  + --Board Table--

  ![Board_Table](https://user-images.githubusercontent.com/32236195/127333523-e2f054bd-caf2-46f5-b607-51b1ece0fbeb.png)
  
---

  + --School Table--

  ![School_Table](https://user-images.githubusercontent.com/32236195/127333525-1e983b0d-a3d4-4280-9b47-d7d2de51f201.png)
  
### **--회원가입--**


![SignUp](https://user-images.githubusercontent.com/32236195/127333527-e72554dc-9994-4aad-b329-e9d826b9c9e7.png)

### **--로그인--**


![Login](https://user-images.githubusercontent.com/32236195/127333534-305e38b6-c2b2-4620-84d4-38fe2cc3a9c1.png)

### **--학교 위치 확인--**


![School_Gps](https://user-images.githubusercontent.com/32236195/127333528-694b5553-8395-4725-b500-d2520704de93.png)

### **--글 작성--**


![Write](https://user-images.githubusercontent.com/32236195/127333530-71f6f3da-8006-45f3-90b9-ad9082731e84.png)


### **--글 확인--**


![BoardChk](https://user-images.githubusercontent.com/32236195/127333532-2c9cf579-b7f0-450e-acee-ca0962eb3d9f.png)

### **--좌측 슬라이드 바--**


![SideBar](https://user-images.githubusercontent.com/32236195/127333536-463bd77e-8bba-480a-8f13-13344caa1fc5.png)

## **--Code--**

  + 대부분 Class들이 BoardCreat와 비슷한 형식으로 구현되어있다.

### **--HttpClient.java--**

  + Spring과의 데이터 연동을 위해 HTTP 통신을 사용하기 위해 사용하는 클래스로
  + https://coding-factory.tistory.com/32 | 코딩팩토리에서 가져와서 사용한다.

### **--IP_and_Port.java--**

  + 개발 시 매 번 바뀌는 유동 IP를 일일이 클래스마다 고칠 수 없어서 만든 부분

```java
public class IP_and_Port {

    public String getIp() {
        return "192.168.000.000";
    }

    public String getPort() {
        return "8081";
    }
}
```

### **--BoardCreat.java--**

  + Map 형식으로 담아서 Json으로 보내주기 위함.
  + HTTP 통신을 위한 IP, Port가 입력된 클래스를 가져온다.
  + HTTP를 연결한 후 Spring Controller에서 처리된 값을 가져온다.

```java
public class BoardCreat extends AsyncTask<Map<String, String>, Integer, String> {

    @Override
    protected String doInBackground(Map<String, String>... maps) {
        IP_and_Port ipAndPort = new IP_and_Port();
        String ip = ipAndPort.getIp();
        String port = ipAndPort.getPort();
        HttpClient.Builder http = new HttpClient.Builder("POST", "http://" + ip + ":" + port + "/secret/board_create");
        http.addAllParameters(maps[0]);

        HttpClient post = http.create();
        post.request();

        int statusCode = post.getHttpStatusCode();

        // 응답 본문 가져오기
        String body = post.getBody();

        return body; // return 되면 아래의 onPostExecute의 인수로 넘어감
    }
}
```
### **--BoardCreatFragment.java--**

  + 버튼이 클릭 되었을 때 각각의 EditText에 입력된 값들을 Map에 넣어 보내고 화면 전환

```java
public void onClick(View v) {
strtitle = title.getText().toString().trim();
strcontent = content.getText().toString();

try {
  BoardCreat boardCreat = new BoardCreat();
  Map<String, String> params = new HashMap<String, String>();
  params.put("title", strtitle);
  params.put("content", strcontent);
  params.put("writer", bundle.getString("nickname"));

  boardCreat.execute(params);
  Toast.makeText(getActivity(), "등록 완료!", Toast.LENGTH_SHORT);

  FreeBoardFrgment freeBoardFrgment = new FreeBoardFrgment();
  freeBoardFrgment.setArguments(getArguments());
  ((MainActivity)getActivity()).replaceFragment(freeBoardFrgment);
  }catch (Exception e){
    e.printStackTrace();
  }
}
```
