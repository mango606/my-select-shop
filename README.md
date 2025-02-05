# 🏬MySelectShop

## 프로젝트 실행 영상
https://github.com/user-attachments/assets/79f4d487-44ff-46fb-a676-8295c9d3660c

## 🛠️프로젝트 기술 스택

### 프로그래밍 언어
- **Java 17**

### 프레임워크 및 라이브러리
- **Spring Boot 3.4.2**
- **Spring Data JPA**
- **Spring Security**
- **Thymeleaf**
- **Validation**
- **JWT**
- **Lombok**

<br>

## 📒프로젝트 요구사항

### 1. 키워드로 상품 정보 검색

- **네이버 쇼핑 API 활용**
  - 필수 파라미터: 상품 이름 (title), 링크 URL (link), 이미지 URL (image), 최저가 (lprice)

### 2. 관심 상품 등록

- **데이터베이스 상품 정보 입력**
  - 상세 정보: 상품 이름 (title), 링크 URL (link), 이미지 URL (image), 최저가 (lprice)
  - 초기 희망 최저가 (myprice)를 0원으로 설정

### 3. 관심 상품의 "희망 최저가" 설정

- **데이터베이스 업데이트 작업**
  - 등록된 관심 상품의 "희망 최저가" (myprice)만 업데이트

### 4. 관심 상품 조회

- **데이터베이스 조회 작업**
  - 등록된 모든 관심 상품 정보 조회
- **UI 표시 조건**
  - 실제 최저가가 희망 최저가보다 낮은 경우 최저가 표시

### 5. 관심상품 API 구현

- **관심상품 등록**
- **관심상품 희망 최저가 업데이트**
- **관심상품 조회**

### 6. 스케줄러 구현

- 매일 새벽 1시에 관심 상품 목록의 제목을 사용하여 최저가 정보를 업데이트하는 스케줄러 구현

### 7. 회원 기능 구현

### 8. 회원별 상품 API 구현

### 9. 상품 페이징 및 정렬

- **페이징 및 정렬 설계**
  - 상품 조회 API (GET /api/products) 수정

### 10. 상품 폴더 설계

1. **폴더 생성**
   - 회원별로 폴더 추가 가능
   - 한 번에 여러 개의 폴더를 추가할 수 있음

2. **관심 상품에 폴더 설정**
   - 관심 상품에 N개의 폴더를 설정 가능
   - 상품이 등록될 때 폴더에 저장되지 않음
   - 관심 상품 별로 이전에 생성한 폴더 선택하여 추가 가능

3. **폴더별 조회**
   - 회원은 폴더별로 관심 상품 조회 가능
   - 조회 방법:
     - **'전체'**: 폴더와 상관 없이 모든 관심 상품 조회 가능
     - **'폴더명'**: 폴더별 저장된 관심 상품 조회 가능

<br>

## 📜API 문서

### Folder API

| 기능                         | HTTP Method | URL            | Request                           | Response                |
|----------------------------|-------------|----------------|-----------------------------------|-------------------------|
| 폴더 추가                   | POST        | /api/folders   | `{ "folderNames": [String, ...] }`| None (HTTP Status Code) |
| 등록한 모든 폴더 조회       | GET         | /api/folders   | None                              | `List<FolderResponseDto>`|

### Product API

| 기능                         | HTTP Method | URL                             | Request                                                   | Response                |
|----------------------------|-------------|---------------------------------|-----------------------------------------------------------|-------------------------|
| 관심 상품 등록              | POST        | /api/products                   | `ProductRequestDto`                                       | `ProductResponseDto`    |
| 관심 상품 희망 최저가 등록  | PUT         | /api/products/{id}              | `ProductMypriceRequestDto`                                | `ProductResponseDto`    |
| 관심 상품 조회              | GET         | /api/products                   | `page, size, sortBy, isAsc`                               | `Page<ProductResponseDto>`|
| 상품에 폴더 추가            | POST        | /api/products/{productId}/folder| `productId, folderId`                                     | None (HTTP Status Code) |
| 폴더 내 관심상품 조회       | GET         | /api/folders/{folderId}/products| `folderId, page, size, sortBy, isAsc`                     | `Page<ProductResponseDto>`|

### User API

| 기능                         | HTTP Method | URL                             | Request                                                   | Response                |
|----------------------------|-------------|---------------------------------|-----------------------------------------------------------|-------------------------|
| 로그인 페이지 이동          | GET         | /api/user/login-page            | None                                                      | Renders login view      |
| 회원가입 페이지 이동        | GET         | /api/user/signup                | None                                                      | Renders signup view     |
| 회원가입                    | POST        | /api/user/signup                | `SignupRequestDto`                                        | Redirects to login page |
| 회원 정보 조회              | GET         | /api/user-info                  | None                                                      | `UserInfoDto`           |
| 사용자 폴더 조회            | GET         | /api/user-folder                | None                                                      | Renders user folders view|

### Home API

| 기능                         | HTTP Method | URL                             | Request                                                   | Response                |
|----------------------------|-------------|---------------------------------|-----------------------------------------------------------|-------------------------|
| 메인 페이지 이동            | GET         | /                               | None                                                      | Renders home view       |

