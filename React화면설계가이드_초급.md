# React 화면 설계서 가이드
*ReactJS + Vite + React Router + RTK 환경 최적화*

## 1. 권장 UI 라이브러리 비교 및 선택 가이드

### 1.1 주요 UI 라이브러리 비교

| 특징 | Material-UI (MUI) | Chakra UI | Ant Design |
|------|-------------------|-----------|------------|
| **학습 곡선** | 보통 | 쉬움 | 보통 |
| **디자인 철학** | Google Material Design | 단순함과 모듈성 | 엔터프라이즈 UI |
| **번들 크기** | 큼 | 작음 | 큼 |
| **커스터마이징** | 복잡하지만 강력함 | 매우 쉬움 | 보통 |
| **TypeScript 지원** | 훌륭함 | 훌륭함 | 좋음 |
| **문서화** | 매우 좋음 | 매우 좋음 | 좋음 |
| **생태계** | 매우 큼 | 중간 | 큼 |

### 1.2 초보자에게 권장하는 UI 라이브러리: **Chakra UI**

**선택 이유:**
- **간단한 API**: 직관적이고 배우기 쉬운 prop 기반 스타일링
- **빠른 개발**: 최소한의 설정으로 바로 사용 가능
- **좋은 기본값**: 접근성과 반응형을 기본으로 지원
- **작은 번들 크기**: 필요한 컴포넌트만 import 가능
- **훌륭한 문서**: 명확하고 이해하기 쉬운 예제

**설치 방법:**
```bash
npm install @chakra-ui/react @emotion/react @emotion/styled framer-motion
```

---

## 2. 화면 설계 방법론

### 2.1 화면 설계 단계
1. **와이어프레임 설계** - 레이아웃과 구조 정의
2. **컴포넌트 분해** - UI를 재사용 가능한 컴포넌트로 분리
3. **상태 설계** - 데이터 흐름과 상태 관리 계획
4. **라우팅 설계** - 페이지 간 네비게이션 구조
5. **반응형 설계** - 다양한 화면 크기 대응

### 2.2 컴포넌트 계층 구조 설계 원칙
```
Page (페이지)
├── Layout (레이아웃)
│   ├── Header (헤더)
│   ├── Sidebar (사이드바)
│   └── Footer (푸터)
├── Container (컨테이너)
│   ├── List (목록)
│   │   └── Item (아이템)
│   └── Form (폼)
│       ├── Input (입력)
│       └── Button (버튼)
└── Modal (모달)
```

---

## 3. Chakra UI 기반 화면 설계 패턴

### 3.1 기본 레이아웃 패턴

**App Shell 패턴**
- Header, Sidebar, Main Content, Footer로 구성
- 일관된 네비게이션과 브랜딩 제공

**Grid 시스템**
- Chakra UI의 Grid와 SimpleGrid 활용
- 반응형 레이아웃 자동 지원

**Container 패턴**
- 콘텐츠의 최대 너비 제한
- 중앙 정렬과 패딩 자동 적용

### 3.2 컴포넌트 디자인 패턴

**Card 패턴**
- 관련 정보를 그룹화
- 시각적 계층 구조 제공

**Form 패턴**
- 입력 검증과 피드백
- 사용자 친화적인 오류 처리

**Table 패턴**
- 데이터 표시와 정렬
- 페이지네이션 및 필터링

---

## 4. 화면별 설계 가이드

### 4.1 메인 페이지 (HomePage)
**목적**: 서비스 소개 및 주요 기능 안내
**구성 요소:**
- Hero Section (큰 제목과 CTA)
- Feature Section (주요 기능 소개)
- Testimonial Section (고객 후기)
- CTA Section (행동 유도)

### 4.2 목록 페이지 (ListPage)
**목적**: 데이터 목록 표시 및 탐색
**구성 요소:**
- 검색 및 필터
- 정렬 옵션
- 페이지네이션
- 로딩 및 빈 상태

### 4.3 상세 페이지 (DetailPage)
**목적**: 개별 아이템의 상세 정보 표시
**구성 요소:**
- 상세 정보 표시
- 관련 액션 버튼
- 브레드크럼 네비게이션
- 관련 아이템 추천

### 4.4 폼 페이지 (FormPage)
**목적**: 데이터 입력 및 수정
**구성 요소:**
- 입력 필드와 검증
- 진행 상태 표시
- 저장/취소 액션
- 오류 처리

---

## 5. 실제 화면 설계 예시

### 5.1 애플리케이션 전체 구조

```jsx
// App.jsx - 메인 애플리케이션 구조
import { ChakraProvider } from '@chakra-ui/react';
import { BrowserRouter as Router } from 'react-router-dom';
import { Provider } from 'react-redux';
import { store } from './store/store';
import theme from './theme/theme';
import AppRouter from './router/AppRouter';

function App() {
  return (
    <Provider store={store}>
      <ChakraProvider theme={theme}>
        <Router>
          <AppRouter />
        </Router>
      </ChakraProvider>
    </Provider>
  );
}

export default App;
```

