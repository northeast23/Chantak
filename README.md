
# 요리 레시피를 해외에서 현지 식재료로 제공하는 사이트 

## 1. 목표와 기능

### 1.1 목표
-  

### 1.2 기능
-  
 

### 1.3 팀 구성
- 실제 사진을 업로드 하시길 권합니다.
<table>
	<tr>
		<th>이호준</th>
		<th>이호준</th>
		<th>이호준</th>
	</tr>
 	<tr>
		<td><img src="my.jpg" width="100%"></td>
		<td><img src="my.jpg" width="100%"></td>
		<td><img src="my.jpg" width="100%"></td>
	</tr>
</table>

## 2. 개발 환경 및 배포 URL
### 2.1 개발 환경
- Web Framework
  - Django 5.0 (Python 3.8)
- 서비스 배포 환경
  - Amazon Lightsail
...중략...
### 2.2 배포 URL
- https://northeast23.github.com/Chantak
- 테스트용 계정
  ```
  id : test@test.test
  pw : test11!!
  ```

### 2.3 URL 구조(모놀리식)
- main

| App       | URL                                        | Views Function    | HTML File Name                        | Note           |
|-----------|--------------------------------------------|-------------------|---------------------------------------|----------------|
| main      | '/'                                        | home              | main/home.html                        | 홈화면          |
| main      | '/about/'                                  | about             | main/about.html                       | 소개화면               |


- accounts

| App       | URL                                        | Views Function    | HTML File Name                        | Note           |
|-----------|--------------------------------------------|-------------------|---------------------------------------|----------------|
| accounts  | 'register/'                                | register          | accounts/register.html                |회원가입         |
| accounts  | 'login/'                                   | login             | accounts/login.html                   |로그인           |
| accounts  | 'logout/'                                  | logout            | accounts/logout.html                  |로그아웃         |
| accounts  | 'profile/'                                 | profile           | accounts/profile.html                 | 비밀번호변경기능 / <br>프로필 수정/ 닉네임추가 |


- boardapp

| App       | URL                                        | Views Function    | HTML File Name                        | Note           |
|-----------|--------------------------------------------|-------------------|---------------------------------------|----------------|
| board     | 'board/'                                   | board             | boardapp/post_list.html               | 게시판 목록 |
| board     | 'board/<int:pk>/'                          | post_detail       | boardapp/post_detail.html            | 게시글 상세보기 |
| board     | 'board/write/'                             | post_write        | boardapp/post_write.html             | 게시글 작성 |
| board     | 'board/edit/<int:pk>/'                     | post_edit         | boardapp/post_edit.html              | 게시글 수정 |
| board     | 'board/delete/<int:pk>/'                   | post_delete       | boardapp/post_delete.html            | 게시글 삭제 |
| board     | 'board/<int:pk>/comment/'                  | comment_create    | boardapp/comment_form.html           | 댓글 작성 |
| board     | 'board/<int:pk>/comment/<br><int:comment_pk>/edit/' | comment_edit | boardapp/comment_form.html           | 댓글 수정 |
| board     | 'board/<int:pk>/comment/<br><int:comment_pk>/delete/' | comment_delete | boardapp/comment_<br>confirm_delete.html| 댓글 삭제 |


- blog


| App       | URL                                        | Views Function    | HTML File Name                        | Note           |
|-----------|--------------------------------------------|-------------------|---------------------------------------|----------------|
| blog      | 'blog/'                                    | blog              | blog/blog.html                        |갤러리형 게시판 메인 화면  |
| blog      | 'blog/<int:pk>/'                           | post              | blog/post.html                        |상세 포스트 화면    |
| blog      | 'blog/write/'                              | write             | blog/write.html                       | 카테고리 지정, 사진업로드,<br> 게시글 조회수 반영|
| blog      | 'blog/edit/<int:pk>/'                      | edit              | blog/edit.html                        | 게시물목록보기 |
| blog      | 'blog/delete/<int:pk>/'                    | delete            | blog/delete.html                      | 삭제 화면      |
| blog      | 'blog/search/'                             | search            | blog/search.html                      | 주제와 카테고리에 따라 검색,<br> 시간순에 따라 정렬|
| blog      | 'post/<int:post_pk>/comment/'              | comment_new       | blog/comment_form.html                | 댓글 입력 폼     |
| blog      | 'post/<int:post_pk>/comment/<br><int:parent_pk>/' | reply_new    | blog/comment_form.html                | 대댓글 폼      |
| blog      | 'post/<int:pk>/like/'                      | like_post         | blog/post.html                        |좋아요를 누르면 blog/post로 Redirect됨|
| blog      | 'comment/<int:pk>/update/'                 | comment_update    | blog/comment_form.html                |댓글 업데이터 경로   |
| blog      | 'comment/<int:pk>/delete/'                 | comment_delete    | blog/comment_<br>confirm_delete.html      |댓글 삭제 폼    |

