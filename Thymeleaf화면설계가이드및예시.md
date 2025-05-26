# Thymeleaf 화면 설계 및 레이아웃 가이드

## 1. Thymeleaf 화면 설계 철학

### 1.1 자연스러운 템플릿 (Natural Templates)
Thymeleaf의 핵심 철학은 "자연스러운 템플릿"입니다. 이는 템플릿 파일이 브라우저에서 직접 열어도 정상적인 HTML로 표시되어야 한다는 의미입니다.

**설계 원칙:**
- HTML 문법을 최대한 유지하면서 동적 기능 추가
- 디자이너와 개발자 간의 협업 용이성
- 프로토타입과 실제 구현 간의 간격 최소화
- SEO 친화적인 서버사이드 렌더링

### 1.2 컴포넌트 기반 설계 접근법
관리자 페이지에서는 재사용 가능한 컴포넌트 단위로 화면을 설계하는 것이 중요합니다.

**주요 컴포넌트 계층:**
- **레이아웃 계층**: 전체 페이지 구조 (헤더, 사이드바, 푸터)
- **섹션 계층**: 페이지별 주요 영역 (검색폼, 테이블, 폼)
- **프래그먼트 계층**: 재사용 가능한 작은 단위 (버튼, 모달, 알림)

## 2. 레이아웃 설계 구조

### 2.1 계층적 레이아웃 시스템

**1단계: Base Layout (기본 골격)**
```
┌─────────────────────────────────────┐
│              Header                 │
├─────────────────────────────────────┤
│ Sidebar │      Main Content         │
│         │                           │
│         │    ┌─────────────────┐    │
│         │    │   Page Content  │    │
│         │    └─────────────────┘    │
├─────────────────────────────────────┤
│              Footer                 │
└─────────────────────────────────────┘
```

**2단계: Page Layout (페이지별 구조)**
```
Main Content Area:
┌─────────────────────────────────────┐
│          Breadcrumb                 │
├─────────────────────────────────────┤
│    Page Header + Action Buttons     │
├─────────────────────────────────────┤
│         Alert Messages              │
├─────────────────────────────────────┤
│          Search/Filter              │
├─────────────────────────────────────┤
│         Content Area                │
│    (Table/Form/Dashboard)           │
├─────────────────────────────────────┤
│         Pagination                  │
└─────────────────────────────────────┘
```

### 2.2 반응형 레이아웃 전략

**데스크톱 (1200px+)**
- 3컬럼 레이아웃: 사이드바 + 메인 + 우측 정보패널
- 풀 테이블 표시
- 모든 액션 버튼 표시

**태블릿 (768px ~ 1199px)**
- 2컬럼 레이아웃: 축소된 사이드바 + 메인
- 테이블 스크롤 또는 카드 형태로 변환
- 중요한 액션 버튼만 표시

**모바일 (767px 이하)**
- 1컬럼 레이아웃: 햄버거 메뉴 + 메인
- 카드 형태의 리스트 뷰
- 드롭다운 액션 메뉴

## 3. 화면 유형별 설계 가이드

### 3.1 목록 페이지 (List View) 설계

**정보 아키텍처:**
```
1. 페이지 헤더
   - 제목 + 아이콘
   - 주요 액션 버튼 (생성, 내보내기)
   - 요약 통계 정보

2. 검색/필터 영역
   - 접이식 또는 항상 표시
   - 명확한 라벨과 플레이스홀더
   - 초기화 버튼

3. 결과 영역
   - 결과 수 표시
   - 정렬 옵션
   - 페이지 크기 선택

4. 데이터 테이블
   - 정렬 가능한 컬럼 헤더
   - 행별 액션 버튼
   - 체크박스 (대량 작업용)
   - 상태 표시 (배지, 아이콘)

5. 페이지네이션
   - 현재 페이지 강조
   - 이전/다음 버튼
   - 페이지 점프 기능
```

**UX 고려사항:**
- **스켈레톤 로딩**: 데이터 로딩 중 레이아웃 유지
- **무한 스크롤 vs 페이지네이션**: 데이터 양에 따른 선택
- **빈 상태 디자인**: 검색 결과가 없을 때의 안내
- **에러 상태**: 로딩 실패 시 복구 방법 제시

### 3.2 상세 페이지 (Detail View) 설계

**레이아웃 패턴:**
```
1. 헤더 영역
   - 제목 (주요 식별자)
   - 상태 배지
   - 액션 버튼 그룹

2. 메타 정보
   - 생성/수정 일시
   - 작성자 정보
   - 기타 시스템 정보

3. 주요 정보 섹션
   - 카드 형태의 그룹핑
   - 명확한 라벨-값 구조
   - 편집 가능 필드 표시

4. 관련 정보 탭
   - 연관 데이터
   - 활동 로그
   - 첨부 파일
```

**정보 표시 전략:**
- **중요도 기반 배치**: 가장 중요한 정보를 상단에
- **시각적 계층구조**: 제목, 소제목, 본문의 명확한 구분
- **데이터 그룹핑**: 관련 있는 정보끼리 묶어서 표시
- **액션의 접근성**: 자주 사용되는 기능을 쉽게 찾을 수 있도록

### 3.3 폼 페이지 (Form View) 설계

**폼 레이아웃 구조:**
```
1. 폼 헤더
   - 폼 제목과 목적 설명
   - 필수 필드 안내
   - 진행 상황 (다단계 폼의 경우)

2. 폼 섹션
   - 논리적 그룹별로 구분
   - 접이식 섹션 (복잡한 폼)
   - 섹션별 제목과 설명

3. 입력 필드
   - 명확한 라벨
   - 도움말 텍스트
   - 실시간 유효성 검사
   - 에러 메시지

4. 액션 영역
   - 주요 액션 (저장, 제출)
   - 보조 액션 (취소, 임시저장)
   - 위험한 액션 (삭제)
```

**폼 UX 모범 사례:**
- **필드 순서**: 논리적이고 직관적인 흐름
- **입력 도움**: 플레이스홀더, 예시, 툴팁 활용
- **에러 처리**: 인라인 에러와 요약 에러의 조합
- **진행 표시**: 긴 폼에서 현재 위치와 완료도 표시

### 3.4 대시보드 설계

**대시보드 구성 요소:**
```
1. 요약 카드 (KPI Cards)
   - 핵심 지표의 시각적 표현
   - 전기간 대비 변화량
   - 드릴다운 링크

2. 차트 영역
   - 시계열 차트
   - 비교 차트
   - 분포 차트

3. 테이블 위젯
   - 최신 활동
   - 상위/하위 항목
   - 알림 목록

4. 액션 위젯
   - 빠른 액션 버튼
   - 바로가기 링크
   - 북마크된 페이지
```

**대시보드 설계 원칙:**
- **5초 룰**: 핵심 정보를 5초 내에 파악 가능해야 함
- **계층적 정보**: 요약 → 상세 → 액션의 흐름
- **일관된 색상**: 상태와 카테고리별 색상 체계
- **적응형 레이아웃**: 화면 크기에 따른 자동 조정

## 4. 공통 UI 컴포넌트 설계

### 4.1 네비게이션 설계

**메인 네비게이션 구조:**
```
1. 글로벌 헤더
   - 로고/브랜드
   - 사용자 메뉴
   - 알림 센터
   - 검색 박스

2. 사이드 네비게이션
   - 계층적 메뉴 구조
   - 현재 위치 표시
   - 접기/펼치기 기능
   - 즐겨찾기 기능

3. 브레드크럼
   - 현재 위치 경로
   - 클릭 가능한 단계
   - 홈으로 돌아가기
```

**네비게이션 UX 가이드라인:**
- **명확한 현재 위치**: 사용자가 어디에 있는지 항상 알 수 있어야 함
- **일관된 구조**: 모든 페이지에서 동일한 네비게이션 패턴
- **접근성**: 키보드 네비게이션과 스크린 리더 지원
- **성능**: 메뉴 로딩 지연 최소화

### 4.2 데이터 테이블 설계

**테이블 구성 요소:**
```
1. 테이블 헤더
   - 정렬 가능 표시 (화살표)
   - 필터 아이콘
   - 컬럼 크기 조정
   - 체크박스 (전체 선택)

2. 테이블 바디
   - 데이터 행
   - 상태 표시 (색상, 아이콘)
   - 인라인 편집 (선택적)
   - 액션 버튼

3. 테이블 푸터
   - 페이지네이션
   - 결과 수 표시
   - 페이지 크기 선택
```

**테이블 반응형 전략:**
- **우선순위 기반 표시**: 중요한 컬럼만 모바일에서 표시
- **카드 변환**: 작은 화면에서 테이블을 카드 형태로 변환
- **스크롤 처리**: 수평 스크롤과 고정 컬럼 활용
- **액션 축약**: 드롭다운 메뉴로 액션 버튼 정리

### 4.3 모달 및 팝업 설계

**모달 사용 시나리오:**
```
1. 확인 모달
   - 삭제, 변경 등 중요한 액션 확인
   - 명확한 제목과 설명
   - 취소/확인 버튼

2. 정보 모달
   - 상세 정보 표시
   - 빠른 미리보기
   - 외부 링크 방지

3. 폼 모달
   - 간단한 생성/편집 폼
   - 복잡하지 않은 입력
   - 실시간 검증

4. 멀티스텝 모달
   - 위자드 형태의 프로세스
   - 진행 상황 표시
   - 이전/다음 네비게이션
```