### 5.2 커스텀 테마 설정

```jsx
// theme/theme.js - Chakra UI 테마 커스터마이징
import { extendTheme } from '@chakra-ui/react';

const theme = extendTheme({
  // 색상 팔레트
  colors: {
    primary: {
      50: '#e3f2fd',
      100: '#bbdefb',
      500: '#2196f3',
      600: '#1976d2',
      700: '#1565c0',
    },
    secondary: {
      50: '#fce4ec',
      100: '#f8bbd9',
      500: '#e91e63',
      600: '#d81b60',
      700: '#c2185b',
    },
  },
  
  // 폰트 설정
  fonts: {
    heading: '"Noto Sans KR", sans-serif',
    body: '"Noto Sans KR", sans-serif',
  },
  
  // 기본 스타일
  styles: {
    global: {
      body: {
        bg: 'gray.50',
        color: 'gray.800',
      },
    },
  },
  
  // 컴포넌트 기본 스타일
  components: {
    Button: {
      defaultProps: {
        colorScheme: 'primary',
      },
      variants: {
        solid: {
          borderRadius: 'md',
          fontWeight: 'medium',
        },
      },
    },
    Card: {
      baseStyle: {
        container: {
          borderRadius: 'lg',
          boxShadow: 'sm',
          _hover: {
            boxShadow: 'md',
          },
        },
      },
    },
  },
});

export default theme;
```

### 5.3 공통 레이아웃 컴포넌트

```jsx
// components/layout/AppLayout.jsx
import {
  Box,
  Flex,
  Container,
  useColorModeValue,
} from '@chakra-ui/react';
import { Outlet } from 'react-router-dom';
import Header from './Header';
import Sidebar from './Sidebar';
import Footer from './Footer';

const AppLayout = () => {
  const bgColor = useColorModeValue('gray.50', 'gray.900');
  
  return (
    <Box minH="100vh" bg={bgColor}>
      {/* 헤더 */}
      <Header />
      
      <Flex>
        {/* 사이드바 (선택적) */}
        <Sidebar />
        
        {/* 메인 콘텐츠 */}
        <Box flex="1">
          <Container maxW="container.xl" py={8}>
            <Outlet />
          </Container>
        </Box>
      </Flex>
      
      {/* 푸터 */}
      <Footer />
    </Box>
  );
};

export default AppLayout;
```

### 5.4 헤더 컴포넌트

```jsx
// components/layout/Header.jsx
import {
  Box,
  Flex,
  Heading,
  Button,
  Menu,
  MenuButton,
  MenuList,
  MenuItem,
  Avatar,
  HStack,
  useColorModeValue,
  useDisclosure,
} from '@chakra-ui/react';
import { Link as RouterLink, useNavigate } from 'react-router-dom';
import { useSelector, useDispatch } from 'react-redux';
import { ChevronDownIcon, HamburgerIcon } from '@chakra-ui/icons';
import { logout } from '../store/slices/authSlice';
import MobileNav from './MobileNav';

const Header = () => {
  const navigate = useNavigate();
  const dispatch = useDispatch();
  const { isOpen, onOpen, onClose } = useDisclosure();
  
  const { user, isAuthenticated } = useSelector(state => state.auth);
  
  const bg = useColorModeValue('white', 'gray.800');
  const borderColor = useColorModeValue('gray.200', 'gray.700');

  const handleLogout = () => {
    dispatch(logout());
    navigate('/');
  };

  return (
    <>
      <Box
        bg={bg}
        borderBottom="1px"
        borderColor={borderColor}
        position="sticky"
        top={0}
        zIndex={1000}
      >
        <Container maxW="container.xl">
          <Flex h={16} alignItems="center" justifyContent="space-between">
            {/* 로고 */}
            <Heading
              as={RouterLink}
              to="/"
              size="lg"
              color="primary.600"
              _hover={{ textDecoration: 'none' }}
            >
              MyApp
            </Heading>

            {/* 데스크톱 네비게이션 */}
            <HStack spacing={8} display={{ base: 'none', md: 'flex' }}>
              <Button
                as={RouterLink}
                to="/products"
                variant="ghost"
                colorScheme="gray"
              >
                상품
              </Button>
              <Button
                as={RouterLink}
                to="/about"
                variant="ghost"
                colorScheme="gray"
              >
                소개
              </Button>
              <Button
                as={RouterLink}
                to="/contact"
                variant="ghost"
                colorScheme="gray"
              >
                연락처
              </Button>
            </HStack>

            {/* 사용자 메뉴 */}
            <Flex alignItems="center">
              {isAuthenticated ? (
                <Menu>
                  <MenuButton
                    as={Button}
                    variant="ghost"
                    rightIcon={<ChevronDownIcon />}
                  >
                    <HStack>
                      <Avatar size="sm" name={user?.name} src={user?.avatar} />
                      <Box display={{ base: 'none', md: 'block' }}>
                        {user?.name}
                      </Box>
                    </HStack>
                  </MenuButton>
                  <MenuList>
                    <MenuItem as={RouterLink} to="/profile">
                      프로필
                    </MenuItem>
                    <MenuItem as={RouterLink} to="/settings">
                      설정
                    </MenuItem>
                    <MenuItem onClick={handleLogout}>
                      로그아웃
                    </MenuItem>
                  </MenuList>
                </Menu>
              ) : (
                <HStack>
                  <Button
                    as={RouterLink}
                    to="/login"
                    variant="ghost"
                    size="sm"
                  >
                    로그인
                  </Button>
                  <Button
                    as={RouterLink}
                    to="/register"
                    colorScheme="primary"
                    size="sm"
                  >
                    회원가입
                  </Button>
                </HStack>
              )}

              {/* 모바일 메뉴 버튼 */}
              <Button
                display={{ base: 'flex', md: 'none' }}
                onClick={onOpen}
                variant="ghost"
                ml={2}
              >
                <HamburgerIcon />
              </Button>
            </Flex>
          </Flex>
        </Container>
      </Box>

      {/* 모바일 네비게이션 */}
      <MobileNav isOpen={isOpen} onClose={onClose} />
    </>
  );
};

export default Header;
```

