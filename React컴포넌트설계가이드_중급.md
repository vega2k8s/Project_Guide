# React 컴포넌트 설계 가이드
*ReactJS + Vite + React Router + RTK 환경 최적화*

## 1. React 컴포넌트 설계 원칙

### 1.1 단일 책임 원칙 (Single Responsibility Principle)
- **하나의 컴포넌트는 하나의 역할만 담당**해야 합니다
- 컴포넌트가 너무 많은 기능을 담당하면 분리를 고려하세요
- UI 표시, 데이터 처리, 비즈니스 로직을 명확히 구분하세요

### 1.2 컴포넌트 분류 체계
**Presentational Components (프레젠테이션 컴포넌트)**
- UI 렌더링에만 집중
- props를 통해서만 데이터를 받음
- 상태 관리는 최소화
- 재사용성이 높음

**Container Components (컨테이너 컴포넌트)**
- 데이터 fetching과 상태 관리를 담당
- Redux store와 연결
- 비즈니스 로직 처리
- Presentational 컴포넌트에 데이터 전달

### 1.3 폴더 구조 원칙
```
src/
├── components/          # 재사용 가능한 UI 컴포넌트
│   ├── common/         # 공통 컴포넌트
│   └── ui/            # 기본 UI 컴포넌트 (Button, Input 등)
├── pages/             # 페이지 컴포넌트
├── containers/        # 컨테이너 컴포넌트
├── hooks/            # 커스텀 훅
├── store/            # Redux 스토어
└── utils/            # 유틸리티 함수
```

### 1.4 네이밍 컨벤션
- **컴포넌트명**: PascalCase 사용 (예: `UserProfile`, `ProductCard`)
- **파일명**: 컴포넌트명과 동일하게 PascalCase
- **props명**: camelCase 사용
- **이벤트 핸들러**: `handle` 접두어 사용 (예: `handleClick`, `handleSubmit`)

---

## 2. React 컴포넌트 Props 설계 원칙

### 2.1 Props 설계 기본 원칙
**명확하고 직관적인 이름 사용**
- props의 목적이 명확히 드러나는 이름을 선택하세요
- `data` 대신 `user`, `product` 같은 구체적인 이름 사용

**Props 개수 최소화**
- 5개 이하의 props를 권장합니다
- 너무 많은 props는 객체로 묶어서 전달하세요

**Props 기본값 설정**
- `defaultProps` 또는 ES6 기본 매개변수를 활용하세요
- 예상치 못한 undefined 오류를 방지합니다

### 2.2 Props 타입별 설계 가이드
**객체 Props**
- 관련된 데이터를 하나의 객체로 묶어 전달
- prop drilling을 줄일 수 있습니다

**함수 Props (콜백)**
- `on` 접두어 사용 (예: `onSubmit`, `onClick`)
- 부모 컴포넌트에서 자식의 상태 변화를 감지할 때 사용

**Boolean Props**
- `is`, `has`, `can` 접두어 사용 (예: `isVisible`, `hasError`)
- 기본값을 false로 설정하는 것을 권장

### 2.3 Props Validation
PropTypes를 사용하여 props의 타입을 검증하세요:
```bash
npm install prop-types
```

---

## 3. Redux(RTK) 상태 관리 설계 원칙

### 3.1 상태 설계 원칙
**정규화된 상태 구조**
- 중첩된 객체보다는 평면적인 구조를 선호
- ID를 키로 하는 객체 형태로 데이터 저장
- 배열보다는 객체 사용을 권장

**최소한의 상태 유지**
- 계산 가능한 값은 상태에 저장하지 않음
- 컴포넌트 로컬 상태와 글로벌 상태를 명확히 구분

### 3.2 Slice 설계 가이드
**기능별 Slice 분리**
- 각 도메인별로 별도의 slice 생성
- 사용자, 제품, 주문 등 논리적 단위로 분리

**Action과 Reducer 네이밍**
- Action: 동사형 사용 (예: `fetchUsers`, `updateUser`)
- Reducer: 현재 시제 사용 (예: `users`, `loading`)