**모달 UX 모범 사례:**
- **명확한 목적**: 모달을 여는 이유가 명확해야 함
- **쉬운 닫기**: ESC 키, 배경 클릭, X 버튼 제공
- **적절한 크기**: 내용에 맞는 크기 조정
- **접근성**: 포커스 관리와 키보드 네비게이션

## 5. 상태 및 피드백 디자인

### 5.1 로딩 상태 디자인

**로딩 표시 전략:**
```
1. 글로벌 로딩
   - 전체 페이지 로딩
   - 스피너 + 로딩 메시지
   - 진행률 표시 (가능한 경우)

2. 섹션 로딩
   - 특정 영역만 로딩
   - 스켈레톤 UI
   - 컨텐츠 영역 블러 처리

3. 인라인 로딩
   - 버튼 내 스피너
   - 테이블 행 업데이트
   - 실시간 검색 결과
```

**로딩 UX 원칙:**
- **즉시 피드백**: 액션 후 즉시 로딩 상태 표시
- **예상 시간**: 가능하면 완료 예상 시간 제공
- **취소 옵션**: 긴 작업의 경우 취소 버튼 제공
- **컨텍스트 유지**: 로딩 중에도 페이지 구조 유지

### 5.2 에러 상태 디자인

**에러 표시 레벨:**
```
1. 페이지 레벨 에러
   - 404, 500 등 시스템 에러
   - 전체 페이지 대체
   - 복구 방법 안내

2. 섹션 레벨 에러
   - 데이터 로딩 실패
   - 재시도 버튼
   - 대안 제시

3. 필드 레벨 에러
   - 폼 입력 검증 에러
   - 인라인 에러 메시지
   - 수정 방법 안내
```

### 5.3 성공 및 알림 메시지

**알림 메시지 유형:**
```
1. 성공 메시지
   - 작업 완료 확인
   - 초록색 계열
   - 자동 사라짐

2. 경고 메시지
   - 주의 필요한 상황
   - 노란색 계열
   - 사용자 액션 유도

3. 정보 메시지
   - 일반적인 안내
   - 파란색 계열
   - 중요도에 따라 지속 시간 조정

4. 에러 메시지
   - 오류 발생 알림
   - 빨간색 계열
   - 수동 닫기
```

## 6. 접근성 및 사용성 가이드

### 6.1 웹 접근성 (WCAG) 준수

**핵심 접근성 원칙:**
```
1. 인식 가능성 (Perceivable)
   - 충분한 색상 대비 (4.5:1 이상)
   - 대체 텍스트 제공
   - 확대 가능한 폰트 크기

2. 운용 가능성 (Operable)
   - 키보드로만 조작 가능
   - 충분한 클릭 영역 (44px 이상)
   - 시간 제한 없음 또는 연장 가능

3. 이해 가능성 (Understandable)
   - 명확한 언어 사용
   - 일관된 네비게이션
   - 에러 메시지의 명확성

4. 견고성 (Robust)
   - 표준 HTML 마크업
   - 스크린 리더 호환성
   - 다양한 브라우저 지원
```

### 6.2 국제화 (i18n) 고려사항

**다국어 대응 설계:**
```
1. 텍스트 확장성
   - 20-30% 텍스트 길이 증가 고려
   - 유연한 레이아웃 설계
   - 폰트 크기 조정 가능

2. 문화적 고려사항
   - 색상의 문화적 의미
   - 읽기 방향 (좌→우, 우→좌)
   - 날짜/시간 형식

3. 기술적 구현
   - 메시지 키 기반 텍스트 관리
   - 동적 로케일 변경
   - 폰트 로딩 최적화
```

## 7. 성능 최적화 전략

### 7.1 렌더링 성능

**서버사이드 렌더링 최적화:**
```
1. 템플릿 캐싱
   - 컴파일된 템플릿 재사용
   - 조건부 캐싱 전략
   - 캐시 무효화 정책

2. 데이터 최적화
   - 필요한 데이터만 로드
   - 지연 로딩 전략
   - 페이지네이션 활용

3. HTML 최적화
   - 불필요한 마크업 제거
   - 인라인 스타일 최소화
   - 압축 및 최소화
```

### 7.2 클라이언트 성능

**프론트엔드 최적화:**
```
1. 리소스 로딩
   - CSS/JS 번들링
   - 이미지 최적화
   - 폰트 최적화

2. 인터랙션 성능
   - 디바운싱/스로틀링
   - 가상 스크롤링
   - 지연 로딩

3. 네트워크 최적화
   - AJAX 요청 최소화
   - 데이터 압축
   - CDN 활용
```

## 8. 테스팅 전략

### 8.1 UI/UX 테스팅

**사용성 테스팅 체크리스트:**
```
1. 네비게이션 테스트
   - 메뉴 찾기 용이성
   - 현재 위치 파악
   - 되돌아가기 기능

2. 폼 사용성 테스트
   - 필드 라벨 명확성
   - 에러 메시지 이해도
   - 자동완성 기능

3. 반응형 테스트
   - 다양한 화면 크기
   - 터치 인터페이스
   - 성능 영향도

4. 접근성 테스트
   - 키보드 네비게이션
   - 스크린 리더 호환
   - 색상 대비 검사
```

### 8.2 크로스 브라우저 테스팅

**테스트 매트릭스:**
```
데스크톱:
- Chrome (최신, 이전 버전)
- Firefox (최신, 이전 버전)
- Safari (최신)
- Edge (최신)

모바일:
- iOS Safari
- Android Chrome
- Samsung Internet

특별 고려사항:
- Internet Explorer 11 (필요시)
- 특정 기업 환경 브라우저
- 접근성 도구
```

## 9. 유지보수 및 확장성

### 9.1 컴포넌트 문서화

**문서화 체계:**
```
1. 컴포넌트 가이드
   - 사용 목적과 시나리오
   - 속성 및 옵션 설명
   - 사용 예시

2. 스타일 가이드
   - 색상 팔레트
   - 타이포그래피
   - 간격 시스템
   - 아이콘 사용법

3. 패턴 라이브러리
   - UI 패턴 모음
   - 인터랙션 가이드
   - 애니메이션 가이드
```

### 9.2 확장성 고려사항

**미래 대응 설계:**
```
1. 모듈러 구조
   - 독립적인 컴포넌트 설계
   - 의존성 최소화
   - 재사용 가능한 패턴

2. 테마 시스템
   - CSS 변수 활용
   - 다크 모드 지원
   - 브랜드 커스터마이징

3. 설정 가능한 UI
   - 사용자 맞춤 레이아웃
   - 기능 토글
   - 개인화 옵션
```

# Thymeleaf 관리자 페이지 개발 가이드

## 1. 프로젝트 구조

```
src/
├── main/
│   ├── java/
│   │   └── com/example/admin/
│   │       ├── config/          # 설정 클래스
│   │       ├── entity/          # JPA 엔티티
│   │       ├── repository/      # JPA Repository
│   │       ├── service/         # 비즈니스 로직
│   │       ├── controller/      # MVC Controller
│   │       ├── dto/            # Data Transfer Object
│   │       └── AdminApplication.java
│   └── resources/
│       ├── templates/          # Thymeleaf 템플릿
│       │   ├── layout/        # 공통 레이아웃
│       │   ├── admin/         # 관리자 페이지
│       │   └── fragments/     # 재사용 가능한 조각
│       ├── static/
│       │   ├── css/
│       │   ├── js/
│       │   └── images/
│       └── application.yml
```

## 2. Entity 설계

### 2.1 기본 Entity 예시 (User)

```java
@Entity
@Table(name = "users")
@Getter @Setter
@NoArgsConstructor
@AllArgsConstructor
@Builder
public class User extends BaseEntity {
    
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @Column(nullable = false, unique = true, length = 50)
    private String username;
    
    @Column(nullable = false, length = 100)
    private String password;
    
    @Column(nullable = false, length = 100)
    private String email;
    
    @Column(length = 20)
    private String phone;
    
    @Enumerated(EnumType.STRING)
    @Column(nullable = false)
    private UserRole role;
    
    @Enumerated(EnumType.STRING)
    @Column(nullable = false)
    private UserStatus status;
    
    @Column(name = "last_login_at")
    private LocalDateTime lastLoginAt;
}
```

### 2.2 공통 BaseEntity

```java
@MappedSuperclass
@EntityListeners(AuditingEntityListener.class)
@Getter @Setter
public abstract class BaseEntity {
    
    @CreatedDate
    @Column(name = "created_at", nullable = false, updatable = false)
    private LocalDateTime createdAt;
    
    @LastModifiedDate
    @Column(name = "updated_at")
    private LocalDateTime updatedAt;
    
    @Column(name = "created_by", length = 50)
    private String createdBy;
    
    @Column(name = "updated_by", length = 50)
    private String updatedBy;
}
```

## 3. Repository 설계