### 5.5 상품 목록 페이지

```jsx
// pages/ProductListPage.jsx
import {
  Box,
  Container,
  Heading,
  SimpleGrid,
  Text,
  Button,
  HStack,
  VStack,
  Input,
  Select,
  Card,
  CardBody,
  CardFooter,
  Image,
  Badge,
  Skeleton,
  Alert,
  AlertIcon,
  Flex,
  Spacer,
} from '@chakra-ui/react';
import { useState, useEffect } from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { SearchIcon } from '@chakra-ui/icons';
import { 
  fetchProducts, 
  setFilters, 
  setPage 
} from '../store/slices/productSlice';
import ProductCard from '../components/ProductCard';
import Pagination from '../components/Pagination';
import ProductFilter from '../components/ProductFilter';

const ProductListPage = () => {
  const dispatch = useDispatch();
  const {
    products,
    loading,
    error,
    totalCount,
    filters,
    pagination
  } = useSelector(state => state.products);

  const [searchTerm, setSearchTerm] = useState('');
  const [sortBy, setSortBy] = useState('name');

  // 초기 데이터 로드
  useEffect(() => {
    dispatch(fetchProducts({
      ...filters,
      page: pagination.page,
      limit: pagination.limit
    }));
  }, [dispatch, filters, pagination]);

  // 검색 핸들러
  const handleSearch = () => {
    dispatch(setFilters({ ...filters, searchKeyword: searchTerm }));
    dispatch(setPage(1));
  };

  // 정렬 변경 핸들러
  const handleSortChange = (value) => {
    setSortBy(value);
    dispatch(setFilters({ ...filters, sortBy: value }));
  };

  // 페이지 변경 핸들러
  const handlePageChange = (page) => {
    dispatch(setPage(page));
    window.scrollTo({ top: 0, behavior: 'smooth' });
  };

  return (
    <Container maxW="container.xl" py={8}>
      <VStack spacing={8} align="stretch">
        {/* 페이지 헤더 */}
        <Box>
          <Heading size="xl" mb={2}>상품 목록</Heading>
          <Text color="gray.600">
            다양한 상품을 둘러보고 마음에 드는 것을 찾아보세요.
          </Text>
        </Box>

        {/* 검색 및 필터 */}
        <Card>
          <CardBody>
            <VStack spacing={4}>
              {/* 검색바 */}
              <HStack w="full">
                <Input
                  placeholder="상품명을 검색하세요"
                  value={searchTerm}
                  onChange={(e) => setSearchTerm(e.target.value)}
                  onKeyPress={(e) => e.key === 'Enter' && handleSearch()}
                />
                <Button
                  leftIcon={<SearchIcon />}
                  colorScheme="primary"
                  onClick={handleSearch}
                >
                  검색
                </Button>
              </HStack>

              {/* 필터 및 정렬 */}
              <Flex w="full" gap={4} flexWrap="wrap">
                <Select
                  value={sortBy}
                  onChange={(e) => handleSortChange(e.target.value)}
                  maxW="200px"
                >
                  <option value="name">이름순</option>
                  <option value="price_asc">가격 낮은순</option>
                  <option value="price_desc">가격 높은순</option>
                  <option value="created_at">최신순</option>
                </Select>
                
                <ProductFilter
                  filters={filters}
                  onFilterChange={(newFilters) => dispatch(setFilters(newFilters))}
                />
                
                <Spacer />
                
                <Text alignSelf="center" fontSize="sm" color="gray.600">
                  총 {totalCount}개 상품
                </Text>
              </Flex>
            </VStack>
          </CardBody>
        </Card>

        {/* 에러 상태 */}
        {error && (
          <Alert status="error">
            <AlertIcon />
            {error}
          </Alert>
        )}

        {/* 상품 목록 */}
        <Box>
          {loading.products ? (
            <SimpleGrid columns={{ base: 1, md: 2, lg: 3, xl: 4 }} spacing={6}>
              {[...Array(8)].map((_, index) => (
                <Card key={index}>
                  <Skeleton height="200px" />
                  <CardBody>
                    <Skeleton height="20px" mb={2} />
                    <Skeleton height="20px" width="60%" />
                  </CardBody>
                </Card>
              ))}
            </SimpleGrid>
          ) : products.length > 0 ? (
            <SimpleGrid columns={{ base: 1, md: 2, lg: 3, xl: 4 }} spacing={6}>
              {products.map(product => (
                <ProductCard
                  key={product.id}
                  product={product}
                />
              ))}
            </SimpleGrid>
          ) : (
            <Card>
              <CardBody textAlign="center" py={12}>
                <Text fontSize="lg" color="gray.500">
                  조건에 맞는 상품이 없습니다.
                </Text>
                <Button
                  mt={4}
                  variant="outline"
                  onClick={() => {
                    setSearchTerm('');
                    dispatch(setFilters({}));
                  }}
                >
                  필터 초기화
                </Button>
              </CardBody>
            </Card>
          )}
        </Box>

        {/* 페이지네이션 */}
        {totalCount > pagination.limit && (
          <Pagination
            currentPage={pagination.page}
            totalCount={totalCount}
            pageSize={pagination.limit}
            onPageChange={handlePageChange}
          />
        )}
      </VStack>
    </Container>
  );
};

export default ProductListPage;
```

