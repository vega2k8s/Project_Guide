# 미니 프로젝트 가이드

## 1. BackEnd 설계 가이드

### 1.1 도메인 설계서 가이드

**목적**: 비즈니스 도메인을 명확히 정의하고 핵심 개념들 간의 관계를 파악

**작성 항목**:
- **도메인 개요**: 프로젝트의 비즈니스 영역 정의
- **핵심 도메인 객체**: 주요 비즈니스 엔티티 나열 (예: 사용자, 상품, 주문 등)
- **도메인 관계도**: 도메인 객체들 간의 관계 시각화
- **비즈니스 규칙**: 각 도메인에서 지켜야 할 규칙들
- **용어 정의**: 프로젝트에서 사용하는 주요 용어 사전

**작성 팁**:
- 실제 비즈니스 관점에서 접근
- 기술적 구현보다는 업무 로직에 집중
- 팀원 모두가 이해할 수 있는 명확한 용어 사용

### 1.2 Entity 설계서 가이드

**목적**: JPA Entity 클래스 설계를 통한 객체 관계 정의

**작성 항목**:
- **Entity 목록**: 모든 Entity 클래스 나열
- **Entity 속성**: 각 Entity의 필드와 데이터 타입
- **연관관계 매핑**: @OneToMany, @ManyToOne 등의 관계 정의
- **제약조건**: @NotNull, @Size 등의 검증 규칙
- **인덱스 전략**: 성능을 위한 인덱스 설계

**Entity 설계 예시**:
```java
@Entity
@Table(name = "users")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @Column(nullable = false, unique = true)
    private String username;
    
    @OneToMany(mappedBy = "user", cascade = CascadeType.ALL)
    private List<Order> orders = new ArrayList<>();
}
```

### 1.3 Table 설계서 가이드

**목적**: 데이터베이스 물리적 구조 설계

**작성 항목**:
- **테이블 목록**: 모든 테이블과 설명
- **컬럼 정의**: 컬럼명, 데이터타입, 길이, NULL 허용여부, 기본값
- **Primary Key**: 기본키 설정
- **Foreign Key**: 외래키 관계 정의
- **인덱스**: 성능 최적화를 위한 인덱스
- **샘플 데이터**: 테스트용 초기 데이터

**테이블 설계 템플릿**:
```
테이블명: users
설명: 사용자 정보 관리

| 컬럼명      | 데이터타입   | 길이 | NULL |    기본값          |   설명     |
|------------|------------|------|------|-------------------|-----------|
| id         | BIGINT     |  -   |  N   |  AUTO_INCREMENT   | 사용자 ID  |
| username   | VARCHAR    |  50  |  N   |     -             | 사용자명   |
| email      | VARCHAR    | 100  |  N   |     -             | 이메일     |
| created_at | TIMESTAMP  |  -   |  N   | CURRENT_TIMESTAMP | 생성일시   |
```

### 1.4 REST API 설계서 가이드

**목적**: 클라이언트와 서버 간 통신 규격 정의

**작성 항목**:
- **API 개요**: 전체 API 구조와 인증 방식
- **Base URL**: API의 기본 경로
- **HTTP 메서드별 엔드포인트**: GET, POST, PUT, DELETE
- **요청/응답 스펙**: Request Body, Response Body, HTTP Status Code
- **에러 응답**: 각종 에러 상황별 응답

**API 설계 예시**:
```
POST /api/users
Content-Type: application/json

Request Body:
{
    "username": "testuser",
    "email": "test@example.com",
    "password": "password123"
}

Response (201 Created):
{
    "id": 1,
    "username": "testuser",
    "email": "test@example.com",
    "createdAt": "2025-05-22T10:30:00"
}

Response (400 Bad Request):
{
    "error": "VALIDATION_ERROR",
    "message": "이메일 형식이 올바르지 않습니다",
    "field": "email"
}
```

### 1.5 에러 코드 관리 가이드

**목적**: 일관된 에러 처리 및 클라이언트 대응 방안 제공

**작성 항목**:
- **에러 코드 체계**: 에러 코드 명명 규칙
- **HTTP 상태 코드**: 상황별 적절한 HTTP 상태 코드
- **에러 메시지**: 사용자 친화적인 에러 메시지
- **로깅 전략**: 서버 로그 기록 방식