```java
@Repository
public interface UserRepository extends JpaRepository<User, Long> {
    
    // 기본 검색 메서드
    Optional<User> findByUsername(String username);
    Optional<User> findByEmail(String email);
    List<User> findByStatus(UserStatus status);
    
    // 페이징 및 정렬
    Page<User> findByUsernameContaining(String username, Pageable pageable);
    Page<User> findByRole(UserRole role, Pageable pageable);
    
    // 복합 조건 검색
    @Query("SELECT u FROM User u WHERE " +
           "(:username IS NULL OR u.username LIKE %:username%) AND " +
           "(:email IS NULL OR u.email LIKE %:email%) AND " +
           "(:role IS NULL OR u.role = :role) AND " +
           "(:status IS NULL OR u.status = :status)")
    Page<User> findBySearchCriteria(
        @Param("username") String username,
        @Param("email") String email,
        @Param("role") UserRole role,
        @Param("status") UserStatus status,
        Pageable pageable
    );
    
    // 통계용 쿼리
    @Query("SELECT COUNT(u) FROM User u WHERE u.createdAt >= :startDate")
    long countNewUsersAfter(@Param("startDate") LocalDateTime startDate);
}
```

## 4. DTO 설계

### 4.1 사용자 관련 DTO

```java
// 목록 조회용 DTO
@Getter @Setter
@Builder
@NoArgsConstructor
@AllArgsConstructor
public class UserListDto {
    private Long id;
    private String username;
    private String email;
    private String phone;
    private UserRole role;
    private UserStatus status;
    private LocalDateTime createdAt;
    private LocalDateTime lastLoginAt;
    
    public static UserListDto from(User user) {
        return UserListDto.builder()
                .id(user.getId())
                .username(user.getUsername())
                .email(user.getEmail())
                .phone(user.getPhone())
                .role(user.getRole())
                .status(user.getStatus())
                .createdAt(user.getCreatedAt())
                .lastLoginAt(user.getLastLoginAt())
                .build();
    }
}

// 상세 조회용 DTO
@Getter @Setter
@Builder
@NoArgsConstructor
@AllArgsConstructor
public class UserDetailDto {
    private Long id;
    private String username;
    private String email;
    private String phone;
    private UserRole role;
    private UserStatus status;
    private LocalDateTime createdAt;
    private LocalDateTime updatedAt;
    private LocalDateTime lastLoginAt;
    
    public static UserDetailDto from(User user) {
        return UserDetailDto.builder()
                .id(user.getId())
                .username(user.getUsername())
                .email(user.getEmail())
                .phone(user.getPhone())
                .role(user.getRole())
                .status(user.getStatus())
                .createdAt(user.getCreatedAt())
                .updatedAt(user.getUpdatedAt())
                .lastLoginAt(user.getLastLoginAt())
                .build();
    }
}

// 생성/수정용 DTO
@Getter @Setter
@NoArgsConstructor
@AllArgsConstructor
public class UserFormDto {
    
    @NotBlank(message = "사용자명은 필수입니다")
    @Size(min = 3, max = 50, message = "사용자명은 3-50자 사이여야 합니다")
    private String username;
    
    @NotBlank(message = "비밀번호는 필수입니다")
    @Size(min = 8, message = "비밀번호는 최소 8자 이상이어야 합니다")
    private String password;
    
    @NotBlank(message = "이메일은 필수입니다")
    @Email(message = "올바른 이메일 형식이 아닙니다")
    private String email;
    
    @Pattern(regexp = "^[0-9]{2,3}-[0-9]{3,4}-[0-9]{4}$", 
             message = "올바른 전화번호 형식이 아닙니다")
    private String phone;
    
    @NotNull(message = "역할은 필수입니다")
    private UserRole role;
    
    @NotNull(message = "상태는 필수입니다")
    private UserStatus status;
    
    public User toEntity() {
        return User.builder()
                .username(this.username)
                .password(this.password) // 실제로는 암호화 필요
                .email(this.email)
                .phone(this.phone)
                .role(this.role)
                .status(this.status)
                .build();
    }
}

// 검색용 DTO
@Getter @Setter
@NoArgsConstructor
@AllArgsConstructor
public class UserSearchDto {
    private String username;
    private String email;
    private UserRole role;
    private UserStatus status;
    private String sortBy = "createdAt";
    private String sortDir = "desc";
    private int page = 0;
    private int size = 10;
    
    public Pageable getPageable() {
        Sort sort = Sort.by(Sort.Direction.fromString(sortDir), sortBy);
        return PageRequest.of(page, size, sort);
    }
}
```

## 5. Service 설계

```java
@Service
@Transactional(readOnly = true)
@RequiredArgsConstructor
public class UserService {
    
    private final UserRepository userRepository;
    private final PasswordEncoder passwordEncoder;
    
    // 목록 조회 (페이징, 검색)
    public Page<UserListDto> getUsers(UserSearchDto searchDto) {
        Pageable pageable = searchDto.getPageable();
        Page<User> users = userRepository.findBySearchCriteria(
            searchDto.getUsername(),
            searchDto.getEmail(),
            searchDto.getRole(),
            searchDto.getStatus(),
            pageable
        );
        
        return users.map(UserListDto::from);
    }
    
    // 상세 조회
    public UserDetailDto getUser(Long id) {
        User user = userRepository.findById(id)
                .orElseThrow(() -> new EntityNotFoundException("사용자를 찾을 수 없습니다"));
        return UserDetailDto.from(user);
    }
    
    // 생성
    @Transactional
    public Long createUser(UserFormDto userFormDto) {
        // 중복 체크
        if (userRepository.findByUsername(userFormDto.getUsername()).isPresent()) {
            throw new DuplicateKeyException("이미 존재하는 사용자명입니다");
        }
        
        if (userRepository.findByEmail(userFormDto.getEmail()).isPresent()) {
            throw new DuplicateKeyException("이미 존재하는 이메일입니다");
        }
        
        // 비밀번호 암호화
        User user = userFormDto.toEntity();
        user.setPassword(passwordEncoder.encode(user.getPassword()));
        
        User savedUser = userRepository.save(user);
        return savedUser.getId();
    }
    
    // 수정
    @Transactional
    public void updateUser(Long id, UserFormDto userFormDto) {
        User user = userRepository.findById(id)
                .orElseThrow(() -> new EntityNotFoundException("사용자를 찾을 수 없습니다"));
        
        // 수정할 필드만 업데이트
        user.setEmail(userFormDto.getEmail());
        user.setPhone(userFormDto.getPhone());
        user.setRole(userFormDto.getRole());
        user.setStatus(userFormDto.getStatus());
        
        // 비밀번호가 변경된 경우에만 암호화하여 업데이트
        if (StringUtils.hasText(userFormDto.getPassword())) {
            user.setPassword(passwordEncoder.encode(userFormDto.getPassword()));
        }
    }
    
    // 삭제 (실제로는 상태 변경)
    @Transactional
    public void deleteUser(Long id) {
        User user = userRepository.findById(id)
                .orElseThrow(() -> new EntityNotFoundException("사용자를 찾을 수 없습니다"));
        user.setStatus(UserStatus.DELETED);
    }
    
    // 통계 정보
    public Map<String, Object> getUserStatistics() {
        Map<String, Object> stats = new HashMap<>();
        stats.put("totalUsers", userRepository.count());
        stats.put("activeUsers", userRepository.findByStatus(UserStatus.ACTIVE).size());
        stats.put("newUsersThisMonth", userRepository.countNewUsersAfter(
            LocalDateTime.now().withDayOfMonth(1).withHour(0).withMinute(0).withSecond(0)
        ));
        return stats;
    }
}
```

## 6. Controller 설계