### 5.6 상품 카드 컴포넌트

```jsx
// components/ProductCard.jsx
import {
  Card,
  CardBody,
  CardFooter,
  Image,
  Text,
  Button,
  HStack,
  VStack,
  Badge,
  IconButton,
  useColorModeValue,
  useToast,
} from '@chakra-ui/react';
import { StarIcon, HeartIcon } from '@chakra-ui/icons';
import { Link as RouterLink } from 'react-router-dom';
import { useDispatch } from 'react-redux';
import { addToCart } from '../store/slices/cartSlice';
import { addToWishlist } from '../store/slices/wishlistSlice';

const ProductCard = ({ product }) => {
  const dispatch = useDispatch();
  const toast = useToast();
  
  const cardBg = useColorModeValue('white', 'gray.800');
  const textColor = useColorModeValue('gray.600', 'gray.300');

  const handleAddToCart = (e) => {
    e.preventDefault(); // Link 이벤트 방지
    dispatch(addToCart(product));
    toast({
      title: '장바구니에 추가되었습니다',
      status: 'success',
      duration: 2000,
      isClosable: true,
    });
  };

  const handleAddToWishlist = (e) => {
    e.preventDefault(); // Link 이벤트 방지
    dispatch(addToWishlist(product));
    toast({
      title: '위시리스트에 추가되었습니다',
      status: 'info',
      duration: 2000,
      isClosable: true,
    });
  };

  return (
    <Card
      as={RouterLink}
      to={`/products/${product.id}`}
      bg={cardBg}
      shadow="sm"
      _hover={{
        shadow: 'md',
        transform: 'translateY(-2px)',
      }}
      transition="all 0.2s"
      position="relative"
    >
      {/* 위시리스트 버튼 */}
      <IconButton
        icon={<HeartIcon />}
        size="sm"
        position="absolute"
        top={2}
        right={2}
        zIndex={1}
        bg="white"
        _hover={{ bg: 'red.50', color: 'red.500' }}
        onClick={handleAddToWishlist}
      />

      {/* 상품 이미지 */}
      <Image
        src={product.imageUrl}
        alt={product.name}
        height="200px"
        width="100%"
        objectFit="cover"
        borderTopRadius="md"
      />

      {/* 할인 배지 */}
      {product.discount && (
        <Badge
          colorScheme="red"
          position="absolute"
          top={2}
          left={2}
          fontSize="xs"
        >
          {product.discount}% OFF
        </Badge>
      )}

      <CardBody>
        <VStack align="start" spacing={2}>
          {/* 상품명 */}
          <Text
            fontWeight="semibold"
            fontSize="md"
            noOfLines={2}
            lineHeight="1.2"
          >
            {product.name}
          </Text>

          {/* 평점 */}
          <HStack spacing={1}>
            {[...Array(5)].map((_, i) => (
              <StarIcon
                key={i}
                color={i < product.rating ? 'yellow.400' : 'gray.300'}
                boxSize={3}
              />
            ))}
            <Text fontSize="sm" color={textColor}>
              ({product.reviewCount})
            </Text>
          </HStack>

          {/* 가격 */}
          <HStack>
            {product.originalPrice && (
              <Text
                fontSize="sm"
                textDecoration="line-through"
                color="gray.400"
              >
                ₩{product.originalPrice.toLocaleString()}
              </Text>
            )}
            <Text fontSize="lg" fontWeight="bold" color="primary.600">
              ₩{product.price.toLocaleString()}
            </Text>
          </HStack>

          {/* 재고 상태 */}
          <Badge
            colorScheme={product.inStock ? 'green' : 'red'}
            variant="subtle"
            fontSize="xs"
          >
            {product.inStock ? '재고 있음' : '품절'}
          </Badge>
        </VStack>
      </CardBody>

      <CardFooter pt={0}>
        <Button
          colorScheme="primary"
          size="sm"
          width="100%"
          isDisabled={!product.inStock}
          onClick={handleAddToCart}
        >
          {product.inStock ? '장바구니 담기' : '품절'}
        </Button>
      </CardFooter>
    </Card>
  );
};

export default ProductCard;
```