### 3.3 비동기 처리 원칙
**createAsyncThunk 활용**
- API 호출은 createAsyncThunk로 처리
- pending, fulfilled, rejected 상태를 자동으로 관리
- 에러 처리를 일관성 있게 구현

**로딩 상태 관리**
- 각 API 호출별로 로딩 상태 분리
- 사용자 경험을 위한 적절한 로딩 UI 제공

---

## 4. Axios를 활용한 HTTP 통신 설계

### 4.1 API 모듈화 원칙
**기능별 API 파일 분리**
- 도메인별로 별도의 API 파일 생성
- 재사용 가능한 구조로 설계

**일관된 응답 처리**
- 성공/실패 응답을 일관되게 처리
- 에러 메시지를 사용자 친화적으로 변환

### 4.2 createAsyncThunk와 Axios 연동
**표준화된 API 호출 패턴**
- 모든 API 호출을 createAsyncThunk로 래핑
- try-catch를 사용한 에러 처리
- 적절한 에러 메시지 반환

---

## 5. React Router 라우팅 설계 원칙

### 5.1 라우팅 구조 설계
**계층적 라우팅**
- 중첩 라우팅을 활용한 레이아웃 구성
- 공통 레이아웃 컴포넌트 활용

**동적 라우팅**
- URL 파라미터를 활용한 동적 페이지
- Query Parameter를 통한 필터링

### 5.2 네비게이션 원칙
**프로그래밍 방식 네비게이션**
- `useNavigate` 훅 활용
- 조건부 리다이렉션 구현

**경로 보호**
- 인증이 필요한 라우트 보호
- 권한에 따른 접근 제어

---

## 6. 코드 예시

### 6.1 Presentational Component (상품 카드)

```jsx
// components/ui/ProductCard.jsx
import PropTypes from 'prop-types';
import './ProductCard.css';

const ProductCard = ({ 
  product, 
  onAddToCart, 
  onViewDetail, 
  isLoading = false 
}) => {
  const handleAddToCart = () => {
    onAddToCart(product.id);
  };

  const handleViewDetail = () => {
    onViewDetail(product.id);
  };

  if (isLoading) {
    return <div className="product-card loading">Loading...</div>;
  }

  return (
    <div className="product-card">
      <img 
        src={product.imageUrl} 
        alt={product.name}
        className="product-image"
      />
      <div className="product-info">
        <h3 className="product-name">{product.name}</h3>
        <p className="product-price">${product.price}</p>
        <p className="product-description">{product.description}</p>
        
        <div className="product-actions">
          <button 
            onClick={handleViewDetail}
            className="btn btn-secondary"
          >
            자세히 보기
          </button>
          <button 
            onClick={handleAddToCart}
            className="btn btn-primary"
            disabled={!product.inStock}
          >
            {product.inStock ? '장바구니 담기' : '품절'}
          </button>
        </div>
      </div>
    </div>
  );
};

ProductCard.propTypes = {
  product: PropTypes.shape({
    id: PropTypes.oneOfType([PropTypes.string, PropTypes.number]).isRequired,
    name: PropTypes.string.isRequired,
    price: PropTypes.number.isRequired,
    description: PropTypes.string,
    imageUrl: PropTypes.string.isRequired,
    inStock: PropTypes.bool.isRequired
  }).isRequired,
  onAddToCart: PropTypes.func.isRequired,
  onViewDetail: PropTypes.func.isRequired,
  isLoading: PropTypes.bool
};

export default ProductCard;
```

### 6.2 Redux Slice (상품 관리)