### 2.4 URL 구조(마이크로식)

* views의 이름과 views에 믹스인 한 것이 있으면 함께 언급하면 좋습니다.

|app:accounts|HTTP Method|설명|로그인 권한 필요|작성자 권한 필요|
|:-|:-|:-|:-:|:-:|
|signup/|POST|회원가입|||
|login/|POST|로그인|||
|logout/|POST|로그아웃| ✅ ||
|\<int:pk\>/|GET|프로필 조회| ✅ ||
|\<int:pk\>/|PUT|프로필 수정| ✅ | ✅ |
|\<int:pk\>/|DELETE|회원 탈퇴| ✅ | ✅ |
|status/|GET|로그인 상태 확인|||
|token/refresh/|POST|만료 토큰 재발급|||
<br>  

|app:blog|HTTP Method|설명|로그인 권한 필요|작성자 권한 필요|
|:-|:-|:-|:-:|:-:|
|list/|GET|게시판 리스트| ✅ ||
|create/|POST|게시물 작성| ✅ ||
<br>

|app:interview|HTTP Method|설명|로그인 권한 필요|작성자 권한 필요|
|:-|:-|:-|:-:|:-:|
|question/|POST|면접 문제 요청| ✅ ||
|grading/|POST|면접 문제 채점| ✅ ||
|total/|POST|면접 점수 통계| ✅ ||
<br>

* 아래와 같이 표현할 수도 있습니다.

| App       | Method        | URL                               | Views Class        | Note           |
|-----------|---------------|-----------------------------------|------------------- |----------------|
| blog  | GET   | '/blog/posts/'                         |   PostViewSet                 |게시글 목록 |
| blog  | POST   | '/blog/posts/'                       |   PostViewSet                 |게시글 생성 / ChatGPT API 요청 |
| blog  | GET   | '/blog/posts/{post_id}/'                |    PostViewSet       |게시글 상세보기 / 게시글 조회수 증가 |
| blog  | PATCH   | '/blog/posts/{post_id}/'                  |   PostViewSet    |게시글 수정 |
| blog  | DELETE   | '/blog/posts/{post_id}/'                   |  PostViewSet    |게시글 삭제 |
| blog  | POST   | '/blog/posts/{post_id}/like/'                   |   PostViewSet    |게시글 좋아요 증가|
| blog  | GET   | '/blog/posts/{post_id}/comments/'                   |   CommentViewSet    | 게시물의 댓글 목록 |
| blog  | POST   | '/blog/posts/{post_id}/comments/'                   |   CommentViewSet    | 게시물의 댓글 생성 |
| blog  | GET   | '/blog/posts/{post_id}/comments/{comment_id}/'       |   CommentViewSet    | 게시물의 특정 댓글 보기 |
| blog  | PATCH   | '/blog/posts/{post_id}/comments/{comment_id}/'       |   CommentViewSet    | 게시물의 특정 댓글 수정 |
| blog  | DELETE   | '/blog/posts/{post_id}/comments/{comment_id}/'       |   CommentViewSet    | 게시물의 특정 댓글 삭제 |
<br>

|URL|페이지 설명|GET|POST|PUT|DELETE|로그인 권한| 작성자 권한|
|------|---|:---:|:---:|:---:|:---:|:---:|:---:|
|/accounts/login|로그인| |✔️| | | | |
|/accounts/logout|로그아웃| |✔️| | | | |
|/accounts/signup|회원가입| |✔️| | | | |
|/accounts/profile|프로필 <br> 프로필 수정 <br> 회원 탈퇴|✔️<br> <br> <br>| |✔️|<br><br>✔️|✔️ <br> ✔️ <br> ✔️|<br> ✔️ <br> ✔️
|/accounts/token/refresh|토큰갱신| |✔️| | | | |
|/board|게시글 목록 <br> 게시글 생성|✔️<br><br>|<br>✔️| | | <br> ✔️| |
|/board/{postid}|게시글 상세 <br> 게시글 수정 <br> 게시글 삭제|✔️<br><br><br>| |✔️|<br><br>✔️| <br> ✔️ <br> ✔️ | <br> ✔️ <br> ✔️
<br>