### 5.7 로그인 폼 페이지

```jsx
// pages/LoginPage.jsx
import {
  Box,
  Container,
  Card,
  CardBody,
  Heading,
  Text,
  VStack,
  HStack,
  FormControl,
  FormLabel,
  Input,
  Button,
  Checkbox,
  Divider,
  Alert,
  AlertIcon,
  Link,
  useColorModeValue,
  useToast,
} from '@chakra-ui/react';
import { useState } from 'react';
import { Link as RouterLink, useNavigate } from 'react-router-dom';
import { useDispatch, useSelector } from 'react-redux';
import { login } from '../store/slices/authSlice';

const LoginPage = () => {
  const navigate = useNavigate();
  const dispatch = useDispatch();
  const toast = useToast();
  
  const { loading, error } = useSelector(state => state.auth);
  
  const [formData, setFormData] = useState({
    email: '',
    password: '',
    rememberMe: false,
  });
  
  const [errors, setErrors] = useState({});
  
  const cardBg = useColorModeValue('white', 'gray.800');

  // 입력값 변경 핸들러
  const handleChange = (e) => {
    const { name, value, type, checked } = e.target;
    setFormData(prev => ({
      ...prev,
      [name]: type === 'checkbox' ? checked : value
    }));
    
    // 에러 초기화
    if (errors[name]) {
      setErrors(prev => ({ ...prev, [name]: '' }));
    }
  };

  // 폼 검증
  const validateForm = () => {
    const newErrors = {};
    
    if (!formData.email) {
      newErrors.email = '이메일을 입력해주세요';
    } else if (!/\S+@\S+\.\S+/.test(formData.email)) {
      newErrors.email = '올바른 이메일 형식이 아닙니다';
    }
    
    if (!formData.password) {
      newErrors.password = '비밀번호를 입력해주세요';
    } else if (formData.password.length < 6) {
      newErrors.password = '비밀번호는 6자 이상이어야 합니다';
    }
    
    setErrors(newErrors);
    return Object.keys(newErrors).length === 0;
  };

  // 로그인 처리
  const handleSubmit = async (e) => {
    e.preventDefault();
    
    if (!validateForm()) return;
    
    try {
      const result = await dispatch(login({
        email: formData.email,
        password: formData.password,
      })).unwrap();
      
      toast({
        title: '로그인 성공',
        description: `환영합니다, ${result.user.name}님!`,
        status: 'success',
        duration: 3000,
        isClosable: true,
      });
      
      navigate('/');
    } catch (error) {
      // 에러는 Redux에서 처리됨
    }
  };

  return (
    <Container maxW="md" py={12}>
      <VStack spacing={8}>
        {/* 헤더 */}
        <VStack spacing={2} textAlign="center">
          <Heading size="xl">로그인</Heading>
          <Text color="gray.600">
            계정에 로그인하여 더 많은 기능을 이용하세요
          </Text>
        </VStack>

        {/* 로그인 폼 */}
        <Card bg={cardBg} shadow="lg" w="100%">
          <CardBody p={8}>
            <form onSubmit={handleSubmit}>
              <VStack spacing={6}>
                {/* 서버 에러 메시지 */}
                {error && (
                  <Alert status="error" borderRadius="md">
                    <AlertIcon />
                    {error}
                  </Alert>
                )}

                {/* 이메일 입력 */}
                <FormControl isInvalid={errors.email} isRequired>
                  <FormLabel>이메일</FormLabel>
                  <Input
                    name="email"
                    type="email"
                    value={formData.email}
                    onChange={handleChange}
                    placeholder="your@email.com"
                    size="lg"
                  />
                  {errors.email && (
                    <Text color="red.500" fontSize="sm" mt={1}>
                      {errors.email}
                    </Text>
                  )}
                </FormControl>

                {/* 비밀번호 입력 */}
                <FormControl isInvalid={errors.password} isRequired>
                  <FormLabel>비밀번호</FormLabel>
                  <Input
                    name="password"
                    type="password"
                    value={formData.password}
                    onChange={handleChange}
                    placeholder="비밀번호를 입력하세요"
                    size="lg"
                  />
                  {errors.password && (
                    <Text color="red.500" fontSize="sm" mt={1}>
                      {errors.password}
                    </Text>
                  )}
                </FormControl>

                {/* 로그인 유지 및 비밀번호 찾기 */}
                <HStack w="100%" justify="space-between">
                  <Checkbox
                    name="rememberMe"
                    isChecked={formData.rememberMe}
                    onChange={handleChange}
                    colorScheme="primary"
                  >
                    로그인 상태 유지
                  </Checkbox>
                  <Link
                    as={RouterLink}
                    to="/forgot-password"
                    color="primary.600"
                    fontSize="sm"
                    _hover={{ textDecoration: 'underline' }}
                  >
                    비밀번호 찾기
                  </Link>
                </HStack>

                {/* 로그인 버튼 */}
                <Button
                  type="submit"
                  colorScheme="primary"
                  size="lg"
                  width="100%"
                  isLoading={loading.login}
                  loadingText="로그인 중..."
                >
                  로그인
                </Button>

                {/* 구분선 */}
                <HStack w="100%">
                  <Divider />
                  <Text fontSize="sm" color="gray.500" whiteSpace="nowrap">
                    또는
                  </Text>
                  <Divider />
                </HStack>

                {/* 소셜 로그인 버튼들 */}
                <VStack w="100%" spacing={3}>
                  <Button
                    variant="outline"
                    size="lg"
                    width="100%"
                    leftIcon={<Box>G</Box>} // 실제로는 Google 아이콘
                  >
                    Google로 로그인
                  </Button>
                  <Button
                    variant="outline"
                    size="lg"
                    width="100%"
                    leftIcon={<Box>K</Box>} // 실제로는 Kakao 아이콘
                    colorScheme="yellow"
                  >
                    카카오로 로그인
                  </Button>
                </VStack>

                {/* 회원가입 링크 */}
                <Text textAlign="center" fontSize="sm">
                  아직 계정이 없으신가요?{' '}
                  <Link
                    as={RouterLink}
                    to="/register"
                    color="primary.600"
                    fontWeight="semibold"
                    _hover={{ textDecoration: 'underline' }}
                  >
                    회원가입
                  </Link>
                </Text>
              </VStack>
            </form>
          </CardBody>
        </Card>
      </VStack>
    </Container>
  );
};

export default LoginPage;
```