```java
@Controller
@RequestMapping("/admin/users")
@RequiredArgsConstructor
public class UserController {
    
    private final UserService userService;
    
    // 사용자 목록 페이지
    @GetMapping
    public String userList(
            @ModelAttribute UserSearchDto searchDto,
            Model model) {
        
        Page<UserListDto> users = userService.getUsers(searchDto);
        
        model.addAttribute("users", users);
        model.addAttribute("searchDto", searchDto);
        model.addAttribute("roles", UserRole.values());
        model.addAttribute("statuses", UserStatus.values());
        
        return "admin/users/list";
    }
    
    // 사용자 상세 페이지
    @GetMapping("/{id}")
    public String userDetail(@PathVariable Long id, Model model) {
        UserDetailDto user = userService.getUser(id);
        model.addAttribute("user", user);
        return "admin/users/detail";
    }
    
    // 사용자 생성 폼 페이지
    @GetMapping("/new")
    public String userCreateForm(Model model) {
        model.addAttribute("userForm", new UserFormDto());
        model.addAttribute("roles", UserRole.values());
        model.addAttribute("statuses", UserStatus.values());
        return "admin/users/form";
    }
    
    // 사용자 생성 처리
    @PostMapping("/new")
    public String userCreate(
            @Valid @ModelAttribute("userForm") UserFormDto userForm,
            BindingResult bindingResult,
            Model model,
            RedirectAttributes redirectAttributes) {
        
        if (bindingResult.hasErrors()) {
            model.addAttribute("roles", UserRole.values());
            model.addAttribute("statuses", UserStatus.values());
            return "admin/users/form";
        }
        
        try {
            Long userId = userService.createUser(userForm);
            redirectAttributes.addFlashAttribute("message", "사용자가 성공적으로 생성되었습니다.");
            return "redirect:/admin/users/" + userId;
        } catch (DuplicateKeyException e) {
            bindingResult.reject("duplicate", e.getMessage());
            model.addAttribute("roles", UserRole.values());
            model.addAttribute("statuses", UserStatus.values());
            return "admin/users/form";
        }
    }
    
    // 사용자 수정 폼 페이지
    @GetMapping("/{id}/edit")
    public String userEditForm(@PathVariable Long id, Model model) {
        UserDetailDto user = userService.getUser(id);
        
        UserFormDto userForm = new UserFormDto();
        userForm.setUsername(user.getUsername());
        userForm.setEmail(user.getEmail());
        userForm.setPhone(user.getPhone());
        userForm.setRole(user.getRole());
        userForm.setStatus(user.getStatus());
        
        model.addAttribute("userForm", userForm);
        model.addAttribute("userId", id);
        model.addAttribute("roles", UserRole.values());
        model.addAttribute("statuses", UserStatus.values());
        
        return "admin/users/form";
    }
    
    // 사용자 수정 처리
    @PostMapping("/{id}/edit")
    public String userUpdate(
            @PathVariable Long id,
            @Valid @ModelAttribute("userForm") UserFormDto userForm,
            BindingResult bindingResult,
            Model model,
            RedirectAttributes redirectAttributes) {
        
        if (bindingResult.hasErrors()) {
            model.addAttribute("userId", id);
            model.addAttribute("roles", UserRole.values());
            model.addAttribute("statuses", UserStatus.values());
            return "admin/users/form";
        }
        
        try {
            userService.updateUser(id, userForm);
            redirectAttributes.addFlashAttribute("message", "사용자 정보가 성공적으로 수정되었습니다.");
            return "redirect:/admin/users/" + id;
        } catch (Exception e) {
            bindingResult.reject("error", "수정 중 오류가 발생했습니다: " + e.getMessage());
            model.addAttribute("userId", id);
            model.addAttribute("roles", UserRole.values());
            model.addAttribute("statuses", UserStatus.values());
            return "admin/users/form";
        }
    }
    
    // 사용자 삭제
    @DeleteMapping("/{id}")
    @ResponseBody
    public ResponseEntity<?> userDelete(@PathVariable Long id) {
        try {
            userService.deleteUser(id);
            return ResponseEntity.ok().body(Map.of("message", "사용자가 삭제되었습니다."));
        } catch (Exception e) {
            return ResponseEntity.badRequest().body(Map.of("error", e.getMessage()));
        }
    }
    
    // AJAX 검색
    @GetMapping("/search")
    @ResponseBody
    public Page<UserListDto> searchUsers(@ModelAttribute UserSearchDto searchDto) {
        return userService.getUsers(searchDto);
    }
}
```

## 7. Thymeleaf 템플릿 설계

### 7.1 공통 레이아웃 (layout/admin.html)

```html
<!DOCTYPE html>
<html lang="ko" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title th:text="${title} + ' - 관리자'">관리자</title>
    
    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <!-- Font Awesome -->
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <!-- Custom CSS -->
    <link th:href="@{/css/admin.css}" rel="stylesheet">
    
    <!-- 페이지별 추가 CSS -->
    <th:block layout:fragment="css"></th:block>
</head>
<body>
    <!-- 네비게이션 바 -->
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
        <div class="container-fluid">
            <a class="navbar-brand" th:href="@{/admin}">
                <i class="fas fa-cogs"></i> 관리자
            </a>
            
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
                <span class="navbar-toggler-icon"></span>
            </button>
            
            <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav me-auto">
                    <li class="nav-item">
                        <a class="nav-link" th:href="@{/admin}" th:classappend="${#request.requestURI == '/admin'} ? 'active'">
                            <i class="fas fa-home"></i> 대시보드
                        </a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" th:href="@{/admin/users}" th:classappend="${#strings.startsWith(#request.requestURI, '/admin/users')} ? 'active'">
                            <i class="fas fa-users"></i> 사용자 관리
                        </a>
                    </li>
                </ul>
                
                <ul class="navbar-nav">
                    <li class="nav-item dropdown">
                        <a class="nav-link dropdown-toggle" href="#" role="button" data-bs-toggle="dropdown">
                            <i class="fas fa-user"></i> 관리자
                        </a>
                        <ul class="dropdown-menu">
                            <li><a class="dropdown-item" th:href="@{/admin/profile}">프로필</a></li>
                            <li><hr class="dropdown-divider"></li>
                            <li><a class="dropdown-item" th:href="@{/logout}">로그아웃</a></li>
                        </ul>
                    </li>
                </ul>
            </div>
        </div>
    </nav>
    
    <!-- 메인 컨텐츠 -->
    <div class="container-fluid mt-4">
        <!-- 브레드크럼 -->
        <nav aria-label="breadcrumb" th:if="${breadcrumbs}">
            <ol class="breadcrumb">
                <li class="breadcrumb-item" th:each="crumb : ${breadcrumbs}" 
                    th:classappend="${crumbStat.last} ? 'active'">
                    <a th:if="${!crumbStat.last}" th:href="${crumb.url}" th:text="${crumb.name}"></a>
                    <span th:if="${crumbStat.last}" th:text="${crumb.name}"></span>
                </li>
            </ol>
        </nav>
        
        <!-- 알림 메시지 -->
        <div th:if="${message}" class="alert alert-success alert-dismissible fade show" role="alert">
            <i class="fas fa-check-circle"></i> <span th:text="${message}"></span>
            <button type="button" class="btn-close" data-bs-dismiss="alert"></button>
        </div>
        
        <div th:if="${error}" class="alert alert-danger alert-dismissible fade show" role="alert">
            <i class="fas fa-exclamation-circle"></i> <span th:text="${error}"></span>
            <button type="button" class="btn-close" data-bs-dismiss="alert"></button>
        </div>
        
        <!-- 페이지 컨텐츠 -->
        <div layout:fragment="content"></div>
    </div>
    
    <!-- Bootstrap JS -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    <!-- jQuery -->
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <!-- Custom JS -->
    <script th:src="@{/js/admin.js}"></script>
    
    <!-- 페이지별 추가 JS -->
    <th:block layout:fragment="script"></th:block>
</body>
</html>
```

### 7.2 사용자 목록 페이지 (admin/users/list.html)