## 3. 요구사항 명세와 기능 명세
- https://www.mindmeister.com/ 등을 사용하여 모델링 및 요구사항 명세를 시각화하면 좋습니다.
- 이미지는 셈플 이미지입니다.
<img src="map.png" width="100%">
- 머메이드를 이용해 시각화 할 수 있습니다.
  
```mermaid
    sequenceDiagram
    actor A as client
    participant B as Web
    participant C as server
    A->>+B: 로그인 요청
    B->>+A: 로그인 정보 요구
    A->>+C: id, pw 전달
    alt 로그인 정보가 있고 로그인 정보가 맞을 시
    C->>+B: access token, refresh token 전달
    B->>+A: 로그인 성공
    else 로그인 정보가 없거나 정보가 맞지 않을시
    C->>+B: False
    B->>+A: 로그인 실패
    end
```

## 4. 프로젝트 구조와 개발 일정
### 4.1 프로젝트 구조
- 해당 프로젝트에서 폴더 트리 잘 다듬어 사용하세요. 필요하다면 주석을 달아주세요.
📦tutorial  
 ┣ 📂accounts  
 ┃ ┣ 📂migrations  
 ┃ ┣ 📂__pycache__  
 ┃ ┣ 📜admin.py  
 ┃ ┣ 📜apps.py  
 ┃ ┣ 📜forms.py  
 ┃ ┣ 📜models.py  
 ┃ ┣ 📜tests.py  
 ┃ ┣ 📜urls.py  
 ┃ ┣ 📜views.py  
 ┃ ┗ 📜__init__.py  
 ┣ 📂blog  
 ┃ ┣ 📂migrations  
 ┃ ┣ 📂__pycache__  
 ┃ ┣ 📜admin.py  
 ┃ ┣ 📜apps.py  
 ┃ ┣ 📜forms.py  
 ┃ ┣ 📜models.py  
 ┃ ┣ 📜tests.py  
 ┃ ┣ 📜urls.py  
 ┃ ┣ 📜views.py  
 ┃ ┗ 📜__init__.py  
 ┣ 📂board  
 ┃ ┣ 📂migrations  
 ┃ ┣ 📂__pycache__  
 ┃ ┣ 📜admin.py  
 ┃ ┣ 📜apps.py  
 ┃ ┣ 📜forms.py  
 ┃ ┣ 📜models.py  
 ┃ ┣ 📜tests.py  
 ┃ ┣ 📜urls.py  
 ┃ ┣ 📜views.py  
 ┃ ┗ 📜__init__.py  
 ┣ 📂main  
 ┃ ┣ 📂migrations  
 ┃ ┣ 📂__pycache__  
 ┃ ┣ 📜admin.py  
 ┃ ┣ 📜apps.py  
 ┃ ┣ 📜models.py  
 ┃ ┣ 📜tests.py  
 ┃ ┣ 📜urls.py  
 ┃ ┣ 📜views.py  
 ┃ ┗ 📜__init__.py  
 ┣ 📂media  
 ┃ ┣ 📂accounts  
 ┃ ┣ 📂blog  
 ┃ ┗ 📂board  
 ┣ 📂static  
 ┃ ┣ 📂assets  
 ┃ ┃ ┣ 📂css  
 ┃ ┃ ┃ ┣ 📂apps  
 ┃ ┃ ┃ ┣ 📂authentication  
 ┃ ┃ ┃ ┣ 📂components  
 ┃ ┃ ┃ ┣ 📂dashboard  
 ┃ ┃ ┃ ┣ 📂elements  
 ┃ ┃ ┃ ┣ 📂forms  
 ┃ ┃ ┃ ┣ 📂pages  
 ┃ ┃ ┃ ┣ 📂tables  
 ┃ ┃ ┃ ┣ 📂users  
 ┃ ┃ ┣ 📂images  
 ┃ ┃ ┃ ┣ 📂mockup_image  
 ┃ ┃ ┣ 📂img  
 ┃ ┃ ┗ 📂js  
 ┃ ┣ 📂bootstrap  
 ┃ ┃ ┣ 📂css  
 ┃ ┃ ┗ 📂js  
 ┃ ┗ 📂plugins  
 ┣ 📂tech_blog  
 ┃ ┣ 📂__pycache__  
 ┃ ┣ 📜.env  
 ┃ ┣ 📜asgi.py  
 ┃ ┣ 📜settings.py  
 ┃ ┣ 📜urls.py  
 ┃ ┣ 📜wsgi.py  
 ┃ ┗ 📜__init__.py  
 ┣ 📂templates  
 ┃ ┣ 📂accounts  
 ┃ ┃ ┣ 📜login.html  
 ┃ ┃ ┣ 📜password_change.html  
 ┃ ┃ ┣ 📜profile.html  
 ┃ ┃ ┣ 📜profile_edit.html  
 ┃ ┃ ┣ 📜signup.html  
 ┃ ┃ ┗ 📜user_list.html  
 ┃ ┣ 📂blog  
 ┃ ┃ ┣ 📜blog_base.html  
 ┃ ┃ ┣ 📜post_detail.html  
 ┃ ┃ ┣ 📜post_form.html  
 ┃ ┃ ┣ 📜post_list.html  
 ┃ ┃ ┗ 📜post_not_found.html  
 ┃ ┣ 📂board  
 ┃ ┃ ┣ 📜board_base.html  
 ┃ ┃ ┣ 📜board_post_detail.html  
 ┃ ┃ ┣ 📜board_post_form.html  
 ┃ ┃ ┗ 📜board_post_list.html  
 ┃ ┣ 📂main  
 ┃ ┃ ┗ 📜index.html  
 ┃ ┣ 📜404.html  
 ┃ ┗ 📜base.html  
 ┣ 📜CONVENTION.md  
 ┣ 📜db.sqlite3  
 ┣ 📜manage.py  
 ┣ 📜README.md  
 ┗ 📜requirements.txt  