### 5.8 반응형 테이블 컴포넌트

```jsx
// components/ResponsiveTable.jsx
import {
  Table,
  Thead,
  Tbody,
  Tr,
  Th,
  Td,
  TableContainer,
  Card,
  CardBody,
  Text,
  Button,
  HStack,
  VStack,
  Badge,
  Menu,
  MenuButton,
  MenuList,
  MenuItem,
  IconButton,
  useBreakpointValue,
  Box,
} from '@chakra-ui/react';
import { ChevronDownIcon, MoreVerticalIcon } from 'lucide-react';

const ResponsiveTable = ({ 
  data, 
  columns, 
  onEdit, 
  onDelete, 
  onView,
  isLoading = false 
}) => {
  const isMobile = useBreakpointValue({ base: true, md: false });

  // 모바일 카드 뷰
  const MobileCard = ({ item, index }) => (
    <Card key={index} mb={4}>
      <CardBody>
        <VStack align="stretch" spacing={3}>
          {columns.map((column, colIndex) => (
            <HStack key={colIndex} justify="space-between">
              <Text fontSize="sm" fontWeight="medium" color="gray.600">
                {column.header}
              </Text>
              <Box textAlign="right">
                {column.render ? column.render(item[column.accessor], item) : (
                  <Text fontSize="sm">{item[column.accessor]}</Text>
                )}
              </Box>
            </HStack>
          ))}
          
          {/* 액션 버튼들 */}
          <HStack spacing={2} pt={2}>
            <Button size="sm" variant="outline" onClick={() => onView?.(item)}>
              보기
            </Button>
            <Button size="sm" colorScheme="primary" onClick={() => onEdit?.(item)}>
              수정
            </Button>
            <Button size="sm" colorScheme="red" variant="outline" onClick={() => onDelete?.(item)}>
              삭제
            </Button>
          </HStack>
        </VStack>
      </CardBody>
    </Card>
  );

  // 데스크톱 테이블 뷰
  const DesktopTable = () => (
    <TableContainer>
      <Table variant="simple">
        <Thead>
          <Tr>
            {columns.map((column, index) => (
              <Th key={index}>{column.header}</Th>
            ))}
            <Th>액션</Th>
          </Tr>
        </Thead>
        <Tbody>
          {data.map((item, index) => (
            <Tr key={index}>
              {columns.map((column, colIndex) => (
                <Td key={colIndex}>
                  {column.render ? column.render(item[column.accessor], item) : (
                    <Text>{item[column.accessor]}</Text>
                  )}
                </Td>
              ))}
              <Td>
                <Menu>
                  <MenuButton
                    as={IconButton}
                    icon={<MoreVerticalIcon size={16} />}
                    variant="ghost"
                    size="sm"
                  />
                  <MenuList>
                    <MenuItem onClick={() => onView?.(item)}>
                      보기
                    </MenuItem>
                    <MenuItem onClick={() => onEdit?.(item)}>
                      수정
                    </MenuItem>
                    <MenuItem onClick={() => onDelete?.(item)} color="red.500">
                      삭제
                    </MenuItem>
                  </MenuList>
                </Menu>
              </Td>
            </Tr>
          ))}
        </Tbody>
      </Table>
    </TableContainer>
  );

  if (isLoading) {
    return (
      <Card>
        <CardBody>
          <Text textAlign="center" py={8}>로딩 중...</Text>
        </CardBody>
      </Card>
    );
  }

  if (!data || data.length === 0) {
    return (
      <Card>
        <CardBody>
          <Text textAlign="center" py={8} color="gray.500">
            데이터가 없습니다
          </Text>
        </CardBody>
      </Card>
    );
  }

  return (
    <Box>
      {isMobile ? (
        <VStack spacing={0}>
          {data.map((item, index) => (
            <MobileCard key={index} item={item} index={index} />
          ))}
        </VStack>
      ) : (
        <Card>
          <CardBody p={0}>
            <DesktopTable />
          </CardBody>
        </Card>
      )}
    </Box>
  );
};

export default ResponsiveTable;
```

