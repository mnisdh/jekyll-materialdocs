---
layout: post
title:  "Java mySql"
date:   2017-03-01 09:00:00 +0800
categories: Java
tags: Java mySql
comments: 1
---
**Connector 설치**  
- osx의 경우 [Connector/j](https://dev.mysql.com/downloads/connector/j/5.1.html)를 다운로드한다
- 이클립스 프로젝트 속성 - Java build path - Libraries - Add External jre로 다운받은 파일 추가하면 완료


**사용법**  
드라이버 동적 로드 :
{% highlight java linenos %}
public ModelWithDB(){
	// 특정 컴퓨터를 찾기위한 주소 체계
	// 아이피 = 213.12.142.132
	// url = naver.com
	//
	// 특정 프로그램에 할당되는 세부 번지
	// port = 1 ~ 6만번대
	//        2000번대 밑은 이미 표준으로 사용되고 있다.
	//
	// 소켓 : 아이피 + 포트

	// 표준 프로토콜
	// http://아이피(주소) : 포트(80)

	// 특정 프로그램에 액세스 하기위한 주소체계
	// 프로토콜이름 :// 아이피(주소) : 포트

	// ("데이터베이스주소","아이디","비밀번호")
	try{
		Class.forName("com.mysql.jdbc.Driver"); //드라이버를 동적으로 로드
	}catch(Exception ex){
		ex.printStackTrace();
	}
}
{% endhighlight %}


Connection 맺기 :
{% highlight java linenos %}
private final String URL = "jdbc:mysql://localhost:3306/memo";
private final String USER = "root";
private final String PASS = "root";

private Connection getConnection(){
	try{
		return DriverManager.getConnection(URL, USER, PASS);
	}catch(Exception ex){
		System.out.println("접속실패");
		ex.printStackTrace();
	}

	return null;
}
{% endhighlight %}


Statement를 사용한 쿼리실행 :
{% highlight java linenos %}
public ArrayList<Memo> getList(){

	ArrayList<Memo> list = new ArrayList<Memo>();

	// 1. 데이터베이스 연결
	Connection conn = getConnection();
	if(conn ==null) return list;

	// 2. 쿼리를 실행
	try{
		// 2.1 쿼리 생성
		String sql = " select * from memo ";
		// 2.2 쿼리를 실행 가능한 상태로 만들어준다
		Statement stmt = conn.createStatement();
		// 2.3 select한 결과값을 돌려받기 위해 쿼리를 실행
		ResultSet rs = stmt.executeQuery(sql);
		// 결과셋을 반복하면서 하나씩 꺼낼 수 있다
		while(rs.next()){
			Memo memo = new Memo(rs.getString("name"), rs.getString("content"));
			memo.setNo(rs.getInt("no"));
			memo.setDatetime(rs.getLong("datetime"));

			list.add(memo);
		}

		// 3. 데이터베이스 연결해제
		conn.close();
	}catch(Exception ex){
		ex.printStackTrace();
	}

	return list;
}
{% endhighlight %}


PreparedStatement를 사용한 쿼리실행(Statement 보다 속도가 빠르다) :
{% highlight java linenos %}
public void create(Memo memo){
	// 1. 데이터베이스 연결
	Connection conn = getConnection();
	if(conn ==null) return;

	// 2. 쿼리를 실행
	try{
		// 2.1 쿼리 생성
		String sql = " insert into memo(name,content,datetime) values(?,?,?) ";

		// 2.2 쿼리를 실행 가능한 상태로 만들어준다
		PreparedStatement pstmt = conn.prepareStatement(sql);
		// 2.3 물음표에 값을 세팅
		pstmt.setString(1, memo.getName());
		pstmt.setString(2, memo.getContent());
		pstmt.setTimestamp(3, new Timestamp( System.currentTimeMillis()));
		// 2.4 쿼리를 실행
		pstmt.executeUpdate();

		// 3. 데이터베이스 연결해제
		conn.close();
	}catch(Exception ex){
		ex.printStackTrace();
	}
}
{% endhighlight %}