# React 컴포넌트 설계 가이드
**ReactJS + ECMAScript JSX + Vite + React Router + RTK 환경**

## 1. React 컴포넌트 설계 원칙

### 1.1 단일 책임 원칙 (Single Responsibility Principle)
- **원칙**: 하나의 컴포넌트는 하나의 명확한 책임만을 가져야 합니다
- **권고사항**: 
  - 컴포넌트가 50줄을 넘어가면 분리를 고려하세요
  - 컴포넌트 이름만 봐도 기능을 알 수 있도록 명명하세요
  - 여러 기능이 섞여있다면 각각을 별도 컴포넌트로 분리하세요

### 1.2 컴포넌트 계층 구조
- **원칙**: 명확한 부모-자식 관계를 유지하고, 깊은 중첩을 피하세요
- **권고사항**:
  - 컴포넌트 트리의 깊이는 5단계를 넘지 않도록 하세요
  - 형제 컴포넌트 간 직접 통신을 피하고, 부모를 통해 소통하세요
  - 공통 부모에서 상태를 관리하세요

### 1.3 재사용성과 확장성
- **원칙**: 컴포넌트는 재사용 가능하고 확장 가능하게 설계해야 합니다
- **권고사항**:
  - UI 컴포넌트와 비즈니스 로직 컴포넌트를 분리하세요
  - 공통 컴포넌트는 `/components/common/` 폴더에 관리하세요
  - 컴포넌트에 기본값(defaultProps)을 제공하세요

### 1.4 파일 구조 및 네이밍
```
src/
├── components/
│   ├── common/          # 재사용 가능한 공통 컴포넌트
│   ├── layout/          # 레이아웃 관련 컴포넌트
│   └── features/        # 기능별 컴포넌트
├── pages/               # 페이지 컴포넌트
├── hooks/               # 커스텀 훅
├── store/               # Redux 스토어
├── services/            # API 관련 서비스
└── utils/               # 유틸리티 함수
```

## 2. React 컴포넌트 Props 설계 원칙

### 2.1 Props 명명 규칙
- **원칙**: 명확하고 일관된 props 이름을 사용하세요
- **권고사항**:
  - 불린 타입은 `is`, `has`, `can`, `should`로 시작
  - 이벤트 핸들러는 `on`으로 시작 (onClick, onSubmit)
  - 데이터 props는 명사형으로 작성
  - 함수 props는 동사형으로 작성

### 2.2 Props 최소화
- **원칙**: 필요한 최소한의 props만 전달하세요
- **권고사항**:
  - props가 5개를 넘어가면 객체로 묶어서 전달 고려
  - 불필요한 props 전달을 피하세요
  - props drilling이 3단계를 넘어가면 Context API나 Redux 사용 고려

### 2.3 Props 검증
- **원칙**: PropTypes를 사용하여 props를 검증하세요
- **권고사항**:
  - 모든 컴포넌트에 PropTypes 정의
  - 필수 props는 `isRequired` 명시
  - 기본값은 `defaultProps`로 제공

### 2.4 Props 구조화
- **원칙**: 관련된 props는 객체로 그룹화하세요
- **권고사항**:
  - 스타일 관련 props는 `style` 객체로 통합
  - 설정 관련 props는 `config` 객체로 통합
  - 이벤트 핸들러들은 `handlers` 객체로 통합 고려

## 3. Redux(RTK) 상태관리 설계 원칙

### 3.1 상태 분리 원칙
- **원칙**: 로컬 상태와 글로벌 상태를 명확히 구분하세요
- **글로벌 상태**: 여러 컴포넌트에서 공유되는 상태
  - 사용자 인증 정보
  - 전역 설정 정보
  - 캐시된 API 데이터
- **로컬 상태**: 단일 컴포넌트나 작은 컴포넌트 그룹에서만 사용
  - 폼 입력값
  - 모달 열림/닫힘 상태
  - 임시 UI 상태

### 3.2 Slice 설계 원칙
- **원칙**: 기능 단위로 slice를 분리하세요
- **권고사항**:
  - 하나의 slice는 하나의 도메인을 담당
  - slice 이름은 명확하고 일관성 있게 작성
  - 액션 타입은 `도메인/액션명` 형태로 작성

### 3.3 상태 정규화
- **원칙**: 중첩된 데이터는 정규화하여 관리하세요
- **권고사항**:
  - 배열 데이터는 id를 키로 하는 객체로 변환
  - 중복 데이터를 최소화
  - 관계형 데이터는 별도 slice로 분리