### 5.9 페이지네이션 컴포넌트

```jsx
// components/Pagination.jsx
import {
  HStack,
  Button,
  Text,
  Select,
  Box,
  IconButton,
  useBreakpointValue,
} from '@chakra-ui/react';
import { ChevronLeftIcon, ChevronRightIcon } from '@chakra-ui/icons';

const Pagination = ({
  currentPage,
  totalCount,
  pageSize = 10,
  onPageChange,
  onPageSizeChange,
  pageSizeOptions = [10, 20, 50, 100]
}) => {
  const totalPages = Math.ceil(totalCount / pageSize);
  const showPageNumbers = useBreakpointValue({ base: false, md: true });
  const maxVisiblePages = useBreakpointValue({ base: 3, md: 5 });

  // 표시할 페이지 번호 계산
  const getVisiblePages = () => {
    const delta = Math.floor(maxVisiblePages / 2);
    let start = Math.max(1, currentPage - delta);
    let end = Math.min(totalPages, start + maxVisiblePages - 1);
    
    if (end - start + 1 < maxVisiblePages) {
      start = Math.max(1, end - maxVisiblePages + 1);
    }
    
    return Array.from({ length: end - start + 1 }, (_, i) => start + i);
  };

  const visiblePages = getVisiblePages();

  if (totalPages <= 1) return null;

  return (
    <HStack justify="space-between" wrap="wrap" spacing={4}>
      {/* 페이지 정보 */}
      <Text fontSize="sm" color="gray.600">
        {totalCount}개 중 {(currentPage - 1) * pageSize + 1}-
        {Math.min(currentPage * pageSize, totalCount)}개 표시
      </Text>

      {/* 페이지네이션 버튼들 */}
      <HStack spacing={1}>
        {/* 이전 페이지 */}
        <IconButton
          icon={<ChevronLeftIcon />}
          size="sm"
          variant="outline"
          isDisabled={currentPage === 1}
          onClick={() => onPageChange(currentPage - 1)}
          aria-label="이전 페이지"
        />

        {/* 첫 페이지 */}
        {showPageNumbers && visiblePages[0] > 1 && (
          <>
            <Button
              size="sm"
              variant="outline"
              onClick={() => onPageChange(1)}
            >
              1
            </Button>
            {visiblePages[0] > 2 && (
              <Text fontSize="sm" color="gray.500">...</Text>
            )}
          </>
        )}

        {/* 페이지 번호들 */}
        {showPageNumbers && visiblePages.map(page => (
          <Button
            key={page}
            size="sm"
            variant={page === currentPage ? "solid" : "outline"}
            colorScheme={page === currentPage ? "primary" : "gray"}
            onClick={() => onPageChange(page)}
          >
            {page}
          </Button>
        ))}

        {/* 마지막 페이지 */}
        {showPageNumbers && visiblePages[visiblePages.length - 1] < totalPages && (
          <>
            {visiblePages[visiblePages.length - 1] < totalPages - 1 && (
              <Text fontSize="sm" color="gray.500">...</Text>
            )}
            <Button
              size="sm"
              variant="outline"
              onClick={() => onPageChange(totalPages)}
            >
              {totalPages}
            </Button>
          </>
        )}

        {/* 다음 페이지 */}
        <IconButton
          icon={<ChevronRightIcon />}
          size="sm"
          variant="outline"
          isDisabled={currentPage === totalPages}
          onClick={() => onPageChange(currentPage + 1)}
          aria-label="다음 페이지"
        />
      </HStack>

      {/* 페이지 크기 선택 */}
      {onPageSizeChange && (
        <HStack>
          <Text fontSize="sm" whiteSpace="nowrap">페이지당</Text>
          <Select
            size="sm"
            value={pageSize}
            onChange={(e) => onPageSizeChange(Number(e.target.value))}
            width="auto"
          >
            {pageSizeOptions.map(option => (
              <option key={option} value={option}>
                {option}개
              </option>
            ))}
          </Select>
        </HStack>
      )}
    </HStack>
  );
};

export default Pagination;
```