```html
<!DOCTYPE html>
<html lang="ko" 
      xmlns:th="http://www.thymeleaf.org"
      xmlns:layout="http://www.ultraq.net.nz/thymeleaf/layout"
      layout:decorate="~{layout/admin}">

<th:block layout:fragment="css">
    <style>
        .search-form { background-color: #f8f9fa; padding: 20px; border-radius: 8px; margin-bottom: 20px; }
        .table-actions { white-space: nowrap; }
        .badge-role { font-size: 0.8em; }
        .pagination-wrapper { display: flex; justify-content: center; margin-top: 20px; }
    </style>
</th:block>

<div layout:fragment="content">
    <div class="d-flex justify-content-between align-items-center mb-4">
        <h2><i class="fas fa-users"></i> 사용자 관리</h2>
        <a th:href="@{/admin/users/new}" class="btn btn-primary">
            <i class="fas fa-plus"></i> 새 사용자 추가
        </a>
    </div>
    
    <!-- 검색 폼 -->
    <form th:action="@{/admin/users}" method="get" th:object="${searchDto}" class="search-form">
        <div class="row g-3">
            <div class="col-md-3">
                <label class="form-label">사용자명</label>
                <input type="text" class="form-control" th:field="*{username}" placeholder="사용자명 검색">
            </div>
            
            <div class="col-md-3">
                <label class="form-label">이메일</label>
                <input type="email" class="form-control" th:field="*{email}" placeholder="이메일 검색">
            </div>
            
            <div class="col-md-2">
                <label class="form-label">역할</label>
                <select class="form-select" th:field="*{role}">
                    <option value="">전체</option>
                    <option th:each="role : ${roles}" th:value="${role}" th:text="${role.displayName}"></option>
                </select>
            </div>
            
            <div class="col-md-2">
                <label class="form-label">상태</label>
                <select class="form-select" th:field="*{status}">
                    <option value="">전체</option>
                    <option th:each="status : ${statuses}" th:value="${status}" th:text="${status.displayName}"></option>
                </select>
            </div>
            
            <div class="col-md-2 d-flex align-items-end">
                <button type="submit" class="btn btn-outline-primary me-2">
                    <i class="fas fa-search"></i> 검색
                </button>
                <a th:href="@{/admin/users}" class="btn btn-outline-secondary">
                    <i class="fas fa-redo"></i> 초기화
                </a>
            </div>
        </div>
        
        <!-- 숨겨진 정렬 필드 -->
        <input type="hidden" th:field="*{sortBy}">
        <input type="hidden" th:field="*{sortDir}">
        <input type="hidden" th:field="*{page}">
        <input type="hidden" th:field="*{size}">
    </form>
    
    <!-- 결과 통계 -->
    <div class="d-flex justify-content-between align-items-center mb-3">
        <span class="text-muted">
            총 <strong th:text="${users.totalElements}">0</strong>명의 사용자 
            (<strong th:text="${users.number + 1}">1</strong> / <strong th:text="${users.totalPages}">1</strong> 페이지)
        </span>
        
        <div>
            <label class="form-label me-2">페이지 크기:</label>
            <select class="form-select form-select-sm d-inline-block" style="width: auto;" 
                    onchange="changePageSize(this.value)">
                <option th:each="size : ${T(java.util.Arrays).asList(10, 20, 50, 100)}" 
                        th:value="${size}" 
                        th:text="${size}"
                        th:selected="${size == searchDto.size}"></option>
            </select>
        </div>
    </div>
    
    <!-- 사용자 목록 테이블 -->
    <div class="card">
        <div class="table-responsive">
            <table class="table table-hover mb-0">
                <thead class="table-dark">
                    <tr>
                        <th>
                            <a th:href="@{/admin/users(${searchDto.getUrlParams()}, sortBy='username', sortDir=${searchDto.sortBy == 'username' and searchDto.sortDir == 'asc' ? 'desc' : 'asc'})}"
                               class="text-white text-decoration-none">
                                사용자명
                                <i th:if="${searchDto.sortBy == 'username'}" 
                                   th:class="${searchDto.sortDir == 'asc' ? 'fas fa-sort-up' : 'fas fa-sort-down'}"></i>
                                <i th:unless="${searchDto.sortBy == 'username'}" class="fas fa-sort"></i>
                            </a>
                        </th>
                        <th>
                            <a th:href="@{/admin/users(${searchDto.getUrlParams()}, sortBy='email', sortDir=${searchDto.sortBy == 'email' and searchDto.sortDir == 'asc' ? 'desc' : 'asc'})}"
                               class="text-white text-decoration-none">
                                이메일
                                <i th:if="${searchDto.sortBy == 'email'}" 
                                   th:class="${searchDto.sortDir == 'asc' ? 'fas fa-sort-up' : 'fas fa-sort-down'}"></i>
                                <i th:unless="${searchDto.sortBy == 'email'}" class="fas fa-sort"></i>
                            </a>
                        </th>
                        <th>전화번호</th>
                        <th>역할</th>
                        <th>상태</th>
                        <th>
                            <a th:href="@{/admin/users(${searchDto.getUrlParams()}, sortBy='createdAt', sortDir=${searchDto.sortBy == 'createdAt' and searchDto.sortDir == 'asc' ? 'desc' : 'asc'})}"
                               class="text-white text-decoration-none">
                                가입일
                                <i th:if="${searchDto.sortBy == 'createdAt'}" 
                                   th:class="${searchDto.sortDir == 'asc' ? 'fas fa-sort-up' : 'fas fa-sort-down'}"></i>
                                <i th:unless="${searchDto.sortBy == 'createdAt'}" class="fas fa-sort"></i>
                            </a>
                        </th>
                        <th>마지막 로그인</th>
                        <th>액션</th>
                    </tr>
                </thead>
                <tbody>
                    <tr th:each="user : ${users.content}">
                        <td>
                            <a th:href="@{/admin/users/{id}(id=${user.id})}" 
                               class="text-decoration-none fw-bold">
                                <span th:text="${user.username}"></span>
                            </a>
                        </td>
                        <td th:text="${user.email}"></td>
                        <td th:text="${user.phone ?: '-'}"></td>
                        <td>
                            <span class="badge badge-role" 
                                  th:classappend="${user.role.name() == 'ADMIN' ? 'bg-danger' : 'bg-info'}"
                                  th:text="${user.role.displayName}"></span>
                        </td>
                        <td>
                            <span class="badge" 
                                  th:classappend="${user.status.name() == 'ACTIVE' ? 'bg-success' : 'bg-secondary'}"
                                  th:text="${user.status.displayName}"></span>
                        </td>
                        <td th:text="${#temporals.format(user.createdAt, 'yyyy-MM-dd')}"></td>
                        <td th:text="${user.lastLoginAt != null ? #temporals.format(user.lastLoginAt, 'yyyy-MM-dd HH:mm') : '-'}"></td>
                        <td class="table-actions">
                            <div class="btn-group btn-group-sm">
                                <a th:href="@{/admin/users/{id}(id=${user.id})}" 
                                   class="btn btn-outline-info" title="상세보기">
                                    <i class="fas fa-eye"></i>
                                </a>
                                <a th:href="@{/admin/users/{id}/edit(id=${user.id})}" 
                                   class="btn btn-outline-warning" title="수정">
                                    <i class="fas fa-edit"></i>
                                </a>
                                <button type="button" class="btn btn-outline-danger" 
                                        title="삭제" onclick="deleteUser([[${user.id}]], '[[${user.username}]]')">
                                    <i class="fas fa-trash"></i>
                                </button>
                            </div>
                        </td>
                    </tr>
                    
                    <tr th:if="${users.content.empty}">
                        <td colspan="8" class="text-center text-muted py-4">
                            <i class="fas fa-search fa-2x mb-2"></i>
                            <div>검색 결과가 없습니다.</div>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
    
    <!-- 페이지네이션 -->
    <div class="pagination-wrapper" th:if="${users.totalPages > 1}">
        <nav>
            <ul class="pagination">
                <!-- 이전 페이지 -->
                <li class="page-item" th:classappend="${!users.hasPrevious()} ? 'disabled'">
                    <a class="page-link" 
                       th:href="${users.hasPrevious()} ? @{/admin/users(${searchDto.getUrlParams()}, page=${users.number - 1})} : '#'">
                        <i class="fas fa-chevron-left"></i>
                    </a>
                </li>
                
                <!-- 페이지 번호 -->
                <li class="page-item" 
                    th:each="pageNum : ${#numbers.sequence(T(java.lang.Math).max(0, users.number - 2), T(java.lang.Math).min(users.totalPages - 1, users.number + 2))}"
                    th:classappend="${pageNum == users.number} ? 'active'">
                    <a class="page-link" 
                       th:href="@{/admin/users(${searchDto.getUrlParams()}, page=${pageNum})}"
                       th:text="${pageNum + 1}"></a>
                </li>
                
                <!-- 다음 페이지 -->
                <li class="page-item" th:classappend="${!users.hasNext()} ? 'disabled'">
                    <a class="page-link" 
                       th:href="${users.hasNext()} ? @{/admin/users(${searchDto.getUrlParams()}, page=${users.number + 1})} : '#'">
                        <i class="fas fa-chevron-right"></i>
                    </a>
                </li>
            </ul>
        </nav>
    </div>
</div>

<th:block layout:fragment="script">
    <script>
        // 페이지 크기 변경
        function changePageSize(size) {
            const url = new URL(window.location);
            url.searchParams.set('size', size);
            url.searchParams.set('page', '0'); // 첫 페이지로 이동
            window.location.href = url.toString();
        }
        
        // 사용자 삭제
        function deleteUser(userId, username) {
            if (confirm(`정말로 '${username}' 사용자를 삭제하시겠습니까?`)) {
                fetch(`/admin/users/${userId}`, {
                    method: 'DELETE',
                    headers: {
                        'Content-Type': 'application/json',
                        'X-Requested-With': 'XMLHttpRequest'
                    }
                })
                .then(response => response.json())
                .then(data => {
                    if (data.message) {
                        alert(data.message);
                        location.reload();
                    } else if (data.error) {
                        alert('오류: ' + data.error);
                    }
                })
                .catch(error => {
                    console.error('Error:', error);
                    alert('삭제 중 오류가 발생했습니다.');
                });
            }
        }
    </script>
</th:block>
```

### 7.3 사용자 상세 페이지 (admin/users/detail.html)