### 3.4 비동기 작업 관리
- **원칙**: createAsyncThunk를 사용하여 비동기 작업을 관리하세요
- **권고사항**:
  - API 호출은 별도 서비스 파일로 분리
  - 로딩, 성공, 실패 상태를 명확히 관리
  - 에러 처리는 일관된 방식으로 구현

## 4. 실제 코드 예시

### 4.1 컴포넌트 설계 예시

#### 공통 버튼 컴포넌트
```jsx
// components/common/Button/Button.jsx
import PropTypes from 'prop-types';
import './Button.css';

const Button = ({ 
  children, 
  variant = 'primary', 
  size = 'medium', 
  disabled = false, 
  loading = false,
  onClick,
  type = 'button',
  className = '',
  ...rest 
}) => {
  const buttonClass = `
    btn 
    btn--${variant} 
    btn--${size} 
    ${disabled ? 'btn--disabled' : ''} 
    ${loading ? 'btn--loading' : ''} 
    ${className}
  `.trim();

  const handleClick = (e) => {
    if (disabled || loading) return;
    onClick?.(e);
  };

  return (
    <button
      type={type}
      className={buttonClass}
      onClick={handleClick}
      disabled={disabled || loading}
      {...rest}
    >
      {loading ? (
        <>
          <span className="btn__spinner" />
          Loading...
        </>
      ) : (
        children
      )}
    </button>
  );
};

Button.propTypes = {
  children: PropTypes.node.isRequired,
  variant: PropTypes.oneOf(['primary', 'secondary', 'danger']),
  size: PropTypes.oneOf(['small', 'medium', 'large']),
  disabled: PropTypes.bool,
  loading: PropTypes.bool,
  onClick: PropTypes.func,
  type: PropTypes.oneOf(['button', 'submit', 'reset']),
  className: PropTypes.string,
};

export default Button;
```

#### 사용자 카드 컴포넌트
```jsx
// components/features/UserCard/UserCard.jsx
import PropTypes from 'prop-types';
import Button from '../../common/Button/Button';
import './UserCard.css';

const UserCard = ({ user, onEdit, onDelete, isLoading = false }) => {
  const { id, name, email, avatar, role } = user;

  const handleEdit = () => {
    onEdit?.(user);
  };

  const handleDelete = () => {
    if (window.confirm('정말 삭제하시겠습니까?')) {
      onDelete?.(id);
    }
  };

  return (
    <div className="user-card">
      <div className="user-card__avatar">
        <img src={avatar} alt={`${name}의 프로필`} />
      </div>
      
      <div className="user-card__info">
        <h3 className="user-card__name">{name}</h3>
        <p className="user-card__email">{email}</p>
        <span className="user-card__role">{role}</span>
      </div>
      
      <div className="user-card__actions">
        <Button 
          variant="secondary" 
          size="small" 
          onClick={handleEdit}
          disabled={isLoading}
        >
          편집
        </Button>
        <Button 
          variant="danger" 
          size="small" 
          onClick={handleDelete}
          disabled={isLoading}
        >
          삭제
        </Button>
      </div>
    </div>
  );
};

UserCard.propTypes = {
  user: PropTypes.shape({
    id: PropTypes.oneOfType([PropTypes.string, PropTypes.number]).isRequired,
    name: PropTypes.string.isRequired,
    email: PropTypes.string.isRequired,
    avatar: PropTypes.string,
    role: PropTypes.string,
  }).isRequired,
  onEdit: PropTypes.func,
  onDelete: PropTypes.func,
  isLoading: PropTypes.bool,
};

export default UserCard;
```

