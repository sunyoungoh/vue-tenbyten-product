# mytt

텐바이텐에 입점된 판매자가 판매 상태와 상품 상세 페이지 내용을 수정할 수 있고, 디지털 작가 시 신규 주문 내역을 확인 및 상품 파일, 메일 템플릿을 등록할 수 있는 서비스입니다.

<br>

## 🌐 배포 사이트
https://mytt.netlify.app/

![image](https://github.com/sunyoungoh/mytt/assets/52486921/2d7bd53f-3803-4d04-b5fc-48e8b46084df)


<br>

## 🪄 기술 스택
- Vue2
- Vuex
- Vuetify
- crypto-js
- vue-quill-editor
<br>

- supabase
- Node.js (express) [🔗 GitHub Link](https://github.com/sunyoungoh/send-mail-server)
<br>

## 📚 API
[텐바이텐 API](https://api.10x10.co.kr/document/docs.html)

<br>

## 👀 어쩌다 개발하게 됐는지?
친구와 함께 텐바이텐 상품 이미지 등록 시 html 코드 등록 방식을 사용 중이었는데, 링크를 가져오는 사이트인 이글루스라는 블로그 서비스가 종료되어 새로운 이미지 호스팅 사이트가 필요하게 되었습니다.
이미지 호스팅 사이트를 찾아 교체해도 되지만 어드민 로그인의 번거로움, 상품 하나 수정을 위해 여러번의 클릭. 이 과정을 단순화 해보고 싶어 개발을 하게 되었습니다.
친구는 코딩을 잘 모르는 친구라서 시각화 하는 것이 좋다는 판단이 들어 `quill editor`를 사용하기로 결정하였고, 에디터 안의 이미지를 서버리스 `supabase`의 storage에 등록되도록 만들었습니다.
이외의 기본적인 상품 내용 수정은 직접 구축한 Node.js 서버를 통해 처리합니다.

<br>

## 🍀 기능
> 페이지 단위 설명
#### 🔐 Login - 로그인
  - supabase DB에 등록된 사용자만 로그인 가능
  - 로그인 시 crpyto-js로 API키 암호화
  - Vuetify v-form validation 기능
    - 필드가 비어있을 시 에러 메시지 표시
    - 로그인하기 버튼 disabled
  - Node.js 백엔드 서버로 api키 확인 요청 후 로그인 처리
  - Navigation Guards 사용으로 미 로그인 시 타 페이지 접근 불가
#### 🏠 Home - 텐바이텐에 등록된 상품 조회, 검색
  - 상품이미지, 상품명, 판매상태 표시
    - 로그인 후 홈 화면 진입 시 vuex actions의 `fetchItem()`를 통해 state에 상품 리스트 저장
      - 한 번에 100개씩만 요청할 수 있어서 while문을 통해 push
    - 이미지는 fetchItems 결과에 포함되지 않아 `ItemCard` 컴포넌트에서 별도 api 요청
      - 이미지 로딩 시 로딩 스피너 동작
  - 상품명 검색으로 필터링
    - 검색 키워드와 개수, 상품 표시
#### 📦 Item - 상품 상세 페이지 수정
  - 상품 판매 상태, 구분, 상세내용, 재질, 사이즈 수정
    - Node.js 백엔드 서버를 통해 텐바이텐 API로 요청
  - 상세 내용 quill editor로 작성
    - html 코드 보기 (toggle)
  - 메일 템플릿, 파일 supabase 등록 및 삭제 (디지털 작가만)
#### 🛒 Order - 주문 조회 (디지털 작가만)
  - 메일 발송 및 송장 등록
    - Node.js 백엔드 서버를 통해 `nodemailer`로 메일 발송 후 텐바이텐 API로 송장 등록 처리
#### 👤 Mypage - 마이페이지
  - 네이버 메일 발송 계정 등록 (디지털 작가만)
  - 로그아웃


<br>

<br>

## 🎬 시연 영상

### 반응형

- 홈 화면
<img src="https://github.com/sunyoungoh/mytt/assets/52486921/7b9cdcdf-3444-4110-8ce4-f89cb10d8a5a" width="500px"/>

- 수정 페이지 (show/hide ItemNav)
<img src="https://github.com/sunyoungoh/mytt/assets/52486921/21f1d310-a187-484b-beb6-c934adc45a4f" width="500px"/>

<br><br>

### 로그인 페이지

- 로그인 과정 (supabase에 등록된 사용자만 로그인 가능)
<img src="https://github.com/sunyoungoh/mytt/assets/52486921/5c80c73b-5bf5-4b28-a90e-c0785a5795f1" width="500px"/>

<br><br>

### 홈 페이지

- 상품명 검색
  
<img src="https://github.com/sunyoungoh/mytt/assets/52486921/f3726d8c-d974-4c18-ac17-60d3f67ba1c7" width="500px"/>

<br><br>

### 상품 수정 페이지

- 상품 내용 수정

<img src="https://github.com/sunyoungoh/mytt/assets/52486921/dbe5fcfb-ffec-4677-b17b-3b141e9fccdd" width="500px"/>

- 상세 내용 HTML 코드 직접 수정
<img src="https://github.com/sunyoungoh/mytt/assets/52486921/a9fdaf1a-55e2-4cc8-b00b-53896472a1cb" width="500px"/>

- 디지털 파일 다운로드 및 삭제 (supabase에 저장된 zip 파일)

| 기존 파일 다운로드 | 기존 파일 삭제 |
| --- | --- |
| ![IMB_abC23m](https://github.com/sunyoungoh/mytt/assets/52486921/8b18e952-67e1-4a92-a301-4ba307c63d6c) | ![IMB_shDFUJ](https://github.com/sunyoungoh/mytt/assets/52486921/78e9b329-f3e5-4bd1-987f-c4a033419337) |

- 이미지 등록 (supabase 이미지 업로드)

![IMB_JMqnr1](https://github.com/sunyoungoh/mytt/assets/52486921/5fdc4fb9-8bd2-4fac-aaba-e95c7975f541)

- 등록하기 후 결과 모달

<img src="https://github.com/sunyoungoh/mytt/assets/52486921/0e30d182-4dc3-4ae6-a92f-bf6e8e9b2893" width="500px"/>

<br><br>

### 주문 내역 (디지털 작가만 보임)

- 주문 확인

![image](https://github.com/sunyoungoh/mytt/assets/52486921/ec529391-f80f-4b6e-9659-7a206d930837)

- supabase DB에 등록된 템플릿과 파일로 메일 발송

![image](https://github.com/sunyoungoh/mytt/assets/52486921/b20a5cd6-3e8f-4e07-9e5a-395f7e327ac6)

<br><br>

### 마이페이지

- 네이버 이메일 계정 수정
- 로그아웃
 
<img src="https://github.com/sunyoungoh/mytt/assets/52486921/defc5dfe-d62d-45b2-a1ed-cb8e22b1c4c0" width="500px"/>