### 4.1 개발 일정(WBS)
* 아래 일정표는 머메이드로 작성했습니다.
```mermaid
gantt
    title Chantak
    dateFormat  YY-MM-DD
    excludes weekends

    section 기획 
    환경설정   :a1, 24-02-13, 0.2d
    사이트기획 :a2, 24-02-13, 1d

    section 프론트엔드(FE)
    chatGPT 연결 및 프롬프트 테스트 : 24-02-13, 1d
    home 화면 : 24-02-14, 1d
    로그인/로그아웃 : 24-02-15, 1d
    회원가입 페이지 : 24-02-16, 1d
    인증 접근 권한 : 24-02-19, 3d
    유저 추가 : 24-02-22, 1d
    프로필 페이지 : 24-02-23, 1d    
    
    section 백엔드(BE)
    chatGPT 연결 및 프롬프트 테스트 : 24-02-13, 1d
    home 화면 : 24-02-14, 1d
    로그인/로그아웃 : 24-02-15, 1d
    회원가입 페이지 : 24-02-16, 1d
    인증 접근 권한 : 24-02-19, 3d
    유저 추가 : 24-02-22, 1d
    프로필 페이지 : 24-02-23, 1d    
```

## 5. 역할 분담

- 팀장 : 이호준
- FE : 이오름
- FE : 김코딩
- BE : northeast23
- BE : 박캠프
- 디자인 : 기안

## 6. 와이어프레임 / UI / BM

### 6.1 와이어프레임
- 아래 페이지별 상세 설명, 더 큰 이미지로 하나하나씩 설명 필요
<img src="ui.png" width="60%">

- 와이어 프레임은 디자인을 할 수 있다면 '피그마'를, 디자인을 할 수 없다면 '카카오 오븐'으로 쉽게 만들 수 있습니다.

### 6.2 화면 설계
- 화면은 gif파일로 업로드해주세요.
 