**에러 코드 예시**:
```java
public enum ErrorCode {
    // 인증/인가 관련 (40X)
    INVALID_CREDENTIALS("AUTH_001", "아이디 또는 비밀번호가 올바르지 않습니다", HttpStatus.UNAUTHORIZED),
    ACCESS_DENIED("AUTH_002", "접근 권한이 없습니다", HttpStatus.FORBIDDEN),
    
    // 데이터 검증 관련 (40X)
    VALIDATION_ERROR("VALID_001", "입력값이 올바르지 않습니다", HttpStatus.BAD_REQUEST),
    DUPLICATE_USERNAME("VALID_002", "이미 존재하는 사용자명입니다", HttpStatus.CONFLICT),
    
    // 서버 오류 (50X)
    INTERNAL_SERVER_ERROR("SERVER_001", "서버 내부 오류가 발생했습니다", HttpStatus.INTERNAL_SERVER_ERROR);
}
```

## 2. FrontEnd 설계 가이드

### 2.1 화면 설계서 가이드

**주요 화면 설계 도구**:
- **Figma**: 가장 인기 있는 UI/UX 설계 도구, 협업 기능 우수
- **Balsamiq**: 와이어프레임 전용, 빠른 프로토타이핑
- **Adobe XD**: Adobe 제품군과 연동성 좋음
- **Sketch**: Mac 전용, 디자이너들이 선호
- **draw.io**: 무료, 간단한 와이어프레임 제작

**추천**: **Figma** (무료, 웹 기반, 실시간 협업, 개발자 친화적)

**화면 설계 작성 항목**:
- **사이트맵**: 전체 페이지 구조도
- **와이어프레임**: 각 페이지의 레이아웃 스케치
- **UI 플로우**: 사용자 동선과 상호작용 흐름
- **컴포넌트 가이드**: 재사용 가능한 UI 컴포넌트들
- **반응형 디자인**: 모바일/태블릿/데스크톱 대응

### 2.2 React 컴포넌트 설계 가이드

**가장 인기 있는 React UI 라이브러리**:
1. **Material-UI (MUI)**: Google Material Design 기반, 가장 인기
2. **Chakra UI**: 간단하고 모듈형 설계
3. **React Bootstrap**: Bootstrap 기반의 친숙한 디자인
2. **Ant Design**: 엔터프라이즈급 애플리케이션에 적합
5. **Mantine**: 현대적이고 기능이 풍부

**추천**: **Material-UI (MUI)** - 학습 자료가 풍부하고 기업에서 많이 사용

**컴포넌트 설계 원칙**:
- **단일 책임 원칙**: 하나의 컴포넌트는 하나의 역할만
- **재사용성**: 여러 곳에서 사용할 수 있도록 설계
- **Props 타입 정의**: PropTypes 또는 TypeScript 활용
- **상태 관리**: 로컬 state vs 전역 state 구분

**컴포넌트 구조 예시**:
```
src/
├── components/
│   ├── common/          # 공통 컴포넌트
│   │   ├── Button/
│   │   ├── Input/
│   │   └── Modal/
│   ├── layout/          # 레이아웃 컴포넌트
│   │   ├── Header/
│   │   ├── Footer/
│   │   └── Sidebar/
│   └── pages/           # 페이지별 컴포넌트
│       ├── Home/
│       ├── Login/
│       └── Dashboard/
```

### 2.3 Thymeleaf 화면 설계 가이드

**Thymeleaf 설계 원칙**:
- **템플릿 레이아웃**: 공통 레이아웃 활용
- **프래그먼트**: 재사용 가능한 화면 조각
- **Spring Security 연동**: 인증/인가 처리
- **폼 검증**: 서버사이드 검증과 연동

**템플릿 구조 예시**:
```
templates/
├── layout/
│   ├── base.html        # 기본 레이아웃
│   └── admin.html       # 관리자 레이아웃
├── fragments/
│   ├── header.html      # 헤더 프래그먼트
│   ├── nav.html         # 네비게이션
│   └── footer.html      # 푸터 프래그먼트
├── admin/
│   ├── dashboard.html   # 관리자 대시보드
│   ├── users.html       # 사용자 관리
│   └── products.html    # 상품 관리
└── error/
    ├── 404.html         # 404 에러 페이지
    └── 500.html         # 500 에러 페이지
```

## 3. 프로젝트 작성 순서 및 9일 타임테이블