#### 사용자 목록 페이지 컴포넌트
```jsx
// pages/UsersPage/UsersPage.jsx
import { useEffect } from 'react';
import { useDispatch, useSelector } from 'react-redux';
import UserCard from '../../components/features/UserCard/UserCard';
import Button from '../../components/common/Button/Button';
import { fetchUsers, deleteUser } from '../../store/slices/usersSlice';
import './UsersPage.css';

const UsersPage = () => {
  const dispatch = useDispatch();
  const { users, loading, error } = useSelector(state => state.users);

  useEffect(() => {
    dispatch(fetchUsers());
  }, [dispatch]);

  const handleEditUser = (user) => {
    // 편집 로직 또는 라우팅
    console.log('Edit user:', user);
  };

  const handleDeleteUser = (userId) => {
    dispatch(deleteUser(userId));
  };

  if (loading) {
    return <div className="users-page__loading">로딩 중...</div>;
  }

  if (error) {
    return <div className="users-page__error">에러: {error}</div>;
  }

  return (
    <div className="users-page">
      <div className="users-page__header">
        <h1>사용자 관리</h1>
        <Button onClick={() => console.log('Add user')}>
          사용자 추가
        </Button>
      </div>

      <div className="users-page__grid">
        {users.map(user => (
          <UserCard
            key={user.id}
            user={user}
            onEdit={handleEditUser}
            onDelete={handleDeleteUser}
            isLoading={loading}
          />
        ))}
      </div>
    </div>
  );
};

export default UsersPage;
```

### 4.2 Redux Store 설계 예시

#### Users Slice
```jsx
// store/slices/usersSlice.js
import { createSlice, createAsyncThunk } from '@reduxjs/toolkit';
import { usersAPI } from '../../services/api';

// 비동기 액션 생성
export const fetchUsers = createAsyncThunk(
  'users/fetchUsers',
  async (_, { rejectWithValue }) => {
    try {
      const response = await usersAPI.getUsers();
      return response.data;
    } catch (error) {
      return rejectWithValue(error.response?.data?.message || '사용자 목록을 불러오는데 실패했습니다.');
    }
  }
);

export const deleteUser = createAsyncThunk(
  'users/deleteUser',
  async (userId, { rejectWithValue }) => {
    try {
      await usersAPI.deleteUser(userId);
      return userId;
    } catch (error) {
      return rejectWithValue(error.response?.data?.message || '사용자 삭제에 실패했습니다.');
    }
  }
);

export const createUser = createAsyncThunk(
  'users/createUser',
  async (userData, { rejectWithValue }) => {
    try {
      const response = await usersAPI.createUser(userData);
      return response.data;
    } catch (error) {
      return rejectWithValue(error.response?.data?.message || '사용자 생성에 실패했습니다.');
    }
  }
);

// 초기 상태
const initialState = {
  users: [],
  selectedUser: null,
  loading: false,
  error: null,
  totalCount: 0,
  currentPage: 1,
};

// Slice 생성
const usersSlice = createSlice({
  name: 'users',
  initialState,
  reducers: {
    // 동기 액션들
    clearError: (state) => {
      state.error = null;
    },
    setSelectedUser: (state, action) => {
      state.selectedUser = action.payload;
    },
    clearSelectedUser: (state) => {
      state.selectedUser = null;
    },
    setCurrentPage: (state, action) => {
      state.currentPage = action.payload;
    },
  },
  extraReducers: (builder) => {
    builder
      // fetchUsers 액션 처리
      .addCase(fetchUsers.pending, (state) => {
        state.loading = true;
        state.error = null;
      })
      .addCase(fetchUsers.fulfilled, (state, action) => {
        state.loading = false;
        state.users = action.payload;
        state.totalCount = action.payload.length;
      })
      .addCase(fetchUsers.rejected, (state, action) => {
        state.loading = false;
        state.error = action.payload;
      })
      // deleteUser 액션 처리
      .addCase(deleteUser.pending, (state) => {
        state.loading = true;
      })
      .addCase(deleteUser.fulfilled, (state, action) => {
        state.loading = false;
        state.users = state.users.filter(user => user.id !== action.payload);
        state.totalCount -= 1;
      })
      .addCase(deleteUser.rejected, (state, action) => {
        state.loading = false;
        state.error = action.payload;
      })
      // createUser 액션 처리
      .addCase(createUser.pending, (state) => {
        state.loading = true;
      })
      .addCase(createUser.fulfilled, (state, action) => {
        state.loading = false;
        state.users.push(action.payload);
        state.totalCount += 1;
      })
      .addCase(createUser.rejected, (state, action) => {
        state.loading = false;
        state.error = action.payload;
      });
  },
});

export const { clearError, setSelectedUser, clearSelectedUser, setCurrentPage } = usersSlice.actions;
export default usersSlice.reducer;
```

#### Store 설정
```jsx
// store/index.js
import { configureStore } from '@reduxjs/toolkit';
import usersReducer from './slices/usersSlice';
import authReducer from './slices/authSlice';

export const store = configureStore({
  reducer: {
    users: usersReducer,
    auth: authReducer,
  },
  middleware: (getDefaultMiddleware) =>
    getDefaultMiddleware({
      serializableCheck: {
        ignoredActions: ['persist/PERSIST', 'persist/REHYDRATE'],
      },
    }),
});

export default store;
```