```html
<!DOCTYPE html>
<html lang="ko" 
      xmlns:th="http://www.thymeleaf.org"
      xmlns:layout="http://www.ultraq.net.nz/thymeleaf/layout"
      layout:decorate="~{layout/admin}">

<th:block layout:fragment="css">
    <style>
        .info-card { border: none; box-shadow: 0 0.125rem 0.25rem rgba(0, 0, 0, 0.075); }
        .info-label { font-weight: 600; color: #6c757d; margin-bottom: 0.25rem; }
        .info-value { font-size: 1.1rem; margin-bottom: 1rem; }
        .status-badge { font-size: 1rem; padding: 0.5rem 1rem; }
    </style>
</th:block>

<div layout:fragment="content">
    <div class="d-flex justify-content-between align-items-center mb-4">
        <div>
            <h2><i class="fas fa-user"></i> 사용자 상세 정보</h2>
            <nav aria-label="breadcrumb">
                <ol class="breadcrumb">
                    <li class="breadcrumb-item"><a th:href="@{/admin/users}">사용자 관리</a></li>
                    <li class="breadcrumb-item active" th:text="${user.username}"></li>
                </ol>
            </nav>
        </div>
        
        <div class="btn-group">
            <a th:href="@{/admin/users/{id}/edit(id=${user.id})}" class="btn btn-warning">
                <i class="fas fa-edit"></i> 수정
            </a>
            <button type="button" class="btn btn-danger" 
                    onclick="deleteUser([[${user.id}]], '[[${user.username}]]')">
                <i class="fas fa-trash"></i> 삭제
            </button>
            <a th:href="@{/admin/users}" class="btn btn-secondary">
                <i class="fas fa-list"></i> 목록으로
            </a>
        </div>
    </div>
    
    <div class="row">
        <!-- 기본 정보 -->
        <div class="col-md-8">
            <div class="card info-card mb-4">
                <div class="card-header">
                    <h5 class="card-title mb-0"><i class="fas fa-info-circle"></i> 기본 정보</h5>
                </div>
                <div class="card-body">
                    <div class="row">
                        <div class="col-md-6">
                            <div class="info-label">사용자명</div>
                            <div class="info-value" th:text="${user.username}"></div>
                            
                            <div class="info-label">이메일</div>
                            <div class="info-value">
                                <a th:href="'mailto:' + ${user.email}" th:text="${user.email}"></a>
                            </div>
                            
                            <div class="info-label">전화번호</div>
                            <div class="info-value" th:text="${user.phone ?: '-'}"></div>
                        </div>
                        
                        <div class="col-md-6">
                            <div class="info-label">역할</div>
                            <div class="info-value">
                                <span class="badge status-badge" 
                                      th:classappend="${user.role.name() == 'ADMIN' ? 'bg-danger' : 'bg-info'}"
                                      th:text="${user.role.displayName}"></span>
                            </div>
                            
                            <div class="info-label">상태</div>
                            <div class="info-value">
                                <span class="badge status-badge" 
                                      th:classappend="${user.status.name() == 'ACTIVE' ? 'bg-success' : 'bg-secondary'}"
                                      th:text="${user.status.displayName}"></span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- 활동 정보 -->
        <div class="col-md-4">
            <div class="card info-card mb-4">
                <div class="card-header">
                    <h5 class="card-title mb-0"><i class="fas fa-clock"></i> 활동 정보</h5>
                </div>
                <div class="card-body">
                    <div class="info-label">가입일</div>
                    <div class="info-value" th:text="${#temporals.format(user.createdAt, 'yyyy년 MM월 dd일 HH:mm')}"></div>
                    
                    <div class="info-label">최종 수정일</div>
                    <div class="info-value" th:text="${user.updatedAt != null ? #temporals.format(user.updatedAt, 'yyyy년 MM월 dd일 HH:mm') : '-'}"></div>
                    
                    <div class="info-label">마지막 로그인</div>
                    <div class="info-value" th:text="${user.lastLoginAt != null ? #temporals.format(user.lastLoginAt, 'yyyy년 MM월 dd일 HH:mm') : '로그인 기록 없음'}"></div>
                </div>
            </div>
        </div>
    </div>
    
    <!-- 추가 정보나 관련 데이터가 있다면 여기에 추가 -->
    <div class="row">
        <div class="col-12">
            <div class="card info-card">
                <div class="card-header">
                    <h5 class="card-title mb-0"><i class="fas fa-history"></i> 활동 로그</h5>
                </div>
                <div class="card-body">
                    <div class="text-muted text-center py-4">
                        <i class="fas fa-info-circle fa-2x mb-2"></i>
                        <div>활동 로그 기능은 추후 구현 예정입니다.</div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>

<th:block layout:fragment="script">
    <script>
        // 사용자 삭제
        function deleteUser(userId, username) {
            if (confirm(`정말로 '${username}' 사용자를 삭제하시겠습니까?`)) {
                fetch(`/admin/users/${userId}`, {
                    method: 'DELETE',
                    headers: {
                        'Content-Type': 'application/json',
                        'X-Requested-With': 'XMLHttpRequest'
                    }
                })
                .then(response => response.json())
                .then(data => {
                    if (data.message) {
                        alert(data.message);
                        window.location.href = '/admin/users';
                    } else if (data.error) {
                        alert('오류: ' + data.error);
                    }
                })
                .catch(error => {
                    console.error('Error:', error);
                    alert('삭제 중 오류가 발생했습니다.');
                });
            }
        }
    </script>
</th:block>
```

### 7.4 사용자 생성/수정 폼 (admin/users/form.html)

```html
<!DOCTYPE html>
<html lang="ko" 
      xmlns:th="http://www.thymeleaf.org"
      xmlns:layout="http://www.ultraq.net.nz/thymeleaf/layout"
      layout:decorate="~{layout/admin}">

<th:block layout:fragment="css">
    <style>
        .form-card { border: none; box-shadow: 0 0.125rem 0.25rem rgba(0, 0, 0, 0.075); }
        .required { color: #dc3545; }
        .form-help { font-size: 0.875rem; color: #6c757d; }
        .password-toggle { cursor: pointer; }
    </style>
</th:block>

<div layout:fragment="content">
    <div class="row justify-content-center">
        <div class="col-lg-8">
            <div class="d-flex justify-content-between align-items-center mb-4">
                <div>
                    <h2 th:if="${userId == null}"><i class="fas fa-plus"></i> 새 사용자 추가</h2>
                    <h2 th:if="${userId != null}"><i class="fas fa-edit"></i> 사용자 수정</h2>
                    <nav aria-label="breadcrumb">
                        <ol class="breadcrumb">
                            <li class="breadcrumb-item"><a th:href="@{/admin/users}">사용자 관리</a></li>
                            <li class="breadcrumb-item active" th:text="${userId == null ? '새 사용자 추가' : '사용자 수정'}"></li>
                        </ol>
                    </nav>
                </div>
                
                <a th:href="${userId != null ? '/admin/users/' + userId : '/admin/users'}" 
                   class="btn btn-secondary">
                    <i class="fas fa-arrow-left"></i> 돌아가기
                </a>
            </div>
            
            <div class="card form-card">
                <div class="card-body">
                    <form th:action="${userId == null ? '/admin/users/new' : '/admin/users/' + userId + '/edit'}" 
                          method="post" 
                          th:object="${userForm}"
                          novalidate>
                        
                        <!-- 전체 오류 메시지 -->
                        <div th:if="${#fields.hasGlobalErrors()}" class="alert alert-danger">
                            <ul class="mb-0">
                                <li th:each="error : ${#fields.globalErrors()}" th:text="${error}"></li>
                            </ul>
                        </div>
                        
                        <div class="row">
                            <!-- 사용자명 -->
                            <div class="col-md-6 mb-3">
                                <label for="username" class="form-label">
                                    사용자명 <span class="required">*</span>
                                </label>
                                <input type="text" 
                                       class="form-control" 
                                       th:field="*{username}"
                                       th:classappend="${#fields.hasErrors('username')} ? 'is-invalid'"
                                       th:readonly="${userId != null}"
                                       placeholder="사용자명을 입력하세요">
                                <div class="form-help" th:if="${userId == null}">3-50자 사이로 입력해주세요.</div>
                                <div class="invalid-feedback" th:if="${#fields.hasErrors('username')}" th:errors="*{username}"></div>
                            </div>
                            
                            <!-- 이메일 -->
                            <div class="col-md-6 mb-3">
                                <label for="email" class="form-label">
                                    이메일 <span class="required">*</span>
                                </label>
                                <input type="email" 
                                       class="form-control" 
                                       th:field="*{email}"
                                       th:classappend="${#fields.hasErrors('email')} ? 'is-invalid'"
                                       placeholder="이메일을 입력하세요">
                                <div class="invalid-feedback" th:if="${#fields.hasErrors('email')}" th:errors="*{email}"></div>
                            </div>
                        </div>
                        
                        <div class="row">
                            <!-- 비밀번호 -->
                            <div class="col-md-6 mb-3">
                                <label for="password" class="form-label">
                                    비밀번호 
                                    <span class="required" th:if="${userId == null}">*</span>
                                    <span th:if="${userId != null}" class="form-help">(변경시에만 입력)</span>
                                </label>
                                <div class="input-group">
                                    <input type="password" 
                                           class="form-control" 
                                           th:field="*{password}"
                                           th:classappend="${#fields.hasErrors('password')} ? 'is-invalid'"
                                           placeholder="비밀번호를 입력하세요"
                                           id="passwordInput">
                                    <button class="btn btn-outline-secondary password-toggle" type="button" onclick="togglePassword()">
                                        <i class="fas fa-eye" id="passwordToggleIcon"></i>
                                    </button>
                                </div>
                                <div class="form-help">최소 8자 이상 입력해주세요.</div>
                                <div class="invalid-feedback" th:if="${#fields.hasErrors('password')}" th:errors="*{password}"></div>
                            </div>
                            
                            <!-- 전화번호 -->
                            <div class="col-md-6 mb-3">
                                <label for="phone" class="form-label">전화번호</label>
                                <input type="tel" 
                                       class="form-control" 
                                       th:field="*{phone}"
                                       th:classappend="${#fields.hasErrors('phone')} ? 'is-invalid'"
                                       placeholder="010-1234-5678">
                                <div class="form-help">하이픈(-) 포함하여 입력해주세요.</div>
                                <div class="invalid-feedback" th:if="${#fields.hasErrors('phone')}" th:errors="*{phone}"></div>
                            </div>
                        </div>
                        
                        <div class="row">
                            <!-- 역할 -->
                            <div class="col-md-6 mb-3">
                                <label for="role" class="form-label">
                                    역할 <span class="required">*</span>
                                </label>
                                <select class="form-select" 
                                        th:field="*{role}"
                                        th:classappend="${#fields.hasErrors('role')} ? 'is-invalid'">
                                    <option value="">역할을 선택하세요</option>
                                    <option th:each="role : ${roles}" 
                                            th:value="${role}" 
                                            th:text="${role.displayName}"></option>
                                </select>
                                <div class="invalid-feedback" th:if="${#fields.hasErrors('role')}" th:errors="*{role}"></div>
                            </div>
                            
                            <!-- 상태 -->
                            <div class="col-md-6 mb-3">
                                <label for="status" class="form-label">
                                    상태 <span class="required">*</span>
                                </label>
                                <select class="form-select" 
                                        th:field="*{status}"
                                        th:classappend="${#fields.hasErrors('status')} ? 'is-invalid'">
                                    <option value="">상태를 선택하세요</option>
                                    <option th:each="status : ${statuses}" 
                                            th:value="${status}" 
                                            th:text="${status.displayName}"></option>
                                </select>
                                <div class="invalid-feedback" th:if="${#fields.hasErrors('status')}" th:errors="*{status}"></div>
                            </div>
                        </div>
                        
                        <hr class="my-4">
                        
                        <!-- 버튼 그룹 -->
                        <div class="d-flex justify-content-end gap-2">
                            <a th:href="${userId != null ? '/admin/users/' + userId : '/admin/users'}" 
                               class="btn btn-secondary">
                                <i class="fas fa-times"></i> 취소
                            </a>
                            <button type="submit" class="btn btn-primary">
                                <i th:class="${userId == null ? 'fas fa-plus' : 'fas fa-save'}"></i>
                                <span th:text="${userId == null ? '사용자 추가' : '수정 저장'}"></span>
                            </button>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </div>
</div>

<th:block layout:fragment="script">
    <script>
        // 비밀번호 보기/숨기기 토글
        function togglePassword() {
            const passwordInput = document.getElementById('passwordInput');
            const toggleIcon = document.getElementById('passwordToggleIcon');
            
            if (passwordInput.type === 'password') {
                passwordInput.type = 'text';
                toggleIcon.className = 'fas fa-eye-slash';
            } else {
                passwordInput.type = 'password';
                toggleIcon.className = 'fas fa-eye';
            }
        }
        
        // 폼 제출 전 확인
        document.querySelector('form').addEventListener('submit', function(e) {
            const isEdit = [[${userId != null}]];
            const username = document.getElementById('username').value;
            
            let message = isEdit ? 
                `'${username}' 사용자 정보를 수정하시겠습니까?` : 
                `'${username}' 사용자를 생성하시겠습니까?`;
                
            if (!confirm(message)) {
                e.preventDefault();
            }
        });
        
        // 전화번호 자동 포맷팅
        document.getElementById('phone').addEventListener('input', function(e) {
            let value = e.target.value.replace(/[^0-9]/g, '');
            if (value.length >= 11) {
                value = value.replace(/(\d{3})(\d{4})(\d{4})/, '$1-$2-$3');
            } else if (value.length >= 7) {
                value = value.replace(/(\d{3})(\d{3})(\d+)/, '$1-$2-$3');
            } else if (value.length >= 3) {
                value = value.replace(/(\d{3})(\d+)/, '$1-$2');
            }
            e.target.value = value;
        });
    </script>
</th:block>
```