### Day 1-2: 기획 및 설계 (2일)
**Day 1**:
- 팀 구성 및 역할 분담
- 프로젝트 주제 선정 및 요구사항 정의
- 도메인 설계서 작성
- 화면 설계서 초안 작성 (와이어프레임)

**Day 2**:
- Entity 설계서 작성
- Table 설계서 작성
- REST API 설계서 작성
- React 컴포넌트 구조 설계
- 개발 환경 구축

### Day 3-4: BackEnd 기본 구현 (2일)
**Day 3**:
- Spring Boot 프로젝트 초기 설정
- Entity 클래스 구현
- Repository 구현
- 데이터베이스 초기화 및 테스트 데이터 생성

**Day 4**:
- Service 클래스 구현
- DTO 클래스 구현
- REST API Controller 기본 CRUD 구현
- API 테스트 (Postman 등)

### Day 5-6: FrontEnd 기본 구현 (2일)
**Day 5**:
- React 프로젝트 초기 설정 (Vite)
- UI 라이브러리 설정 (MUI 등)
- 기본 레이아웃 컴포넌트 구현
- 라우팅 구조 설정

**Day 6**:
- 주요 페이지 컴포넌트 구현
- API 연동 (Axios)
- 기본 CRUD 기능 구현
- Thymeleaf 관리자 페이지 기본 구현

### Day 7: 통합 및 고급 기능 (1일)
- FrontEnd ↔ BackEnd 통합 테스트
- Spring Security 인증/인가 구현
- JWT 토큰 기반 인증 구현
- 에러 처리 및 예외 상황 대응

### Day 8: 추가 기능 및 최적화 (1일)
- 추가 비즈니스 로직 구현
- 성능 최적화
- 코드 리팩토링
- 단위 테스트 작성 (선택)

### Day 9: 최종 점검 및 발표 준비 (1일)
- 전체 기능 테스트
- 문서 정리 
- 발표 자료 준비
- 데모 시연 준비

## 4. 프로젝트 평가 및 배점표

### 평가 기준 (총 100점)

#### 4.1 기본 구현 영역 (70점)
**BackEnd 구현 (35점)**:
- Entity 및 Repository 구현 (10점)
  - JPA 연관관계 매핑의 정확성
  - 적절한 제약조건 설정
- Service 및 비즈니스 로직 (10점)
  - 트랜잭션 처리
  - 예외 처리
- REST API 구현 (10점)
  - HTTP 메서드 적절한 사용
  - 일관된 응답 형식
- Spring Security 구현 (5점)
  - 인증/인가 처리
  - JWT 또는 Form 인증

**FrontEnd 구현 (35점)**:
- React 컴포넌트 구조 (10점)
  - 컴포넌트 재사용성
  - Props와 State 관리
- UI/UX 구현 (10점)
  - 사용자 친화적 인터페이스
  - 반응형 디자인
- API 연동 (10점)
  - 적절한 HTTP 통신
  - 에러 처리
- Thymeleaf 관리자 페이지 (5점)
  - 서버사이드 렌더링
  - 폼 처리

#### 4.2 추가 구현 영역 (15점)
**고급 기능 구현**:
- JPA 성능 튜닝 : N+1 문제해결 (5점)
- 상태 관리 라이브러리 활용 (Redux) (5점)
- 페이징 및 검색 기능 (3점)
- 파일 업로드/다운로드 (2점)

#### 4.3 설계 및 문서화 (15점)
- 도메인 및 Entity 설계서 (5점)
- API 설계서 (5점)
- 화면 설계서 (3점)
- 프로젝트 문서화 및 README (2점)

### 평가 방식
1. **개별 평가 (70%)**: 개인별 기여도 및 이해도 평가
2. **팀 평가 (30%)**: 프로젝트 완성도 및 팀워크 평가

### 제출물
1. **소스 코드**: GitHub Repository
2. **설계 문서**: 모든 설계서 (PDF / word /google docs/ Notion 양식가능)
3. **실행 가능한 애플리케이션**: 데모 준비
4. **발표 자료**: 10분 내외 프레젠테이션
5. **개인 회고록**: 학습 내용 정리 및 소감

### 평가 시 주의사항
- **기본기 중시**: 화려한 기능보다는 배운 내용의 정확한 구현
- **팀워크**: 모든 팀원의 균등한 참여 권장
- **문서화**: 코드만큼 중요한 문서 작성