```jsx
// store/slices/productSlice.js
import { createSlice, createAsyncThunk } from '@reduxjs/toolkit';
import { productAPI } from '../api/productAPI';

// 비동기 액션: 상품 목록 조회
export const fetchProducts = createAsyncThunk(
  'products/fetchProducts',
  async (params, { rejectWithValue }) => {
    try {
      const response = await productAPI.getProducts(params);
      return response.data;
    } catch (error) {
      return rejectWithValue(
        error.response?.data?.message || '상품을 불러오는데 실패했습니다.'
      );
    }
  }
);

// 비동기 액션: 상품 상세 조회
export const fetchProductDetail = createAsyncThunk(
  'products/fetchProductDetail',
  async (productId, { rejectWithValue }) => {
    try {
      const response = await productAPI.getProductById(productId);
      return response.data;
    } catch (error) {
      return rejectWithValue(
        error.response?.data?.message || '상품 정보를 불러오는데 실패했습니다.'
      );
    }
  }
);

const initialState = {
  // 상품 목록
  products: [],
  totalCount: 0,
  
  // 현재 선택된 상품
  selectedProduct: null,
  
  // 로딩 상태
  loading: {
    products: false,
    productDetail: false
  },
  
  // 에러 상태
  error: {
    products: null,
    productDetail: null
  },
  
  // 필터 및 페이지네이션
  filters: {
    category: '',
    minPrice: 0,
    maxPrice: 1000,
    searchKeyword: ''
  },
  pagination: {
    page: 1,
    limit: 12
  }
};

const productSlice = createSlice({
  name: 'products',
  initialState,
  reducers: {
    // 필터 설정
    setFilters: (state, action) => {
      state.filters = { ...state.filters, ...action.payload };
      state.pagination.page = 1; // 필터 변경 시 첫 페이지로 이동
    },
    
    // 페이지 변경
    setPage: (state, action) => {
      state.pagination.page = action.payload;
    },
    
    // 에러 초기화
    clearError: (state, action) => {
      const errorType = action.payload;
      if (errorType) {
        state.error[errorType] = null;
      } else {
        state.error = { products: null, productDetail: null };
      }
    },
    
    // 선택된 상품 초기화
    clearSelectedProduct: (state) => {
      state.selectedProduct = null;
      state.error.productDetail = null;
    }
  },
  extraReducers: (builder) => {
    builder
      // 상품 목록 조회
      .addCase(fetchProducts.pending, (state) => {
        state.loading.products = true;
        state.error.products = null;
      })
      .addCase(fetchProducts.fulfilled, (state, action) => {
        state.loading.products = false;
        state.products = action.payload.products;
        state.totalCount = action.payload.totalCount;
      })
      .addCase(fetchProducts.rejected, (state, action) => {
        state.loading.products = false;
        state.error.products = action.payload;
      })
      
      // 상품 상세 조회
      .addCase(fetchProductDetail.pending, (state) => {
        state.loading.productDetail = true;
        state.error.productDetail = null;
      })
      .addCase(fetchProductDetail.fulfilled, (state, action) => {
        state.loading.productDetail = false;
        state.selectedProduct = action.payload;
      })
      .addCase(fetchProductDetail.rejected, (state, action) => {
        state.loading.productDetail = false;
        state.error.productDetail = action.payload;
      });
  }
});

export const { 
  setFilters, 
  setPage, 
  clearError, 
  clearSelectedProduct 
} = productSlice.actions;

export default productSlice.reducer;
```

### 6.3 API 모듈

```jsx
// api/productAPI.js
import axios from 'axios';

const BASE_URL = import.meta.env.VITE_API_BASE_URL || 'http://localhost:3001/api';

const productAPI = {
  // 상품 목록 조회
  getProducts: async (params = {}) => {
    const queryParams = new URLSearchParams();
    
    if (params.category) queryParams.append('category', params.category);
    if (params.minPrice) queryParams.append('minPrice', params.minPrice);
    if (params.maxPrice) queryParams.append('maxPrice', params.maxPrice);
    if (params.searchKeyword) queryParams.append('search', params.searchKeyword);
    if (params.page) queryParams.append('page', params.page);
    if (params.limit) queryParams.append('limit', params.limit);
    
    const url = `${BASE_URL}/products${queryParams.toString() ? '?' + queryParams.toString() : ''}`;
    return await axios.get(url);
  },
  
  // 상품 상세 조회
  getProductById: async (productId) => {
    return await axios.get(`${BASE_URL}/products/${productId}`);
  },
  
  // 상품 생성 (관리자용)
  createProduct: async (productData) => {
    return await axios.post(`${BASE_URL}/products`, productData);
  },
  
  // 상품 수정 (관리자용)
  updateProduct: async (productId, productData) => {
    return await axios.put(`${BASE_URL}/products/${productId}`, productData);
  },
  
  // 상품 삭제 (관리자용)
  deleteProduct: async (productId) => {
    return await axios.delete(`${BASE_URL}/products/${productId}`);
  }
};

export { productAPI };
```