### 4.3 API 서비스 예시

```jsx
// services/api.js
import axios from 'axios';

// Axios 인스턴스 생성
const apiClient = axios.create({
  baseURL: import.meta.env.VITE_API_BASE_URL || 'http://localhost:3000/api',
  timeout: 10000,
  headers: {
    'Content-Type': 'application/json',
  },
});

// 요청 인터셉터 (간단한 버전)
apiClient.interceptors.request.use(
  (config) => {
    const token = localStorage.getItem('accessToken');
    if (token) {
      config.headers.Authorization = `Bearer ${token}`;
    }
    return config;
  },
  (error) => {
    return Promise.reject(error);
  }
);

// 응답 인터셉터 (간단한 버전)
apiClient.interceptors.response.use(
  (response) => response,
  (error) => {
    if (error.response?.status === 401) {
      localStorage.removeItem('accessToken');
      window.location.href = '/login';
    }
    return Promise.reject(error);
  }
);

// API 서비스 객체들
export const usersAPI = {
  getUsers: () => apiClient.get('/users'),
  getUser: (id) => apiClient.get(`/users/${id}`),
  createUser: (userData) => apiClient.post('/users', userData),
  updateUser: (id, userData) => apiClient.put(`/users/${id}`, userData),
  deleteUser: (id) => apiClient.delete(`/users/${id}`),
};

export const authAPI = {
  login: (credentials) => apiClient.post('/auth/login', credentials),
  logout: () => apiClient.post('/auth/logout'),
  register: (userData) => apiClient.post('/auth/register', userData),
  refreshToken: () => apiClient.post('/auth/refresh'),
};

export default apiClient;
```

### 4.4 커스텀 훅 예시

```jsx
// hooks/useUsers.js
import { useDispatch, useSelector } from 'react-redux';
import { useEffect } from 'react';
import { fetchUsers, deleteUser, clearError } from '../store/slices/usersSlice';

export const useUsers = () => {
  const dispatch = useDispatch();
  const { users, loading, error, totalCount } = useSelector(state => state.users);

  const loadUsers = () => {
    dispatch(fetchUsers());
  };

  const removeUser = (userId) => {
    dispatch(deleteUser(userId));
  };

  const clearUserError = () => {
    dispatch(clearError());
  };

  return {
    users,
    loading,
    error,
    totalCount,
    loadUsers,
    removeUser,
    clearUserError,
  };
};
```

### 4.5 라우터 설정 예시

```jsx
// App.jsx
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
import { Provider } from 'react-redux';
import { store } from './store';
import Layout from './components/layout/Layout';
import UsersPage from './pages/UsersPage/UsersPage';
import UserDetailPage from './pages/UserDetailPage/UserDetailPage';
import LoginPage from './pages/LoginPage/LoginPage';

function App() {
  return (
    <Provider store={store}>
      <Router>
        <Routes>
          <Route path="/login" element={<LoginPage />} />
          <Route path="/" element={<Layout />}>
            <Route index element={<UsersPage />} />
            <Route path="users" element={<UsersPage />} />
            <Route path="users/:id" element={<UserDetailPage />} />
          </Route>
        </Routes>
      </Router>
    </Provider>
  );
}

export default App;
```

## 5. 추가 권장사항

### 5.1 성능 최적화
- `React.memo`를 사용하여 불필요한 리렌더링 방지
- `useCallback`과 `useMemo`를 적절히 활용
- 큰 리스트에는 가상화 라이브러리 사용 고려

### 5.2 에러 처리
- Error Boundary를 사용하여 컴포넌트 에러 처리
- try-catch를 사용하여 비동기 작업 에러 처리
- 사용자 친화적인 에러 메시지 제공

### 5.3 접근성
- 적절한 ARIA 속성 사용
- 키보드 네비게이션 지원
- 시맨틱 HTML 요소 사용

### 5.4 코드 품질
- ESLint와 Prettier를 사용한 코드 스타일 통일
- 컴포넌트별 PropTypes 정의
- 의미있는 변수명과 함수명 사용

이 가이드를 따라 개발하시면 유지보수하기 쉽고 확장 가능한 React 애플리케이션을 만들 수 있습니다.