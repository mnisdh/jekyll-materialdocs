---
layout: post
title:  "Java File I/O"
date:   2017-03-01 09:00:00 +0800
categories: Java
tags: Java File I/O
comments: 1
---
**File I/O**  

Input :
{% highlight java linenos %}
public ArrayList<Memo> getList(){
	list.clear();

	// 1. 읽는 스트림을 연다
	try(FileInputStream fis = new FileInputStream(database)){
		// 2. 실제 파일 인코딩을 바꿔주는 래퍼 클래스 사용
		InputStreamReader isr = new InputStreamReader(fis, "UTF-8");

		// 3. 버퍼처리
		BufferedReader br = new BufferedReader(isr);

		// readLine이 null이 아닐때까지 실행
		String row;
		while((row = br.readLine()) != null){
			String[] tempRow = row.split(COLUMN_SEP);
			if(tempRow.length == 4){
				Memo memo = new Memo(tempRow[1], tempRow[2]);
				memo.setNo(Integer.parseInt(tempRow[0]));
				memo.setDatetime(Long.parseLong(tempRow[3]));

				list.add(memo);
			}
		}
		br.close();
		isr.close();
	}catch(Exception ex){
		ex.printStackTrace();
	}

	return list;
}
{% endhighlight %}


Output :
{% highlight java linenos %}
public void create(Memo memo){
	int newCount = getCount() + 1;
	memo.setNo(newCount);

	// memo 객체의 내용을 파일에 쓴다
	FileOutputStream fos = null;

	//try with문법 ( ) 안의 객체는 문법종료 후 자동으로 close해줌
	//try(FileOutputStream fos = new FileOutputStream(database, true))
	try{
		// 1. 쓰는 스트림을 연다
		fos = new FileOutputStream(database, true);

		// 2. 스트림 중간처리를 함(인코딩 변경 등....)
		OutputStreamWriter osw = new OutputStreamWriter(fos);

		// 3. 버퍼처리
		BufferedWriter bw = new BufferedWriter(osw);

		// 저장할 내용을 구분자로 분리하여 한줄의 문자열로 바꾼다
		String str = memo.getNo() + COLUMN_SEP;
				 str += memo.getName() + COLUMN_SEP;
				 str += memo.getContent() + COLUMN_SEP;
				 str += memo.getDatetimeLong() + "\n";

		bw.append(str);
		bw.close();
		osw.close();

		updateCount(newCount);
	} catch(Exception ex) {
		ex.printStackTrace();
	} finally {
		// 스트림이 생성되기전에 오류가 발생할 수 있으므로 null 체크 필요
		if(fos != null){
			try {
				fos.close();
			} catch(Exception ex) {
				ex.printStackTrace();
			}
		}
	}
}
{% endhighlight %}