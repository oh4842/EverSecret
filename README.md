# EverSecret

## Android_Prject / Spring_boot / Tomcat

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