---

## 6. 반응형 디자인 가이드

### 6.1 Chakra UI 반응형 원칙
```jsx
// 브레이크포인트 기반 스타일링
<Box
  display={{ base: 'block', md: 'flex' }}
  fontSize={{ base: 'sm', md: 'md', lg: 'lg' }}
  p={{ base: 4, md: 6, lg: 8 }}
>
  콘텐츠
</Box>

// 조건부 렌더링
const isMobile = useBreakpointValue({ base: true, md: false });
return isMobile ? <MobileComponent /> : <DesktopComponent />;
```

### 6.2 모바일 우선 설계
- **기본값은 모바일**: `base` 값을 모바일 스타일로 설정
- **점진적 향상**: 큰 화면에서 기능 추가
- **터치 친화적**: 최소 44px 터치 영역 확보

---

## 7. 상태 관리와 UI 연동 패턴

### 7.1 로딩 상태 UI 패턴
```jsx
// 스켈레톤 로딩
{loading ? (
  <SkeletonText noOfLines={4} spacing={4} />
) : (
  <Text>{content}</Text>
)}

// 스피너 로딩
<Button isLoading={isSubmitting} loadingText="저장 중...">
  저장
</Button>
```

### 7.2 에러 상태 UI 패턴
```jsx
// 인라인 에러
<Alert status="error">
  <AlertIcon />
  <AlertDescription>{error}</AlertDescription>
</Alert>

// 토스트 알림
const toast = useToast();
toast({
  title: "오류 발생",
  description: error,
  status: "error",
  duration: 5000,
  isClosable: true,
});
```

---

## 8. 성능 최적화 팁

### 8.1 컴포넌트 최적화
- **React.memo**: 불필요한 리렌더링 방지
- **useCallback/useMemo**: 함수와 값 메모화
- **지연 로딩**: React.lazy와 Suspense 활용

### 8.2 Chakra UI 최적화
- **선택적 임포트**: 필요한 컴포넌트만 import
- **테마 최적화**: 사용하지 않는 컴포넌트 스타일 제거
- **아이콘 최적화**: 필요한 아이콘만 번들에 포함

---

## 9. 접근성(Accessibility) 가이드

### 9.1 기본 접근성 원칙
- **시맨틱 HTML**: 의미있는 마크업 사용
- **키보드 네비게이션**: Tab으로 모든 요소 접근 가능
- **색상 대비**: WCAG 가이드라인 준수
- **스크린 리더**: aria-label, aria-describedby 활용

### 9.2 Chakra UI 접근성 기능
```jsx
// 스크린 리더를 위한 라벨
<Button aria-label="장바구니에 상품 추가">
  <PlusIcon />
</Button>

// 포커스 관리
<Modal isOpen={isOpen} onClose={onClose} initialFocusRef={initialRef}>
  <ModalContent>
    <Input ref={initialRef} placeholder="검색어 입력" />
  </ModalContent>
</Modal>
```

---

## 10. 배포 및 빌드 최적화

### 10.1 Vite 설정 최적화
```js
// vite.config.js
export default defineConfig({
  build: {
    rollupOptions: {
      output: {
        manualChunks: {
          vendor: ['react', 'react-dom'],
          ui: ['@chakra-ui/react'],
        },
      },
    },
  },
});
```

### 10.2 환경별 설정
```js
// .env.development
VITE_API_BASE_URL=http://localhost:3001/api
VITE_APP_TITLE=MyApp (Development)

// .env.production
VITE_API_BASE_URL=https://api.myapp.com
VITE_APP_TITLE=MyApp
```

이 가이드를 통해 Chakra UI를 활용한 현대적이고 사용자 친화적인 React 애플리케이션을 구축할 수 있습니다. 각 컴포넌트는 재사용 가능하도록 설계되었으며, 반응형 디자인과 접근성을 고려하여 작성되었습니다.