## 8. Enum 클래스 정의

```java
// 사용자 역할
public enum UserRole {
    ADMIN("관리자"),
    USER("일반사용자"),
    MANAGER("매니저");
    
    private final String displayName;
    
    UserRole(String displayName) {
        this.displayName = displayName;
    }
    
    public String getDisplayName() {
        return displayName;
    }
}

// 사용자 상태
public enum UserStatus {
    ACTIVE("활성"),
    INACTIVE("비활성"),
    SUSPENDED("정지"),
    DELETED("삭제");
    
    private final String displayName;
    
    UserStatus(String displayName) {
        this.displayName = displayName;
    }
    
    public String getDisplayName() {
        return displayName;
    }
}
```

## 9. 설정 파일

### 9.1 application.yml

```yaml
spring:
  datasource:
    url: jdbc:h2:mem:testdb
    driver-class-name: org.h2.Driver
    username: sa
    password: 
    
  jpa:
    hibernate:
      ddl-auto: create-drop
    show-sql: true
    properties:
      hibernate:
        format_sql: true
        
  thymeleaf:
    cache: false
    prefix: classpath:/templates/
    suffix: .html
    
  web:
    resources:
      static-locations: classpath:/static/
      
server:
  port: 8080
  
logging:
  level:
    org.hibernate.SQL: DEBUG
    org.hibernate.type.descriptor.sql.BasicBinder: TRACE
```

### 9.2 JPA 설정 클래스

```java
@Configuration
@EnableJpaAuditing
public class JpaConfig {
    
    @Bean
    public AuditorAware<String> auditorProvider() {
        return () -> {
            // 실제 구현에서는 SecurityContext에서 현재 사용자 정보를 가져와야 함
            return Optional.of("system");
        };
    }
}
```

## 10. CSS 스타일 (static/css/admin.css)

```css
/* 관리자 페이지 공통 스타일 */
body {
    background-color: #f8f9fa;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
}

.navbar-brand {
    font-weight: 600;
}

.card {
    border-radius: 8px;
    margin-bottom: 1.5rem;
}

.btn {
    border-radius: 6px;
    font-weight: 500;
}

.table th {
    font-weight: 600;
    border-bottom: 2px solid #dee2e6;
}

.badge {
    font-size: 0.75rem;
    font-weight: 500;
}

.pagination .page-link {
    border-radius: 6px;
    margin: 0 2px;
    border: 1px solid #dee2e6;
}

.pagination .page-item.active .page-link {
    background-color: #0d6efd;
    border-color: #0d6efd;
}

/* 검색 폼 스타일 */
.search-form {
    background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
    border: 1px solid #dee2e6;
}

/* 테이블 반응형 */
@media (max-width: 768px) {
    .table-responsive {
        font-size: 0.875rem;
    }
    
    .btn-group-sm .btn {
        padding: 0.125rem 0.5rem;
        font-size: 0.75rem;
    }
}

/* 폼 스타일 */
.form-control:focus,
.form-select:focus {
    border-color: #86b7fe;
    box-shadow: 0 0 0 0.25rem rgba(13, 110, 253, 0.25);
}

.required {
    color: #dc3545;
}

/* 알림 스타일 */
.alert {
    border-radius: 8px;
    border: none;
}

.alert-success {
    background-color: #d1e7dd;
    color: #0a3622;
}

.alert-danger {
    background-color: #f8d7da;
    color: #58151c;
}

/* 로딩 스피너 */
.spinner-border-sm {
    width: 1rem;
    height: 1rem;
}

/* 커스텀 배지 색상 */
.bg-info {
    background-color: #0dcaf0 !important;
}

.bg-warning {
    background-color: #ffc107 !important;
    color: #000 !important;
}
```

## 11. JavaScript 공통 함수 (static/js/admin.js)

```javascript
// 관리자 페이지 공통 JavaScript

// 전역 유틸리티 함수
const AdminUtils = {
    // 확인 대화상자
    confirm: function(message, callback) {
        if (confirm(message)) {
            if (typeof callback === 'function') {
                callback();
            }
            return true;
        }
        return false;
    },
    
    // AJAX 요청 공통 함수
    request: function(url, options = {}) {
        const defaultOptions = {
            headers: {
                'Content-Type': 'application/json',
                'X-Requested-With': 'XMLHttpRequest'
            }
        };
        
        return fetch(url, { ...defaultOptions, ...options })
            .then(response => {
                if (!response.ok) {
                    throw new Error(`HTTP error! status: ${response.status}`);
                }
                return response.json();
            });
    },
    
    // 알림 메시지 표시
    showAlert: function(message, type = 'info') {
        const alertHtml = `
            <div class="alert alert-${type} alert-dismissible fade show" role="alert">
                <i class="fas fa-${type === 'success' ? 'check-circle' : type === 'danger' ? 'exclamation-circle' : 'info-circle'}"></i>
                ${message}
                <button type="button" class="btn-close" data-bs-dismiss="alert"></button>
            </div>
        `;
        
        const container = document.querySelector('.container-fluid');
        if (container) {
            container.insertAdjacentHTML('afterbegin', alertHtml);
            
            // 5초 후 자동 제거
            setTimeout(() => {
                const alert = container.querySelector('.alert');
                if (alert) {
                    alert.remove();
                }
            }, 5000);
        }
    },
    
    // 로딩 상태 표시
    showLoading: function(element, show = true) {
        if (show) {
            element.disabled = true;
            const originalText = element.textContent;
            element.dataset.originalText = originalText;
            element.innerHTML = '<span class="spinner-border spinner-border-sm me-2"></span>처리중...';
        } else {
            element.disabled = false;
            element.textContent = element.dataset.originalText || '확인';
        }
    },
    
    // 날짜 포맷팅
    formatDate: function(dateString, format = 'YYYY-MM-DD HH:mm') {
        const date = new Date(dateString);
        const year = date.getFullYear();
        const month = String(date.getMonth() + 1).padStart(2, '0');
        const day = String(date.getDate()).padStart(2, '0');
        const hours = String(date.getHours()).padStart(2, '0');
        const minutes = String(date.getMinutes()).padStart(2, '0');
        
        return format
            .replace('YYYY', year)
            .replace('MM', month)
            .replace('DD', day)
            .replace('HH', hours)
            .replace('mm', minutes);
    }
};

// 페이지 로드 시 초기화
document.addEventListener('DOMContentLoaded', function() {
    // 툴팁 초기화
    const tooltipTriggerList = [].slice.call(document.querySelectorAll('[data-bs-toggle="tooltip"]'));
    tooltipTriggerList.map(function (tooltipTriggerEl) {
        return new bootstrap.Tooltip(tooltipTriggerEl);
    });
    
    // 모든 테이블에 반응형 클래스 추가
    document.querySelectorAll('table').forEach(table => {
        if (!table.closest('.table-responsive')) {
            table.classList.add('table-responsive');
        }
    });
    
    // 폼 유효성 검사 스타일 적용
    document.querySelectorAll('.needs-validation').forEach(form => {
        form.addEventListener('submit', function(e) {
            if (!form.checkValidity()) {
                e.preventDefault();
                e.stopPropagation();
            }
            form.classList.add('was-validated');
        });
    });
});
```