### 6.4 Container Component (상품 목록 페이지)

```jsx
// pages/ProductListPage.jsx
import { useEffect } from 'react';
import { useDispatch, useSelector } from 'react-redux';
import { useNavigate, useSearchParams } from 'react-router-dom';
import ProductCard from '../components/ui/ProductCard';
import ProductFilter from '../components/ProductFilter';
import Pagination from '../components/ui/Pagination';
import LoadingSpinner from '../components/ui/LoadingSpinner';
import ErrorMessage from '../components/ui/ErrorMessage';
import { 
  fetchProducts, 
  setFilters, 
  setPage, 
  clearError 
} from '../store/slices/productSlice';

const ProductListPage = () => {
  const dispatch = useDispatch();
  const navigate = useNavigate();
  const [searchParams, setSearchParams] = useSearchParams();
  
  const {
    products,
    totalCount,
    loading,
    error,
    filters,
    pagination
  } = useSelector(state => state.products);

  // URL 파라미터와 Redux 상태 동기화
  useEffect(() => {
    const urlFilters = {
      category: searchParams.get('category') || '',
      searchKeyword: searchParams.get('search') || '',
      minPrice: parseInt(searchParams.get('minPrice')) || 0,
      maxPrice: parseInt(searchParams.get('maxPrice')) || 1000
    };
    
    const urlPage = parseInt(searchParams.get('page')) || 1;
    
    // URL 파라미터가 Redux 상태와 다르면 Redux 상태 업데이트
    if (JSON.stringify(urlFilters) !== JSON.stringify(filters)) {
      dispatch(setFilters(urlFilters));
    }
    
    if (urlPage !== pagination.page) {
      dispatch(setPage(urlPage));
    }
  }, [searchParams, dispatch, filters, pagination.page]);

  // 상품 데이터 로드
  useEffect(() => {
    const fetchParams = {
      ...filters,
      page: pagination.page,
      limit: pagination.limit
    };
    
    dispatch(fetchProducts(fetchParams));
  }, [dispatch, filters, pagination]);

  // 필터 변경 핸들러
  const handleFilterChange = (newFilters) => {
    dispatch(setFilters(newFilters));
    
    // URL 파라미터 업데이트
    const newSearchParams = new URLSearchParams();
    Object.entries({ ...filters, ...newFilters }).forEach(([key, value]) => {
      if (value) {
        newSearchParams.set(key, value);
      }
    });
    setSearchParams(newSearchParams);
  };

  // 페이지 변경 핸들러
  const handlePageChange = (newPage) => {
    dispatch(setPage(newPage));
    
    const newSearchParams = new URLSearchParams(searchParams);
    newSearchParams.set('page', newPage);
    setSearchParams(newSearchParams);
    
    // 페이지 변경 시 상단으로 스크롤
    window.scrollTo({ top: 0, behavior: 'smooth' });
  };

  // 장바구니 추가 핸들러
  const handleAddToCart = (productId) => {
    // 실제로는 장바구니 관련 액션을 dispatch
    console.log('장바구니에 추가:', productId);
    // dispatch(addToCart(productId));
  };

  // 상품 상세 보기 핸들러
  const handleViewDetail = (productId) => {
    navigate(`/products/${productId}`);
  };

  // 에러 처리 핸들러
  const handleRetry = () => {
    dispatch(clearError('products'));
    dispatch(fetchProducts({
      ...filters,
      page: pagination.page,
      limit: pagination.limit
    }));
  };

  // 로딩 상태
  if (loading.products && products.length === 0) {
    return <LoadingSpinner message="상품을 불러오는 중..." />;
  }

  // 에러 상태
  if (error.products) {
    return (
      <ErrorMessage 
        message={error.products}
        onRetry={handleRetry}
      />
    );
  }

  return (
    <div className="product-list-page">
      <div className="container">
        <h1 className="page-title">상품 목록</h1>
        
        {/* 필터 섹션 */}
        <ProductFilter 
          filters={filters}
          onFilterChange={handleFilterChange}
        />
        
        {/* 상품 개수 정보 */}
        <div className="product-count">
          총 {totalCount}개의 상품이 있습니다.
        </div>
        
        {/* 상품 목록 */}
        <div className="product-grid">
          {products.map(product => (
            <ProductCard
              key={product.id}
              product={product}
              onAddToCart={handleAddToCart}
              onViewDetail={handleViewDetail}
              isLoading={loading.products}
            />
          ))}
        </div>
        
        {/* 상품이 없는 경우 */}
        {products.length === 0 && !loading.products && (
          <div className="no-products">
            <p>조건에 맞는 상품이 없습니다.</p>
          </div>
        )}
        
        {/* 페이지네이션 */}
        {totalCount > pagination.limit && (
          <Pagination
            currentPage={pagination.page}
            totalCount={totalCount}
            pageSize={pagination.limit}
            onPageChange={handlePageChange}
          />
        )}
      </div>
    </div>
  );
};

export default ProductListPage;
```