<table>
    <tbody>
        <tr>
            <td>메인</td>
            <td>로그인</td>
        </tr>
        <tr>
            <td>
		<img src="ui1.png" width="100%">
            </td>
            <td>
                <img src="ui2.png" width="100%">
            </td>
        </tr>
        <tr>
            <td>회원가입</td>
            <td>정보수정</td>
        </tr>
        <tr>
            <td>
                <img src="ui3.png" width="100%">
            </td>
            <td>
                <img src="ui3.png" width="100%">
            </td>
        </tr>
        <tr>
            <td>검색</td>
            <td>번역</td>
        </tr>
        <tr>
            <td>
                <img src="ui3.png" width="100%">
            </td>
            <td>
                <img src="ui3.png" width="100%">
            </td>
        </tr>
        <tr>
            <td>선택삭제</td>
            <td>글쓰기</td>
        </tr>
        <tr>
            <td>
	        <img src="ui3.png" width="100%">
            </td>
            <td>
                <img src="ui3.png" width="100%">
            </td>
        </tr>
        <tr>
            <td>글 상세보기</td>
            <td>댓글</td>
        </tr>
        <tr>
            <td>
                <img src="ui3.png" width="100%">
            </td>
            <td>
                <img src="ui3.png" width="100%">
            </td>
        </tr>
    </tbody>
</table>


## 7. 데이터베이스 모델링(ERD)

* 아래 ERD는 머메이드를 사용했습니다.
```mermaid
erDiagram
    user ||--o{ post : write
    user {
      integer id PK
      varchar username
      varchar password
      image profile_image
      datetime created_at
      varchar ip_address
      datetime last_login
    }
    post }|--|{ tag : contains
    post ||--o| category : has
    post {
      integer id PK
      varchar title
      text content
      file file_upload
      image image_upload
      datetime created_at
      datetime updated_at
      varchar writer
      integer user_id FK
      integer hits
      integer tags FK
      varchar category FK
    }
    post ||--o{ comment : contains
    comment ||--o{ comment : contains
    comment {
      integer id PK
      integer parent FK
      text comment
      comment comment_reply FK
      datetime created_at
      datetime updated_at
    }
    
    tag {
      integer id PK
      varchar name
    }
    
    
    category {
      integer id PK
      varchar name
    }
```

* 아래 ERD는 [ERDCloud](https://www.erdcloud.com/)를 사용했습니다.
<img src="erd.png" width="60%">

* https://dbdiagram.io/home도 많이 사용합니다.

## 8. Architecture

* 아래 Architecture 설계도는 ChatGPT에게 아키텍처를 설명하고 mermaid로 그려달라 요청한 것입니다.
```mermaid
graph TD;
    CI[GitHub CI/CD] -->|Deploys| LS[AWS Lightsail];
    A[Django Application] -->|Uses| DRF[Django REST Framework];
    A -->|Real-time communication| C[Django Channels];
    C -->|Messaging backend| R[Redis];
    A -->|Connects to| DB[postgresql];
    A -->|Static & Media Files| S3[AWS S3];
    FE[Frontend] -->|Deployed on| LS;
    LS -->|Hosts| A;
    LS -->|Hosts| FE;

    classDef framework fill:#f9f,stroke:#333,stroke-width:2px;
    classDef aws fill:#ff9,stroke:#f66,stroke-width:2px,stroke-dasharray: 5, 5;
    classDef ci fill:#9cf,stroke:#33f,stroke-width:2px;
    
    class A,DRF,C,DB framework;
    class LS,S3 aws;
    class CI ci;

```

* 아래 Architecture 설계도는 PPT를 사용했습니다.
  
![image](./architecture.png)

- PPT로 간단하게 작성하였으나, 아키텍쳐가 커지거나, 상세한 내용이 필요할 경우 [AWS architecture Tool](https://online.visual-paradigm.com/ko/diagrams/features/aws-architecture-diagram-tool/)을 사용하기도 합니다.

## 9. 메인 기능
- 



```mermaid
		graph TD
	    A[하루 시작] -->|일어난다| B(세수한다)
	    B --> C{오늘은 무엇을 할까}
	    C -->|밥을 먹는다| D[냉장고 확인]
	    C -->|다시 잔다| E[침대로 돌아가기]
	    C -->|티비를 본다| F[거실로 가기]
```

```mermaid
		sequenceDiagram
	    A->>+B: B야 소금좀 건내줘
	    B->>+A: 여기
	    A-->>-B: 고마워
```

```mermaid
		stateDiagram-v2
	    [*] --> 로그인
	    로그인 --> 성공
	    로그인 --> 실패
	    실패 --> 아이디/비밀번호찾기
	    아이디/비밀번호찾기 --> 로그인재시도
	    로그인재시도 --> 성공
	    성공 --> [*]
```

## 10. 에러와 에러 해결
-  
## 10. 개발하며 느낀점