## 12. 추가 기능 구현 예시

### 12.1 엑셀 다운로드 기능

```java
// Controller에 추가
@GetMapping("/export")
public void exportUsers(
        @ModelAttribute UserSearchDto searchDto,
        HttpServletResponse response) throws IOException {
    
    response.setContentType("application/vnd.openxmlformats-officedocument.spreadsheetml.sheet");
    response.setHeader("Content-Disposition", "attachment; filename=users.xlsx");
    
    List<UserListDto> users = userService.getAllUsers(searchDto);
    
    try (Workbook workbook = new XSSFWorkbook()) {
        Sheet sheet = workbook.createSheet("사용자 목록");
        
        // 헤더 생성
        Row headerRow = sheet.createRow(0);
        String[] headers = {"ID", "사용자명", "이메일", "전화번호", "역할", "상태", "가입일"};
        for (int i = 0; i < headers.length; i++) {
            Cell cell = headerRow.createCell(i);
            cell.setCellValue(headers[i]);
        }
        
        // 데이터 생성
        int rowNum = 1;
        for (UserListDto user : users) {
            Row row = sheet.createRow(rowNum++);
            row.createCell(0).setCellValue(user.getId());
            row.createCell(1).setCellValue(user.getUsername());
            row.createCell(2).setCellValue(user.getEmail());
            row.createCell(3).setCellValue(user.getPhone());
            row.createCell(4).setCellValue(user.getRole().getDisplayName());
            row.createCell(5).setCellValue(user.getStatus().getDisplayName());
            row.createCell(6).setCellValue(user.getCreatedAt().toString());
        }
        
        // 컬럼 크기 자동 조정
        for (int i = 0; i < headers.length; i++) {
            sheet.autoSizeColumn(i);
        }
        
        workbook.write(response.getOutputStream());
    }
}
```

### 12.2 대량 작업 기능

```javascript
// 체크박스 전체 선택/해제
function toggleAllCheckboxes(source) {
    const checkboxes = document.querySelectorAll('input[name="selectedIds"]');
    checkboxes.forEach(checkbox => {
        checkbox.checked = source.checked;
    });
    updateBulkActionButtons();
}

// 선택된 항목 수에 따른 버튼 상태 업데이트
function updateBulkActionButtons() {
    const selectedCount = document.querySelectorAll('input[name="selectedIds"]:checked').length;
    const bulkButtons = document.querySelector('.bulk-actions');
    
    if (selectedCount > 0) {
        bulkButtons.style.display = 'block';
        document.getElementById('selectedCount').textContent = selectedCount;
    } else {
        bulkButtons.style.display = 'none';
    }
}

// 대량 삭제
function bulkDelete() {
    const selectedIds = Array.from(document.querySelectorAll('input[name="selectedIds"]:checked'))
        .map(checkbox => checkbox.value);
    
    if (selectedIds.length === 0) {
        alert('삭제할 항목을 선택해주세요.');
        return;
    }
    
    if (confirm(`선택된 ${selectedIds.length}개의 사용자를 삭제하시겠습니까?`)) {
        AdminUtils.request('/admin/users/bulk-delete', {
            method: 'POST',
            body: JSON.stringify({ ids: selectedIds })
        })
        .then(data => {
            AdminUtils.showAlert(data.message, 'success');
            location.reload();
        })
        .catch(error => {
            AdminUtils.showAlert('삭제 중 오류가 발생했습니다.', 'danger');
        });
    }
}
```

## 13. 보안 고려사항

### 13.1 Spring Security 설정 (선택사항)

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig {
    
    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/admin/**").hasRole("ADMIN")
                .requestMatchers("/css/**", "/js/**", "/images/**").permitAll()
                .anyRequest().authenticated()
            )
            .formLogin(form -> form
                .loginPage("/login")
                .defaultSuccessUrl("/admin")
                .permitAll()
            )
            .logout(logout -> logout
                .logoutUrl("/logout")
                .logoutSuccessUrl("/login")
                .permitAll()
            )
            .csrf(csrf -> csrf
                .csrfTokenRepository(CookieCsrfTokenRepository.withHttpOnlyFalse())
            );
            
        return http.build();
    }
    
    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }
}
```

### 13.2 입력 검증 및 XSS 방지

```java
// XSS 방지를 위한 HTML 이스케이프 유틸리티
@Component
public class SecurityUtils {
    
    private static final PolicyFactory POLICY = Sanitizers.FORMATTING.and(Sanitizers.LINKS);
    
    public static String sanitizeHtml(String input) {
        if (input == null) return null;
        return POLICY.sanitize(input);
    }
    
    public static String escapeHtml(String input) {
        if (input == null) return null;
        return StringEscapeUtils.escapeHtml4(input);
    }
}
```

## 14. 테스트 코드 예시

### 14.1 Service 테스트

```java
@SpringBootTest
@Transactional
class UserServiceTest {
    
    @Autowired
    private UserService userService;
    
    @Autowired
    private UserRepository userRepository;
    
    @Test
    @DisplayName("사용자 생성 테스트")
    void createUser() {
        // given
        UserFormDto userForm = new UserFormDto();
        userForm.setUsername("testuser");
        userForm.setPassword("password123");
        userForm.setEmail("test@example.com");
        userForm.setRole(UserRole.USER);
        userForm.setStatus(UserStatus.ACTIVE);
        
        // when
        Long userId = userService.createUser(userForm);
        
        // then
        assertThat(userId).isNotNull();
        Optional<User> savedUser = userRepository.findById(userId);
        assertThat(savedUser).isPresent();
        assertThat(savedUser.get().getUsername()).isEqualTo("testuser");
    }
    
    @Test
    @DisplayName("중복 사용자명 검증 테스트")
    void createUserWithDuplicateUsername() {
        // given
        User existingUser = User.builder()
                .username("duplicate")
                .password("password")
                .email("existing@example.com")
                .role(UserRole.USER)
                .status(UserStatus.ACTIVE)
                .build();
        userRepository.save(existingUser);
        
        UserFormDto userForm = new UserFormDto();
        userForm.setUsername("duplicate");
        userForm.setPassword("password123");
        userForm.setEmail("new@example.com");
        userForm.setRole(UserRole.USER);
        userForm.setStatus(UserStatus.ACTIVE);
        
        // when & then
        assertThatThrownBy(() -> userService.createUser(userForm))
                .isInstanceOf(DuplicateKeyException.class)
                .hasMessageContaining("이미 존재하는 사용자명입니다");
    }
}
```

### 14.2 Controller 테스트

```java
@WebMvcTest(UserController.class)
class UserControllerTest {
    
    @Autowired
    private MockMvc mockMvc;
    
    @MockBean
    private UserService userService;
    
    @Test
    @DisplayName("사용자 목록 페이지 테스트")
    void userListPage() throws Exception {
        // given
        List<UserListDto> users = Arrays.asList(
                UserListDto.builder().id(1L).username("user1").build(),
                UserListDto.builder().id(2L).username("user2").build()
        );
        Page<UserListDto> userPage = new PageImpl<>(users);
        
        when(userService.getUsers(any(UserSearchDto.class))).thenReturn(userPage);
        
        // when & then
        mockMvc.perform(get("/admin/users"))
                .andExpect(status().isOk())
                .andExpect(view().name("admin/users/list"))
                .andExpect(model().attributeExists("users"))
                .andExpect(model().attribute("users", userPage));
    }
}
```

## 15. 배포 및 운영 가이드

### 15.1 프로덕션 설정 (application-prod.yml)

```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/admin_db
    username: ${DB_USERNAME}
    password: ${DB_PASSWORD}
    driver-class-name: com.mysql.cj.jdbc.Driver
    
  jpa:
    hibernate:
      ddl-auto: validate
    show-sql: false
    properties:
      hibernate:
        dialect: org.hibernate.dialect.MySQL8Dialect
        
  thymeleaf:
    cache: true
    
logging:
  level:
    com.example.admin: INFO
    org.hibernate.SQL: WARN
    
server:
  port: 8080
  compression:
    enabled: true
    mime-types: text/html,text/xml,text/plain,text/css,text/javascript,application/javascript,application/json
```

### 15.2 Docker 설정

```dockerfile
FROM openjdk:17-jdk-slim

VOLUME /tmp

COPY target/admin-app.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "/app.jar", "--spring.profiles.active=prod"]
```