### 6.5 라우터 설정

```jsx
// App.jsx
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
import { Provider } from 'react-redux';
import { store } from './store/store';
import Layout from './components/Layout';
import HomePage from './pages/HomePage';
import ProductListPage from './pages/ProductListPage';
import ProductDetailPage from './pages/ProductDetailPage';
import CartPage from './pages/CartPage';
import NotFoundPage from './pages/NotFoundPage';

function App() {
  return (
    <Provider store={store}>
      <Router>
        <Routes>
          <Route path="/" element={<Layout />}>
            <Route index element={<HomePage />} />
            <Route path="products" element={<ProductListPage />} />
            <Route path="products/:productId" element={<ProductDetailPage />} />
            <Route path="cart" element={<CartPage />} />
            <Route path="*" element={<NotFoundPage />} />
          </Route>
        </Routes>
      </Router>
    </Provider>
  );
}

export default App;
```

### 6.6 커스텀 훅 예시

```jsx
// hooks/useProducts.js
import { useEffect, useState } from 'react';
import { useDispatch, useSelector } from 'react-redux';
import { fetchProducts, setFilters, setPage } from '../store/slices/productSlice';

const useProducts = (initialFilters = {}) => {
  const dispatch = useDispatch();
  const productState = useSelector(state => state.products);
  const [isInitialized, setIsInitialized] = useState(false);

  // 초기 필터 설정
  useEffect(() => {
    if (!isInitialized && Object.keys(initialFilters).length > 0) {
      dispatch(setFilters(initialFilters));
      setIsInitialized(true);
    }
  }, [dispatch, initialFilters, isInitialized]);

  // 상품 데이터 로드
  const loadProducts = (params = {}) => {
    const fetchParams = {
      ...productState.filters,
      ...params,
      page: productState.pagination.page,
      limit: productState.pagination.limit
    };
    
    dispatch(fetchProducts(fetchParams));
  };

  // 필터 변경
  const updateFilters = (newFilters) => {
    dispatch(setFilters(newFilters));
  };

  // 페이지 변경
  const changePage = (page) => {
    dispatch(setPage(page));
  };

  return {
    ...productState,
    loadProducts,
    updateFilters,
    changePage
  };
};

export default useProducts;
```

---

## 추가 권장사항

### 성능 최적화
- React.memo를 활용한 불필요한 리렌더링 방지
- useCallback과 useMemo를 적절히 활용
- 큰 리스트는 가상화(virtualization) 고려

### 코드 품질
- ESLint와 Prettier 설정으로 일관된 코드 스타일 유지
- PropTypes를 통한 타입 검증
- 의미있는 컴포넌트명과 변수명 사용

### 사용자 경험
- 로딩 상태와 에러 상태를 명확히 표시
- 적절한 피드백과 알림 제공
- 접근성(Accessibility) 고려한 마크업
