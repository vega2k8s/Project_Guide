# Chakra UI 상세 화면 설계 가이드
*실무 중심의 디자인 시스템 구축 가이드*

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

## 1. Chakra UI 디자인 시스템 원칙

### 1.1 디자인 토큰 체계

**색상 시스템 (Color System)**
```js
// theme/colors.js
const colors = {
  // Primary 브랜드 색상 (9단계)
  primary: {
    50: '#e3f2fd',   // 가장 연한 색 (배경용)
    100: '#bbdefb',  // 연한 색 (호버 배경)
    200: '#90caf9',  // 
    300: '#64b5f6',  // 
    400: '#42a5f5',  // 
    500: '#2196f3',  // 기본 색상 (메인)
    600: '#1e88e5',  // 진한 색 (호버)
    700: '#1976d2',  // 더 진한 색 (액티브)
    800: '#1565c0',  // 
    900: '#0d47a1',  // 가장 진한 색 (텍스트)
  },
  
  // Semantic 색상
  semantic: {
    success: '#10b981',
    warning: '#f59e0b',
    error: '#ef4444',
    info: '#3b82f6',
  },
  
  // Gray Scale
  gray: {
    50: '#f8fafc',
    100: '#f1f5f9',
    200: '#e2e8f0',
    300: '#cbd5e1',
    400: '#94a3b8',
    500: '#64748b',
    600: '#475569',
    700: '#334155',
    800: '#1e293b',
    900: '#0f172a',
  }
};
```

**간격 시스템 (Spacing System)**
```js
// 4px 기반 스케일 (rem 단위)
const space = {
  0: '0',
  1: '0.25rem',  // 4px
  2: '0.5rem',   // 8px
  3: '0.75rem',  // 12px
  4: '1rem',     // 16px
  5: '1.25rem',  // 20px
  6: '1.5rem',   // 24px
  8: '2rem',     // 32px
  10: '2.5rem',  // 40px
  12: '3rem',    // 48px
  16: '4rem',    // 64px
  20: '5rem',    // 80px
  24: '6rem',    // 96px
};
```

**타이포그래피 시스템**
```js
const fontSizes = {
  xs: '0.75rem',    // 12px
  sm: '0.875rem',   // 14px
  md: '1rem',       // 16px (기본)
  lg: '1.125rem',   // 18px
  xl: '1.25rem',    // 20px
  '2xl': '1.5rem',  // 24px
  '3xl': '1.875rem', // 30px
  '4xl': '2.25rem',  // 36px
  '5xl': '3rem',     // 48px
  '6xl': '3.75rem',  // 60px
};

const fontWeights = {
  hairline: 100,
  thin: 200,
  light: 300,
  normal: 400,
  medium: 500,
  semibold: 600,
  bold: 700,
  extrabold: 800,
  black: 900,
};
```

### 1.2 컴포넌트 설계 원칙

**일관성 (Consistency)**
- 동일한 기능에는 동일한 컴포넌트 사용
- 색상, 간격, 타이포그래피의 일관된 적용
- 인터랙션 패턴의 통일성

**계층 구조 (Hierarchy)**
- 시각적 가중치를 통한 정보 우선순위 표현
- 크기, 색상, 간격을 활용한 계층 구조
- 사용자의 시선 흐름 고려

**접근성 (Accessibility)**
- 색상 대비비 4.5:1 이상 유지
- 키보드 네비게이션 지원
- 스크린 리더 호환성

**반응형 (Responsive)**
- 모바일 우선 설계
- 브레이크포인트별 최적화
- 유연한 그리드 시스템

---

## 2. 레이아웃 설계 원칙

### 2.1 그리드 시스템

**12컬럼 그리드 기반**
```jsx
// 기본 그리드 레이아웃
<SimpleGrid columns={{ base: 1, md: 2, lg: 3, xl: 4 }} spacing={6}>
  {items.map(item => <ItemCard key={item.id} item={item} />)}
</SimpleGrid>

// 복합 레이아웃
<Grid templateColumns="repeat(12, 1fr)" gap={6}>
  <GridItem colSpan={{ base: 12, md: 8 }}>
    <MainContent />
  </GridItem>
  <GridItem colSpan={{ base: 12, md: 4 }}>
    <Sidebar />
  </GridItem>
</Grid>
```

**Container 시스템**
```jsx
// 컨테이너 크기별 최대 너비
const containerSizes = {
  sm: '640px',
  md: '768px',
  lg: '1024px',
  xl: '1280px',
  '2xl': '1536px',
};

// 사용 예시
<Container maxW="container.xl" px={{ base: 4, md: 6 }}>
  <Content />
</Container>
```

### 2.2 컴포넌트 간격 규칙

**수직 간격 (Vertical Spacing)**
- 제목과 본문: `spacing={4}` (16px)
- 섹션 간: `spacing={8}` (32px)
- 페이지 섹션 간: `spacing={12}` (48px)

**수평 간격 (Horizontal Spacing)**
- 버튼 간: `spacing={3}` (12px)
- 폼 요소 간: `spacing={4}` (16px)
- 카드 간: `spacing={6}` (24px)

---

## 3. 컴포넌트별 설계 가이드

### 3.1 버튼 (Button) 설계 원칙

**버튼 계층 구조**
1. **Primary Button**: 주요 액션 (페이지당 1개)
2. **Secondary Button**: 보조 액션
3. **Tertiary Button**: 부가 액션
4. **Destructive Button**: 삭제/취소 액션

**버튼 크기 가이드**
- `xs`: 24px 높이 (아이콘 버튼)
- `sm`: 32px 높이 (폼 내부)
- `md`: 40px 높이 (기본)
- `lg`: 48px 높이 (주요 CTA)

### 3.2 폼 (Form) 설계 원칙

**폼 레이아웃 패턴**
```jsx
// 단일 컬럼 폼 (권장)
<VStack spacing={6} align="stretch">
  <FormField />
  <FormField />
  <ActionButtons />
</VStack>

// 다중 컬럼 폼 (필요시)
<SimpleGrid columns={{ base: 1, md: 2 }} spacing={6}>
  <FormField />
  <FormField />
</SimpleGrid>
```

**입력 필드 상태**
- Default: 기본 상태
- Focus: 포커스 상태 (border 색상 변경)
- Error: 오류 상태 (빨간색 border + 오류 메시지)
- Disabled: 비활성 상태 (회색 처리)

### 3.3 카드 (Card) 설계 원칙

**카드 변형**
- **Elevated**: 그림자 있는 카드 (기본)
- **Outlined**: 테두리만 있는 카드
- **Filled**: 배경색이 있는 카드

**카드 내부 구조**
1. **Header**: 제목과 액션
2. **Body**: 주요 콘텐츠
3. **Footer**: 부가 정보와 액션

---

## 4. 실제 화면 설계 예시

### 4.1 커스텀 테마 설정

```jsx
// theme/index.js
import { extendTheme } from '@chakra-ui/react';
import { colors } from './colors';
import { fonts } from './fonts';
import { components } from './components';

const theme = extendTheme({
  colors,
  fonts,
  components,
  
  // 전역 스타일
  styles: {
    global: (props) => ({
      body: {
        fontFamily: 'body',
        color: props.colorMode === 'dark' ? 'whiteAlpha.900' : 'gray.800',
        bg: props.colorMode === 'dark' ? 'gray.900' : 'gray.50',
        lineHeight: 'base',
      },
      '*::placeholder': {
        color: props.colorMode === 'dark' ? 'whiteAlpha.400' : 'gray.400',
      },
      '*, *::before, &::after': {
        borderColor: props.colorMode === 'dark' ? 'whiteAlpha.300' : 'gray.200',
        wordWrap: 'break-word',
      },
    }),
  },
  
  // 브레이크포인트
  breakpoints: {
    sm: '30em',    // 480px
    md: '48em',    // 768px
    lg: '62em',    // 992px
    xl: '80em',    // 1280px
    '2xl': '96em', // 1536px
  },
  
  // 컴포넌트 기본 props
  config: {
    initialColorMode: 'light',
    useSystemColorMode: false,
  },
});

export default theme;
```

### 4.2 컴포넌트 변형 정의

```jsx
// theme/components.js
const Button = {
  baseStyle: {
    fontWeight: 'semibold',
    borderRadius: 'md',
    _focus: {
      boxShadow: 'outline',
    },
  },
  sizes: {
    xs: {
      h: '6',
      minW: '6',
      fontSize: 'xs',
      px: '2',
    },
    sm: {
      h: '8',
      minW: '8',
      fontSize: 'sm',
      px: '3',
    },
    md: {
      h: '10',
      minW: '10',
      fontSize: 'md',
      px: '4',
    },
    lg: {
      h: '12',
      minW: '12',
      fontSize: 'lg',
      px: '6',
    },
  },
  variants: {
    solid: (props) => ({
      bg: `${props.colorScheme}.500`,
      color: 'white',
      _hover: {
        bg: `${props.colorScheme}.600`,
        _disabled: {
          bg: `${props.colorScheme}.500`,
        },
      },
      _active: { bg: `${props.colorScheme}.700` },
    }),
    outline: (props) => ({
      border: '1px solid',
      borderColor: `${props.colorScheme}.500`,
      color: `${props.colorScheme}.500`,
      _hover: {
        bg: `${props.colorScheme}.50`,
      },
      _active: {
        bg: `${props.colorScheme}.100`,
      },
    }),
    ghost: (props) => ({
      color: `${props.colorScheme}.500`,
      _hover: {
        bg: `${props.colorScheme}.50`,
      },
      _active: {
        bg: `${props.colorScheme}.100`,
      },
    }),
  },
  defaultProps: {
    size: 'md',
    variant: 'solid',
    colorScheme: 'primary',
  },
};

const Card = {
  baseStyle: {
    container: {
      borderRadius: 'lg',
      bg: 'white',
      boxShadow: 'sm',
      overflow: 'hidden',
      _dark: {
        bg: 'gray.800',
      },
    },
    header: {
      px: '6',
      py: '4',
      borderBottom: '1px solid',
      borderColor: 'gray.100',
      _dark: {
        borderColor: 'gray.700',
      },
    },
    body: {
      px: '6',
      py: '4',
    },
    footer: {
      px: '6',
      py: '4',
      borderTop: '1px solid',
      borderColor: 'gray.100',
      _dark: {
        borderColor: 'gray.700',
      },
    },
  },
  variants: {
    elevated: {
      container: {
        boxShadow: 'md',
        _hover: {
          boxShadow: 'lg',
        },
      },
    },
    outline: {
      container: {
        boxShadow: 'none',
        border: '1px solid',
        borderColor: 'gray.200',
        _dark: {
          borderColor: 'gray.700',
        },
      },
    },
    filled: {
      container: {
        bg: 'gray.50',
        _dark: {
          bg: 'gray.900',
        },
      },
    },
  },
  defaultProps: {
    variant: 'elevated',
  },
};

export const components = { Button, Card };
```

### 4.3 대시보드 메인 페이지

```jsx
// pages/DashboardPage.jsx
import {
  Box,
  Container,
  Heading,
  Text,
  SimpleGrid,
  Stat,
  StatLabel,
  StatNumber,
  StatHelpText,
  StatArrow,
  Card,
  CardHeader,
  CardBody,
  VStack,
  HStack,
  Icon,
  useColorModeValue,
  Flex,
  Spacer,
  Button,
  Menu,
  MenuButton,
  MenuList,
  MenuItem,
  Avatar,
  Breadcrumb,
  BreadcrumbItem,
  BreadcrumbLink,
} from '@chakra-ui/react';
import {
  TrendingUpIcon,
  UsersIcon,
  ShoppingCartIcon,
  DollarSignIcon,
  MoreVerticalIcon,
  ChevronRightIcon,
} from 'lucide-react';
import { useState, useEffect } from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { fetchDashboardData } from '../store/slices/dashboardSlice';
import DashboardChart from '../components/DashboardChart';
import RecentActivity from '../components/RecentActivity';
import QuickActions from '../components/QuickActions';

const DashboardPage = () => {
  const dispatch = useDispatch();
  const { data, loading, error } = useSelector(state => state.dashboard);
  const { user } = useSelector(state => state.auth);
  
  const cardBg = useColorModeValue('white', 'gray.800');
  const borderColor = useColorModeValue('gray.200', 'gray.700');
  const textSecondary = useColorModeValue('gray.600', 'gray.400');

  useEffect(() => {
    dispatch(fetchDashboardData());
  }, [dispatch]);

  // 통계 카드 데이터
  const stats = [
    {
      label: '총 매출',
      value: '₩2,847,293',
      change: 12.5,
      icon: DollarSignIcon,
      color: 'green',
    },
    {
      label: '총 주문',
      value: '1,247',
      change: 8.2,
      icon: ShoppingCartIcon,
      color: 'blue',
    },
    {
      label: '신규 고객',
      value: '394',
      change: -2.4,
      icon: UsersIcon,
      color: 'purple',
    },
    {
      label: '전환율',
      value: '3.2%',
      change: 5.1,
      icon: TrendingUpIcon,
      color: 'orange',
    },
  ];

  return (
    <Container maxW="container.2xl" py={8}>
      <VStack spacing={8} align="stretch">
        {/* 페이지 헤더 */}
        <Box>
          {/* 브레드크럼 */}
          <Breadcrumb 
            separator={<ChevronRightIcon size={16} />}
            fontSize="sm"
            mb={4}
          >
            <BreadcrumbItem>
              <BreadcrumbLink href="/">홈</BreadcrumbLink>
            </BreadcrumbItem>
            <BreadcrumbItem isCurrentPage>
              <BreadcrumbLink>대시보드</BreadcrumbLink>
            </BreadcrumbItem>
          </Breadcrumb>

          {/* 헤더 콘텐츠 */}
          <Flex align="center" mb={2}>
            <VStack align="start" spacing={1}>
              <Heading size="xl">대시보드</Heading>
              <Text color={textSecondary}>
                안녕하세요, {user?.name}님! 오늘도 좋은 하루 되세요.
              </Text>
            </VStack>
            <Spacer />
            
            {/* 액션 버튼들 */}
            <HStack>
              <Button variant="outline" size="sm">
                보고서 다운로드
              </Button>
              <Button colorScheme="primary" size="sm">
                새 프로젝트
              </Button>
              <Menu>
                <MenuButton
                  as={Button}
                  variant="ghost"
                  size="sm"
                  p={2}
                >
                  <MoreVerticalIcon size={16} />
                </MenuButton>
                <MenuList>
                  <MenuItem>설정</MenuItem>
                  <MenuItem>도움말</MenuItem>
                </MenuList>
              </Menu>
            </HStack>
          </Flex>
        </Box>

        {/* 통계 카드들 */}
        <SimpleGrid columns={{ base: 1, md: 2, lg: 4 }} spacing={6}>
          {stats.map((stat, index) => (
            <Card key={index} variant="elevated">
              <CardBody>
                <Flex align="center">
                  <Box>
                    <Stat>
                      <StatLabel color={textSecondary} fontSize="sm">
                        {stat.label}
                      </StatLabel>
                      <StatNumber fontSize="2xl" fontWeight="bold">
                        {stat.value}
                      </StatNumber>
                      <StatHelpText mb={0}>
                        <StatArrow 
                          type={stat.change >= 0 ? 'increase' : 'decrease'} 
                        />
                        {Math.abs(stat.change)}% 지난 달 대비
                      </StatHelpText>
                    </Stat>
                  </Box>
                  <Spacer />
                  <Box
                    p={3}
                    borderRadius="md"
                    bg={`${stat.color}.50`}
                    _dark={{ bg: `${stat.color}.900` }}
                  >
                    <Icon
                      as={stat.icon}
                      boxSize={6}
                      color={`${stat.color}.500`}
                    />
                  </Box>
                </Flex>
              </CardBody>
            </Card>
          ))}
        </SimpleGrid>

        {/* 메인 콘텐츠 그리드 */}
        <SimpleGrid columns={{ base: 1, xl: 3 }} spacing={8}>
          {/* 차트 영역 (2/3 너비) */}
          <Box gridColumn={{ xl: 'span 2' }}>
            <Card variant="elevated" h="400px">
              <CardHeader>
                <Flex align="center">
                  <VStack align="start" spacing={1}>
                    <Heading size="md">매출 트렌드</Heading>
                    <Text fontSize="sm" color={textSecondary}>
                      최근 12개월 매출 현황
                    </Text>
                  </VStack>
                  <Spacer />
                  <Menu>
                    <MenuButton as={Button} variant="ghost" size="sm">
                      <MoreVerticalIcon size={16} />
                    </MenuButton>
                    <MenuList>
                      <MenuItem>PDF로 내보내기</MenuItem>
                      <MenuItem>데이터 보기</MenuItem>
                      <MenuItem>설정</MenuItem>
                    </MenuList>
                  </Menu>
                </Flex>
              </CardHeader>
              <CardBody pt={0}>
                <DashboardChart data={data?.chartData} loading={loading} />
              </CardBody>
            </Card>
          </Box>

          {/* 사이드바 영역 (1/3 너비) */}
          <VStack spacing={6} align="stretch">
            {/* 빠른 액션 */}
            <Card variant="elevated">
              <CardHeader>
                <Heading size="sm">빠른 액션</Heading>
              </CardHeader>
              <CardBody pt={0}>
                <QuickActions />
              </CardBody>
            </Card>

            {/* 최근 활동 */}
            <Card variant="elevated">
              <CardHeader>
                <Flex align="center">
                  <Heading size="sm">최근 활동</Heading>
                  <Spacer />
                  <Button variant="ghost" size="xs" color={textSecondary}>
                    모두 보기
                  </Button>
                </Flex>
              </CardHeader>
              <CardBody pt={0}>
                <RecentActivity activities={data?.recentActivities} />
              </CardBody>
            </Card>
          </VStack>
        </SimpleGrid>

        {/* 하단 테이블 영역 */}
        <Card variant="elevated">
          <CardHeader>
            <Flex align="center">
              <VStack align="start" spacing={1}>
                <Heading size="md">최근 주문</Heading>
                <Text fontSize="sm" color={textSecondary}>
                  오늘 접수된 주문 현황
                </Text>
              </VStack>
              <Spacer />
              <Button variant="outline" size="sm">
                전체 보기
              </Button>
            </Flex>
          </CardHeader>
          <CardBody pt={0}>
            {/* 여기에 주문 테이블 컴포넌트 */}
            <RecentOrdersTable orders={data?.recentOrders} />
          </CardBody>
        </Card>
      </VStack>
    </Container>
  );
};

export default DashboardPage;
```

### 4.4 고급 폼 컴포넌트

```jsx
// components/AdvancedForm.jsx
import {
  Box,
  VStack,
  HStack,
  FormControl,
  FormLabel,
  FormErrorMessage,
  FormHelperText,
  Input,
  Textarea,
  Select,
  Checkbox,
  Radio,
  RadioGroup,
  Switch,
  Button,
  Progress,
  Alert,
  AlertIcon,
  AlertDescription,
  Divider,
  Text,
  Badge,
  useToast,
  useColorModeValue,
} from '@chakra-ui/react';
import { useState } from 'react';
import { useForm, Controller } from 'react-hook-form';
import { yupResolver } from '@hookform/resolvers/yup';
import * as yup from 'yup';

// 폼 검증 스키마
const schema = yup.object({
  firstName: yup.string().required('이름을 입력해주세요'),
  lastName: yup.string().required('성을 입력해주세요'),
  email: yup.string().email('올바른 이메일을 입력해주세요').required('이메일을 입력해주세요'),
  phone: yup.string().matches(/^[0-9-]+$/, '올바른 전화번호를 입력해주세요'),
  age: yup.number().min(18, '18세 이상이어야 합니다').max(100, '100세 이하여야 합니다'),
  category: yup.string().required('카테고리를 선택해주세요'),
  description: yup.string().max(500, '500자 이하로 입력해주세요'),
  terms: yup.boolean().oneOf([true], '약관에 동의해주세요'),
});

const AdvancedForm = ({ onSubmit, initialData = {} }) => {
  const toast = useToast();
  const [currentStep, setCurrentStep] = useState(1);
  const totalSteps = 3;
  
  const borderColor = useColorModeValue('gray.200', 'gray.700');
  const bgColor = useColorModeValue('gray.50', 'gray.900');

  const {
    register,
    handleSubmit,
    control,
    watch,
    formState: { errors, isValid, isSubmitting, touchedFields }
  } = useForm({
    resolver: yupResolver(schema),
    defaultValues: initialData,
    mode: 'onChange',
  });

  // 진행률 계산
  const getProgress = () => (currentStep / totalSteps) * 100;

  // 다음 단계로
  const nextStep = () => {
    if (currentStep < totalSteps) {
      setCurrentStep(currentStep + 1);
    }
  };

  // 이전 단계로
  const prevStep = () => {
    if (currentStep > 1) {
      setCurrentStep(currentStep - 1);
    }
  };

  // 폼 제출 처리
  const handleFormSubmit = async (data) => {
    try {
      await onSubmit(data);
      toast({
        title: '저장 완료',
        description: '정보가 성공적으로 저장되었습니다.',
        status: 'success',
        duration: 3000,
        isClosable: true,
      });
    } catch (error) {
      toast({
        title: '저장 실패',
        description: error.message || '오류가 발생했습니다.',
        status: 'error',
        duration: 5000,
        isClosable: true,
      });
    }
  };

  // 필드 상태에 따른 스타일
  const getFieldStatus = (fieldName) => {
    if (errors[fieldName]) return 'error';
    if (touchedFields[fieldName] && !errors[fieldName]) return 'success';
    return 'default';
  };

  return (
    <Box maxW="600px" mx="auto" p={6}>
      <VStack spacing={8} align="stretch">
        {/* 진행률 표시 */}
        <Box>
          <HStack justify="space-between" mb={2}>
            <Text fontSize="sm" fontWeight="medium">
              단계 {currentStep} / {totalSteps}
            </Text>
            <Text fontSize="sm" color="gray.500">
              {Math.round(getProgress())}% 완료
            </Text>
          </HStack>
          <Progress 
            value={getProgress()} 
            colorScheme="primary" 
            size="sm" 
            borderRadius="full"
          />
        </Box>

        {/* 단계별 제목 */}
        <Box textAlign="center">
          <Text fontSize="2xl" fontWeight="bold" mb={2}>
            {currentStep === 1 && '기본 정보'}
            {currentStep === 2 && '상세 정보'}
            {currentStep === 3 && '약관 동의'}
          </Text>
          <Text color="gray.600">
            {currentStep === 1 && '기본적인 개인정보를 입력해주세요'}
            {currentStep === 2 && '추가 정보를 입력해주세요'}
            {currentStep === 3 && '약관을 확인하고 동의해주세요'}
          </Text>
        </Box>

        {/* 폼 콘텐츠 */}
        <form onSubmit={handleSubmit(handleFormSubmit)}>
          <VStack spacing={6} align="stretch">
            
            {/* 1단계: 기본 정보 */}
            {currentStep === 1 && (
              <VStack spacing={6} align="stretch">
                <HStack spacing={4}>
                  <FormControl isInvalid={errors.firstName} isRequired>
                    <FormLabel>이름</FormLabel>
                    <Input
                      {...register('firstName')}
                      placeholder="홍길동"
                      borderColor={getFieldStatus('firstName') === 'error' ? 'red.300' : borderColor}
                      _focus={{
                        borderColor: getFieldStatus('firstName') === 'error' ? 'red.500' : 'primary.500',
                        boxShadow: '0 0 0 1px var(--chakra-colors-primary-500)',
                      }}
                    />
                    <FormErrorMessage>{errors.firstName?.message}</FormErrorMessage>
                  </FormControl>

                  <FormControl isInvalid={errors.lastName} isRequired>
                    <FormLabel>성</FormLabel>
                    <Input
                      {...register('lastName')}
                      placeholder="홍"
                      borderColor={getFieldStatus('lastName') === 'error' ? 'red.300' : borderColor}
                    />
                    <FormErrorMessage>{errors.lastName?.message}</FormErrorMessage>
                  </FormControl>
                </HStack>

                <FormControl isInvalid={errors.email} isRequired>
                  <FormLabel>이메일</FormLabel>
                  <Input
                    {...register('email')}
                    type="email"
                    placeholder="hong@example.com"
                    borderColor={getFieldStatus('email') === 'error' ? 'red.300' : borderColor}
                  />
                  <FormErrorMessage>{errors.email?.message}</FormErrorMessage>
                  <FormHelperText>
                    인증 메일이 발송될 이메일 주소입니다.
                  </FormHelperText>
                </FormControl>

                <FormControl isInvalid={errors.phone}>
                  <FormLabel>전화번호</FormLabel>
                  <Input
                    {...register('phone')}
                    type="tel"
                    placeholder="010-1234-5678"
                    borderColor={getFieldStatus('phone') === 'error' ? 'red.300' : borderColor}
                  />
                  <FormErrorMessage>{errors.phone?.message}</FormErrorMessage>
                </FormControl>
              </VStack>
            )}

            {/* 2단계: 상세 정보 */}
            {currentStep === 2 && (
              <VStack spacing={6} align="stretch">
                <HStack spacing={4}>
                  <FormControl isInvalid={errors.age}>
                    <FormLabel>나이</FormLabel>
                    <Input
                      {...register('age')}
                      type="number"
                      placeholder="25"
                      min="18"
                      max="100"
                    />
                    <FormErrorMessage>{errors.age?.message}</FormErrorMessage>
                  </FormControl>

                  <FormControl isInvalid={errors.category} isRequired>
                    <FormLabel>카테고리</FormLabel>
                    <Select {...register('category')} placeholder="선택해주세요">
                      <option value="individual">개인</option>
                      <option value="business">사업자</option>
                      <option value="organization">단체</option>
                    </Select>
                    <FormErrorMessage>{errors.category?.message}</FormErrorMessage>
                  </FormControl>
                </HStack>

                <FormControl>
                  <FormLabel>알림 설정</FormLabel>
                  <VStack align="start" spacing={3}>
                    <Controller
                      name="emailNotifications"
                      control={control}
                      render={({ field }) => (
                        <Checkbox {...field} colorScheme="primary">
                          이메일 알림 받기
                        </Checkbox>
                      )}
                    />
                    <Controller
                      name="smsNotifications"
                      control={control}
                      render={({ field }) => (
                        <Checkbox {...field} colorScheme="primary">
                          SMS 알림 받기
                        </Checkbox>
                      )}
                    />
                    <Controller
                      name="pushNotifications"
                      control={control}
                      render={({ field }) => (
                        <Checkbox {...field} colorScheme="primary">
                          푸시 알림 받기
                        </Checkbox>
                      )}
                    />
                  </VStack>
                </FormControl>

                <FormControl>
                  <FormLabel>언어 설정</FormLabel>
                  <Controller
                    name="language"
                    control={control}
                    defaultValue="ko"
                    render={({ field }) => (
                      <RadioGroup {...field}>
                        <HStack spacing={6}>
                          <Radio value="ko" colorScheme="primary">한국어</Radio>
                          <Radio value="en" colorScheme="primary">English</Radio>
                          <Radio value="ja" colorScheme="primary">日本語</Radio>
                        </HStack>
                      </RadioGroup>
                    )}
                  />
                </FormControl>

                <FormControl isInvalid={errors.description}>
                  <FormLabel>자기소개</FormLabel>
                  <Textarea
                    {...register('description')}
                    placeholder="간단한 자기소개를 작성해주세요"
                    rows={4}
                    resize="vertical"
                  />
                  <FormErrorMessage>{errors.description?.message}</FormErrorMessage>
                  <FormHelperText>
                    {watch('description')?.length || 0}/500자
                  </FormHelperText>
                </FormControl>
              </VStack>
            )}

            {/* 3단계: 약관 동의 */}
            {currentStep === 3 && (
              <VStack spacing={6} align="stretch">
                <Alert status="info" borderRadius="md">
                  <AlertIcon />
                  <AlertDescription>
                    서비스 이용을 위해 아래 약관에 동의해주세요.
                  </AlertDescription>
                </Alert>

                <Box
                  border="1px solid"
                  borderColor={borderColor}
                  borderRadius="md"
                  p={4}
                  bg={bgColor}
                  maxH="200px"
                  overflowY="auto"
                >
                  <Text fontSize="sm" lineHeight="1.6">
                    <Text fontWeight="bold" mb={2}>이용약관</Text>
                    제1조 (목적) 이 약관은 회사가 제공하는 서비스의 이용조건 및 절차에 관한 사항과 
                    기타 필요한 사항을 규정함을 목적으로 합니다.
                    <br /><br />
                    제2조 (정의) 이 약관에서 사용하는 용어의 정의는 다음과 같습니다...
                    <br /><br />
                    제3조 (약관의 효력 및 변경) 이 약관은 서비스 화면에 게시하거나 
                    기타의 방법으로 회원에게 공지함으로써 효력을 발생합니다...
                  </Text>
                </Box>

                <FormControl isInvalid={errors.terms} isRequired>
                  <Controller
                    name="terms"
                    control={control}
                    render={({ field }) => (
                      <Checkbox 
                        {...field} 
                        colorScheme="primary"
                        size="lg"
                      >
                        <Text>
                          <Text as="span" fontWeight="semibold">
                            이용약관
                          </Text>
                          에 동의합니다. (필수)
                        </Text>
                      </Checkbox>
                    )}
                  />
                  <FormErrorMessage>{errors.terms?.message}</FormErrorMessage>
                </FormControl>

                <FormControl>
                  <Controller
                    name="marketing"
                    control={control}
                    render={({ field }) => (
                      <Checkbox {...field} colorScheme="primary" size="lg">
                        마케팅 정보 수신에 동의합니다. (선택)
                      </Checkbox>
                    )}
                  />
                  <FormHelperText>
                    이벤트, 할인 혜택 등의 마케팅 정보를 받아보실 수 있습니다.
                  </FormHelperText>
                </FormControl>
              </VStack>
            )}

            <Divider />

            {/* 네비게이션 버튼들 */}
            <HStack justify="space-between">
              <Button
                variant="outline"
                onClick={prevStep}
                isDisabled={currentStep === 1}
              >
                이전
              </Button>

              <HStack>
                {/* 단계 인디케이터 */}
                <HStack spacing={2}>
                  {[...Array(totalSteps)].map((_, index) => (
                    <Box
                      key={index}
                      w="8px"
                      h="8px"
                      borderRadius="full"
                      bg={index + 1 <= currentStep ? 'primary.500' : 'gray.300'}
                      transition="all 0.2s"
                    />
                  ))}
                </HStack>
              </HStack>

              {currentStep < totalSteps ? (
                <Button colorScheme="primary" onClick={nextStep}>
                  다음
                </Button>
              ) : (
                <Button
                  type="submit"
                  colorScheme="primary"
                  isLoading={isSubmitting}
                  loadingText="저장 중..."
                  isDisabled={!isValid}
                >
                  완료
                </Button>
              )}
            </HStack>
          </VStack>
        </form>
      </VStack>
    </Box>
  );
};

export default AdvancedForm;
```

### 4.5 데이터 테이블 컴포넌트

```jsx
// components/DataTable.jsx
import {
  Table,
  Thead,
  Tbody,
  Tr,
  Th,
  Td,
  TableContainer,
  Box,
  Flex,
  HStack,
  VStack,
  Text,
  Button,
  IconButton,
  Input,
  Select,
  Checkbox,
  Badge,
  Avatar,
  Menu,
  MenuButton,
  MenuList,
  MenuItem,
  Skeleton,
  Alert,
  AlertIcon,
  useColorModeValue,
  Card,
  CardHeader,
  CardBody,
} from '@chakra-ui/react';
import {
  ChevronUpIcon,
  ChevronDownIcon,
  SearchIcon,
  FilterIcon,
  DownloadIcon,
  MoreVerticalIcon,
} from 'lucide-react';
import { useState, useMemo } from 'react';
import Pagination from './Pagination';

const DataTable = ({
  data = [],
  columns = [],
  loading = false,
  error = null,
  onRowClick,
  onSort,
  onFilter,
  onExport,
  selectable = false,
  searchable = true,
  filterable = true,
  exportable = true,
  pageSize = 10,
}) => {
  const [selectedRows, setSelectedRows] = useState(new Set());
  const [searchTerm, setSearchTerm] = useState('');
  const [sortConfig, setSortConfig] = useState({ key: null, direction: 'asc' });
  const [currentPage, setCurrentPage] = useState(1);
  const [filters, setFilters] = useState({});

  const headerBg = useColorModeValue('gray.50', 'gray.700');
  const borderColor = useColorModeValue('gray.200', 'gray.600');
  const hoverBg = useColorModeValue('gray.50', 'gray.700');

  // 데이터 필터링 및 검색
  const filteredData = useMemo(() => {
    let filtered = [...data];

    // 검색 필터링
    if (searchTerm) {
      filtered = filtered.filter(row =>
        columns.some(column => {
          const cellValue = row[column.accessor];
          return cellValue?.toString().toLowerCase().includes(searchTerm.toLowerCase());
        })
      );
    }

    // 컬럼 필터링
    Object.entries(filters).forEach(([key, value]) => {
      if (value) {
        filtered = filtered.filter(row => 
          row[key]?.toString().toLowerCase().includes(value.toLowerCase())
        );
      }
    });

    return filtered;
  }, [data, searchTerm, filters, columns]);

  // 데이터 정렬
  const sortedData = useMemo(() => {
    if (!sortConfig.key) return filteredData;

    return [...filteredData].sort((a, b) => {
      const aValue = a[sortConfig.key];
      const bValue = b[sortConfig.key];

      if (aValue < bValue) {
        return sortConfig.direction === 'asc' ? -1 : 1;
      }
      if (aValue > bValue) {
        return sortConfig.direction === 'asc' ? 1 : -1;
      }
      return 0;
    });
  }, [filteredData, sortConfig]);

  // 페이지네이션
  const paginatedData = useMemo(() => {
    const startIndex = (currentPage - 1) * pageSize;
    return sortedData.slice(startIndex, startIndex + pageSize);
  }, [sortedData, currentPage, pageSize]);

  // 정렬 처리
  const handleSort = (columnKey) => {
    let direction = 'asc';
    if (sortConfig.key === columnKey && sortConfig.direction === 'asc') {
      direction = 'desc';
    }
    setSortConfig({ key: columnKey, direction });
    onSort?.(columnKey, direction);
  };

  // 행 선택 처리
  const handleRowSelect = (rowId, isSelected) => {
    const newSelected = new Set(selectedRows);
    if (isSelected) {
      newSelected.add(rowId);
    } else {
      newSelected.delete(rowId);
    }
    setSelectedRows(newSelected);
  };

  // 전체 선택 처리
  const handleSelectAll = (isSelected) => {
    if (isSelected) {
      const allIds = new Set(paginatedData.map(row => row.id));
      setSelectedRows(allIds);
    } else {
      setSelectedRows(new Set());
    }
  };

  // 필터 변경 처리
  const handleFilterChange = (columnKey, value) => {
    setFilters(prev => ({
      ...prev,
      [columnKey]: value
    }));
    setCurrentPage(1);
    onFilter?.(columnKey, value);
  };

  // 로딩 상태
  if (loading) {
    return (
      <Card>
        <CardBody>
          <VStack spacing={4}>
            {[...Array(5)].map((_, index) => (
              <Skeleton key={index} height="40px" width="100%" />
            ))}
          </VStack>
        </CardBody>
      </Card>
    );
  }

  // 에러 상태
  if (error) {
    return (
      <Alert status="error" borderRadius="md">
        <AlertIcon />
        {error}
      </Alert>
    );
  }

  return (
    <Card>
      {/* 테이블 헤더 (검색, 필터, 액션) */}
      <CardHeader>
        <Flex justify="space-between" align="center" wrap="wrap" gap={4}>
          <VStack align="start" spacing={1}>
            <Text fontSize="lg" fontWeight="semibold">
              데이터 목록
            </Text>
            <Text fontSize="sm" color="gray.500">
              총 {filteredData.length}개 항목
            </Text>
          </VStack>

          <HStack spacing={2} wrap="wrap">
            {/* 검색 */}
            {searchable && (
              <HStack>
                <SearchIcon size={16} />
                <Input
                  placeholder="검색..."
                  value={searchTerm}
                  onChange={(e) => setSearchTerm(e.target.value)}
                  size="sm"
                  width="200px"
                />
              </HStack>
            )}

            {/* 필터 */}
            {filterable && (
              <Menu>
                <MenuButton as={Button} leftIcon={<FilterIcon size={16} />} size="sm">
                  필터
                </MenuButton>
                <MenuList>
                  {columns
                    .filter(col => col.filterable)
                    .map(column => (
                      <Box key={column.accessor} px={3} py={2}>
                        <Text fontSize="sm" fontWeight="medium" mb={1}>
                          {column.header}
                        </Text>
                        <Input
                          size="sm"
                          placeholder={`${column.header} 필터`}
                          value={filters[column.accessor] || ''}
                          onChange={(e) => handleFilterChange(column.accessor, e.target.value)}
                        />
                      </Box>
                    ))}
                </MenuList>
              </Menu>
            )}

            {/* 내보내기 */}
            {exportable && (
              <Button
                leftIcon={<DownloadIcon size={16} />}
                size="sm"
                variant="outline"
                onClick={onExport}
              >
                내보내기
              </Button>
            )}

            {/* 선택된 항목 액션 */}
            {selectedRows.size > 0 && (
              <Badge colorScheme="primary" fontSize="sm" px={2} py={1}>
                {selectedRows.size}개 선택됨
              </Badge>
            )}
          </HStack>
        </Flex>
      </CardHeader>

      {/* 테이블 */}
      <CardBody pt={0}>
        <TableContainer>
          <Table variant="simple" size="sm">
            <Thead bg={headerBg}>
              <Tr>
                {/* 전체 선택 체크박스 */}
                {selectable && (
                  <Th width="40px">
                    <Checkbox
                      isChecked={selectedRows.size === paginatedData.length && paginatedData.length > 0}
                      isIndeterminate={selectedRows.size > 0 && selectedRows.size < paginatedData.length}
                      onChange={(e) => handleSelectAll(e.target.checked)}
                      colorScheme="primary"
                    />
                  </Th>
                )}

                {/* 컬럼 헤더 */}
                {columns.map((column) => (
                  <Th
                    key={column.accessor}
                    cursor={column.sortable ? 'pointer' : 'default'}
                    onClick={() => column.sortable && handleSort(column.accessor)}
                    _hover={column.sortable ? { bg: hoverBg } : {}}
                    position="relative"
                    width={column.width}
                  >
                    <HStack spacing={1} justify="space-between">
                      <Text>{column.header}</Text>
                      {column.sortable && (
                        <Box>
                          {sortConfig.key === column.accessor ? (
                            sortConfig.direction === 'asc' ? (
                              <ChevronUpIcon size={14} />
                            ) : (
                              <ChevronDownIcon size={14} />
                            )
                          ) : (
                            <ChevronUpIcon size={14} opacity={0.3} />
                          )}
                        </Box>
                      )}
                    </HStack>
                  </Th>
                ))}

                {/* 액션 컬럼 */}
                <Th width="60px">액션</Th>
              </Tr>
            </Thead>

            <Tbody>
              {paginatedData.map((row, index) => (
                <Tr
                  key={row.id || index}
                  _hover={{ bg: hoverBg }}
                  cursor={onRowClick ? 'pointer' : 'default'}
                  onClick={() => onRowClick?.(row)}
                >
                  {/* 행 선택 체크박스 */}
                  {selectable && (
                    <Td>
                      <Checkbox
                        isChecked={selectedRows.has(row.id)}
                        onChange={(e) => handleRowSelect(row.id, e.target.checked)}
                        colorScheme="primary"
                        onClick={(e) => e.stopPropagation()}
                      />
                    </Td>
                  )}

                  {/* 데이터 셀 */}
                  {columns.map((column) => (
                    <Td key={column.accessor}>
                      {column.render ? (
                        column.render(row[column.accessor], row)
                      ) : (
                        <Text noOfLines={1}>{row[column.accessor]}</Text>
                      )}
                    </Td>
                  ))}

                  {/* 액션 메뉴 */}
                  <Td>
                    <Menu>
                      <MenuButton
                        as={IconButton}
                        icon={<MoreVerticalIcon size={16} />}
                        variant="ghost"
                        size="sm"
                        onClick={(e) => e.stopPropagation()}
                      />
                      <MenuList>
                        <MenuItem>보기</MenuItem>
                        <MenuItem>수정</MenuItem>
                        <MenuItem color="red.500">삭제</MenuItem>
                      </MenuList>
                    </Menu>
                  </Td>
                </Tr>
              ))}
            </Tbody>
          </Table>
        </TableContainer>

        {/* 빈 상태 */}
        {paginatedData.length === 0 && (
          <Box textAlign="center" py={12}>
            <Text color="gray.500" fontSize="lg">
              데이터가 없습니다
            </Text>
            <Text color="gray.400" fontSize="sm" mt={1}>
              검색 조건을 변경해보세요
            </Text>
          </Box>
        )}

        {/* 페이지네이션 */}
        {sortedData.length > pageSize && (
          <Box mt={6}>
            <Pagination
              currentPage={currentPage}
              totalCount={sortedData.length}
              pageSize={pageSize}
              onPageChange={setCurrentPage}
            />
          </Box>
        )}
      </CardBody>
    </Card>
  );
};

export default DataTable;
```

### 4.6 사용 예시 - 사용자 관리 페이지

```jsx
// pages/UserManagementPage.jsx
import { useState, useEffect } from 'react';
import { useSelector, useDispatch } from 'react-redux';
import {
  Container,
  VStack,
  HStack,
  Heading,
  Text,
  Button,
  Avatar,
  Badge,
  useDisclosure,
  useToast,
} from '@chakra-ui/react';
import { PlusIcon, UserIcon } from 'lucide-react';
import DataTable from '../components/DataTable';
import UserModal from '../components/UserModal';
import { fetchUsers, deleteUser } from '../store/slices/userSlice';

const UserManagementPage = () => {
  const dispatch = useDispatch();
  const toast = useToast();
  const { isOpen, onOpen, onClose } = useDisclosure();
  
  const { users, loading, error } = useSelector(state => state.users);
  const [selectedUser, setSelectedUser] = useState(null);

  useEffect(() => {
    dispatch(fetchUsers());
  }, [dispatch]);

  // 테이블 컬럼 정의
  const columns = [
    {
      header: '사용자',
      accessor: 'name',
      sortable: true,
      render: (value, row) => (
        <HStack spacing={3}>
          <Avatar size="sm" name={row.name} src={row.avatar} />
          <VStack align="start" spacing={0}>
            <Text fontWeight="medium">{row.name}</Text>
            <Text fontSize="xs" color="gray.500">{row.email}</Text>
          </VStack>
        </HStack>
      ),
    },
    {
      header: '역할',
      accessor: 'role',
      sortable: true,
      filterable: true,
      render: (value) => (
        <Badge
          colorScheme={
            value === 'admin' ? 'red' :
            value === 'manager' ? 'blue' : 'gray'
          }
          variant="subtle"
        >
          {value === 'admin' ? '관리자' :
           value === 'manager' ? '매니저' : '사용자'}
        </Badge>
      ),
    },
    {
      header: '상태',
      accessor: 'status',
      sortable: true,
      filterable: true,
      render: (value) => (
        <Badge
          colorScheme={value === 'active' ? 'green' : 'red'}
          variant="subtle"
        >
          {value === 'active' ? '활성' : '비활성'}
        </Badge>
      ),
    },
    {
      header: '마지막 로그인',
      accessor: 'lastLogin',
      sortable: true,
      render: (value) => (
        <Text fontSize="sm">
          {value ? new Date(value).toLocaleDateString('ko-KR') : '-'}
        </Text>
      ),
    },
    {
      header: '가입일',
      accessor: 'createdAt',
      sortable: true,
      render: (value) => (
        <Text fontSize="sm">
          {new Date(value).toLocaleDateString('ko-KR')}
        </Text>
      ),
    },
  ];

  // 사용자 편집
  const handleEditUser = (user) => {
    setSelectedUser(user);
    onOpen();
  };

  // 사용자 삭제
  const handleDeleteUser = async (userId) => {
    try {
      await dispatch(deleteUser(userId)).unwrap();
      toast({
        title: '사용자 삭제 완료',
        status: 'success',
        duration: 3000,
      });
    } catch (error) {
      toast({
        title: '삭제 실패',
        description: error.message,
        status: 'error',
        duration: 5000,
      });
    }
  };

  // 새 사용자 추가
  const handleAddUser = () => {
    setSelectedUser(null);
    onOpen();
  };

  // 데이터 내보내기
  const handleExport = () => {
    // CSV 내보내기 로직
    const csvContent = [
      ['이름', '이메일', '역할', '상태', '가입일'],
      ...users.map(user => [
        user.name,
        user.email,
        user.role,
        user.status,
        new Date(user.createdAt).toLocaleDateString('ko-KR')
      ])
    ]
      .map(row => row.join(','))
      .join('\n');

    const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' });
    const link = document.createElement('a');
    link.href = URL.createObjectURL(blob);
    link.download = 'users.csv';
    link.click();
  };

  return (
    <Container maxW="container.xl" py={8}>
      <VStack spacing={6} align="stretch">
        {/* 페이지 헤더 */}
        <HStack justify="space-between" align="start">
          <VStack align="start" spacing={1}>
            <Heading size="xl">사용자 관리</Heading>
            <Text color="gray.600">
              시스템 사용자를 관리하고 권한을 설정하세요.
            </Text>
          </VStack>
          
          <Button
            leftIcon={<PlusIcon size={16} />}
            colorScheme="primary"
            onClick={handleAddUser}
          >
            사용자 추가
          </Button>
        </HStack>

        {/* 사용자 테이블 */}
        <DataTable
          data={users}
          columns={columns}
          loading={loading}
          error={error}
          onRowClick={handleEditUser}
          selectable={true}
          searchable={true}
          filterable={true}
          exportable={true}
          onExport={handleExport}
          pageSize={15}
        />
      </VStack>

      {/* 사용자 편집/추가 모달 */}
      <UserModal
        isOpen={isOpen}
        onClose={onClose}
        user={selectedUser}
        onSave={() => {
          onClose();
          dispatch(fetchUsers());
        }}
      />
    </Container>
  );
};

export default UserManagementPage;
```

---

## 5. 성능 최적화 가이드

### 5.1 번들 크기 최적화
```jsx
// 개별 컴포넌트 import (권장)
import { Button, Box, Text } from '@chakra-ui/react';

// 전체 라이브러리 import (지양)
import * as ChakraUI from '@chakra-ui/react';
```

### 5.2 테마 최적화
```js
// 사용하지 않는 컴포넌트 스타일 제거
const theme = extendTheme({
  components: {
    // 사용하는 컴포넌트만 정의
    Button: { /* 스타일 정의 */ },
    Input: { /* 스타일 정의 */ },
  }
});
```

### 5.3 렌더링 최적화
```jsx
// React.memo로 불필요한 리렌더링 방지
const OptimizedCard = React.memo(({ data }) => {
  return (
    <Card>
      <CardBody>{data.content}</CardBody>
    </Card>
  );
});

// useCallback으로 함수 메모화
const handleClick = useCallback((id) => {
  // 클릭 처리 로직
}, []);

// useMemo로 계산 값 메모화
const expensiveValue = useMemo(() => {
  return data.reduce((acc, item) => acc + item.value, 0);
}, [data]);
```

---

## 6. 접근성(A11y) 가이드

### 6.1 키보드 네비게이션
```jsx
// 포커스 관리
const FocusableComponent = () => {
  const initialRef = useRef();
  
  return (
    <Modal isOpen={isOpen} initialFocusRef={initialRef}>
      <ModalContent>
        <Input ref={initialRef} placeholder="자동 포커스" />
      </ModalContent>
    </Modal>
  );
};

// Skip Link 구현
const SkipLink = () => (
  <Box
    as="a"
    href="#main-content"
    position="absolute"
    left="-9999px"
    _focus={{
      left: "6px",
      top: "6px",
      zIndex: 9999,
      p: 2,
      bg: "primary.500",
      color: "white",
    }}
  >
    메인 콘텐츠로 건너뛰기
  </Box>
);
```

### 6.2 스크린 리더 지원
```jsx
// ARIA 레이블과 설명
<Button
  aria-label="사용자 프로필 메뉴 열기"
  aria-describedby="profile-menu-desc"
>
  <Avatar />
</Button>
<VisuallyHidden id="profile-menu-desc">
  프로필 설정 및 로그아웃 옵션
</VisuallyHidden>

// 동적 콘텐츠 알림
const [announcement, setAnnouncement] = useState('');

const handleSave = () => {
  // 저장 로직
  setAnnouncement('데이터가 성공적으로 저장되었습니다');
};

return (
  <>
    <Button onClick={handleSave}>저장</Button>
    <Box
      aria-live="polite"
      aria-atomic="true"
      position="absolute"
      left="-10000px"
      width="1px"
      height="1px"
      overflow="hidden"
    >
      {announcement}
    </Box>
  </>
);
```

### 6.3 색상 대비 및 시각적 표시
```jsx
// 색상에만 의존하지 않는 상태 표시
const StatusIndicator = ({ status }) => (
  <HStack>
    <Box
      w="8px"
      h="8px"
      borderRadius="full"
      bg={status === 'success' ? 'green.500' : 'red.500'}
    />
    <Text>
      {status === 'success' ? '✓ 성공' : '✗ 실패'}
    </Text>
  </HStack>
);

// 고대비 모드 지원
const HighContrastButton = (props) => (
  <Button
    {...props}
    _hover={{
      outline: '2px solid',
      outlineColor: 'primary.500',
    }}
    _focus={{
      boxShadow: '0 0 0 3px rgba(66, 153, 225, 0.6)',
    }}
  />
);
```

---

## 7. 다크 모드 구현 가이드

### 7.1 컬러 모드 설정
```jsx
// App.jsx에서 ColorModeScript 추가
import { ColorModeScript } from '@chakra-ui/react';

function App() {
  return (
    <>
      <ColorModeScript initialColorMode={theme.config.initialColorMode} />
      <ChakraProvider theme={theme}>
        {/* 앱 콘텐츠 */}
      </ChakraProvider>
    </>
  );
}

// 테마에서 다크 모드 설정
const config = {
  initialColorMode: 'light',
  useSystemColorMode: true, // 시스템 설정 따라가기
};

const theme = extendTheme({ config });
```

### 7.2 다크 모드 대응 컴포넌트
```jsx
// useColorModeValue 훅 활용
const DarkModeCard = ({ children }) => {
  const bg = useColorModeValue('white', 'gray.800');
  const borderColor = useColorModeValue('gray.200', 'gray.600');
  const textColor = useColorModeValue('gray.800', 'white');

  return (
    <Box
      bg={bg}
      borderColor={borderColor}
      color={textColor}
      border="1px solid"
      borderRadius="md"
      p={4}
    >
      {children}
    </Box>
  );
};

// 다크 모드 토글 버튼
const ColorModeToggle = () => {
  const { colorMode, toggleColorMode } = useColorMode();
  
  return (
    <IconButton
      aria-label="다크모드 토글"
      icon={colorMode === 'light' ? <MoonIcon /> : <SunIcon />}
      onClick={toggleColorMode}
      variant="ghost"
    />
  );
};
```

### 7.3 이미지 및 아이콘 다크 모드 대응
```jsx
// 다크 모드용 이미지 분기
const ResponsiveImage = ({ lightSrc, darkSrc, alt, ...props }) => {
  const src = useColorModeValue(lightSrc, darkSrc);
  
  return <Image src={src} alt={alt} {...props} />;
};

// 아이콘 색상 자동 조정
const ThemedIcon = ({ icon: IconComponent, ...props }) => {
  const color = useColorModeValue('gray.600', 'gray.300');
  
  return <Icon as={IconComponent} color={color} {...props} />;
};
```

---

## 8. 애니메이션 및 모션 가이드

### 8.1 Framer Motion 통합
```jsx
// 페이지 전환 애니메이션
import { motion } from 'framer-motion';

const MotionBox = motion(Box);

const PageTransition = ({ children }) => (
  <MotionBox
    initial={{ opacity: 0, y: 20 }}
    animate={{ opacity: 1, y: 0 }}
    exit={{ opacity: 0, y: -20 }}
    transition={{ duration: 0.3 }}
  >
    {children}
  </MotionBox>
);

// 스태거 애니메이션
const StaggeredList = ({ items }) => {
  const containerVariants = {
    hidden: { opacity: 0 },
    visible: {
      opacity: 1,
      transition: {
        staggerChildren: 0.1
      }
    }
  };

  const itemVariants = {
    hidden: { y: 20, opacity: 0 },
    visible: { y: 0, opacity: 1 }
  };

  return (
    <MotionBox
      variants={containerVariants}
      initial="hidden"
      animate="visible"
    >
      {items.map((item, index) => (
        <MotionBox
          key={index}
          variants={itemVariants}
          whileHover={{ scale: 1.05 }}
          whileTap={{ scale: 0.95 }}
        >
          <Card>{item.content}</Card>
        </MotionBox>
      ))}
    </MotionBox>
  );
};
```

### 8.2 로딩 애니메이션
```jsx
// 커스텀 스피너
const CustomSpinner = () => (
  <MotionBox
    animate={{ rotate: 360 }}
    transition={{ duration: 1, repeat: Infinity, ease: "linear" }}
  >
    <Spinner size="xl" color="primary.500" thickness="4px" />
  </MotionBox>
);

// 펄스 애니메이션
const PulseBox = ({ children, ...props }) => (
  <MotionBox
    animate={{ scale: [1, 1.05, 1] }}
    transition={{ duration: 2, repeat: Infinity }}
    {...props}
  >
    {children}
  </MotionBox>
);

// 스켈레톤 로딩 with 애니메이션
const AnimatedSkeleton = () => (
  <MotionBox
    animate={{ opacity: [0.4, 1, 0.4] }}
    transition={{ duration: 1.5, repeat: Infinity }}
  >
    <Skeleton height="20px" />
  </MotionBox>
);
```

---

## 9. 에러 처리 및 피드백 시스템

### 9.1 에러 바운더리
```jsx
// React Error Boundary
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false, error: null };
  }

  static getDerivedStateFromError(error) {
    return { hasError: true, error };
  }

  componentDidCatch(error, errorInfo) {
    console.error('Error caught by boundary:', error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      return (
        <Container maxW="md" py={12}>
          <VStack spacing={6} textAlign="center">
            <Box fontSize="6xl">😵</Box>
            <Heading size="lg">문제가 발생했습니다</Heading>
            <Text color="gray.600">
              예상치 못한 오류가 발생했습니다. 페이지를 새로고침해주세요.
            </Text>
            <Button
              colorScheme="primary"
              onClick={() => window.location.reload()}
            >
              새로고침
            </Button>
          </VStack>
        </Container>
      );
    }

    return this.props.children;
  }
}
```

### 9.2 토스트 시스템
```jsx
// 커스텀 토스트 훅
const useCustomToast = () => {
  const toast = useToast();

  const showSuccess = (title, description) => {
    toast({
      title,
      description,
      status: 'success',
      duration: 3000,
      isClosable: true,
      position: 'top-right',
    });
  };

  const showError = (title, description) => {
    toast({
      title,
      description,
      status: 'error',
      duration: 5000,
      isClosable: true,
      position: 'top-right',
    });
  };

  const showWarning = (title, description) => {
    toast({
      title,
      description,
      status: 'warning',
      duration: 4000,
      isClosable: true,
      position: 'top-right',
    });
  };

  return { showSuccess, showError, showWarning };
};

// 사용 예시
const MyComponent = () => {
  const { showSuccess, showError } = useCustomToast();

  const handleSave = async () => {
    try {
      await saveData();
      showSuccess('저장 완료', '데이터가 성공적으로 저장되었습니다.');
    } catch (error) {
      showError('저장 실패', error.message);
    }
  };

  return <Button onClick={handleSave}>저장</Button>;
};
```

### 9.3 폼 에러 처리
```jsx
// 실시간 폼 검증
const ValidatedInput = ({ name, label, rules, ...props }) => {
  const { register, formState: { errors, touchedFields } } = useFormContext();
  
  const error = errors[name];
  const isTouched = touchedFields[name];
  const isValid = isTouched && !error;

  return (
    <FormControl isInvalid={!!error}>
      <FormLabel>{label}</FormLabel>
      <InputGroup>
        <Input
          {...register(name, rules)}
          {...props}
          borderColor={
            error ? 'red.300' : 
            isValid ? 'green.300' : 
            'gray.200'
          }
        />
        {isValid && (
          <InputRightElement>
            <CheckIcon color="green.500" />
          </InputRightElement>
        )}
      </InputGroup>
      <FormErrorMessage>{error?.message}</FormErrorMessage>
    </FormControl>
  );
};
```

---

## 10. 테스팅 가이드

### 10.1 컴포넌트 테스트
```jsx
// 기본 컴포넌트 테스트
import { render, screen, fireEvent } from '@testing-library/react';
import { ChakraProvider } from '@chakra-ui/react';
import Button from './Button';

const renderWithChakra = (component) => {
  return render(
    <ChakraProvider>
      {component}
    </ChakraProvider>
  );
};

describe('Button Component', () => {
  test('버튼이 올바르게 렌더링된다', () => {
    renderWithChakra(<Button>Click me</Button>);
    expect(screen.getByRole('button')).toBeInTheDocument();
  });

  test('클릭 이벤트가 올바르게 작동한다', () => {
    const handleClick = jest.fn();
    renderWithChakra(<Button onClick={handleClick}>Click me</Button>);
    
    fireEvent.click(screen.getByRole('button'));
    expect(handleClick).toHaveBeenCalledTimes(1);
  });
});
```

### 10.2 접근성 테스트
```jsx
// 접근성 테스트
import { axe, toHaveNoViolations } from 'jest-axe';
expect.extend(toHaveNoViolations);

test('접근성 위반이 없어야 한다', async () => {
  const { container } = renderWithChakra(<MyComponent />);
  const results = await axe(container);
  expect(results).toHaveNoViolations();
});
```

---

## 11. 배포 최적화

### 11.1 빌드 최적화
```js
// vite.config.js
export default defineConfig({
  build: {
    rollupOptions: {
      output: {
        manualChunks: {
          vendor: ['react', 'react-dom'],
          chakra: ['@chakra-ui/react', '@emotion/react', '@emotion/styled'],
          utils: ['lodash', 'date-fns'],
        },
      },
    },
    chunkSizeWarningLimit: 1000,
  },
  optimizeDeps: {
    include: ['@chakra-ui/react', '@emotion/react', '@emotion/styled'],
  },
});
```

### 11.2 환경별 설정
```jsx
// 환경별 테마 설정
const getTheme = () => {
  const baseTheme = {
    colors: { /* 기본 색상 */ },
    components: { /* 기본 컴포넌트 */ },
  };

  if (process.env.NODE_ENV === 'development') {
    return extendTheme({
      ...baseTheme,
      config: {
        initialColorMode: 'light',
        useSystemColorMode: true,
      },
    });
  }

  return extendTheme({
    ...baseTheme,
    config: {
      initialColorMode: 'light',
      useSystemColorMode: false,
    },
  });
};
```

---

## 12. 실무 팁 및 베스트 프랙티스

### 12.1 컴포넌트 문서화
```jsx
// PropTypes를 활용한 문서화
import PropTypes from 'prop-types';

/**
 * 사용자 카드 컴포넌트
 * @param {Object} user - 사용자 정보
 * @param {Function} onEdit - 편집 버튼 클릭 핸들러
 * @param {Function} onDelete - 삭제 버튼 클릭 핸들러
 * @param {boolean} isLoading - 로딩 상태
 */
const UserCard = ({ user, onEdit, onDelete, isLoading }) => {
  // 컴포넌트 구현
};

UserCard.propTypes = {
  user: PropTypes.shape({
    id: PropTypes.oneOfType([PropTypes.string, PropTypes.number]).isRequired,
    name: PropTypes.string.isRequired,
    email: PropTypes.string.isRequired,
    avatar: PropTypes.string,
  }).isRequired,
  onEdit: PropTypes.func.isRequired,
  onDelete: PropTypes.func.isRequired,
  isLoading: PropTypes.bool,
};

UserCard.defaultProps = {
  isLoading: false,
};
```

### 12.2 성능 모니터링
```jsx
// React DevTools Profiler 활용
import { Profiler } from 'react';

const onRenderCallback = (id, phase, actualDuration) => {
  if (process.env.NODE_ENV === 'development') {
    console.log(`${id} ${phase} phase: ${actualDuration}ms`);
  }
};

const App = () => (
  <Profiler id="App" onRender={onRenderCallback}>
    <ChakraProvider theme={theme}>
      <Router>
        <Routes>
          {/* 라우트 정의 */}
        </Routes>
      </Router>
    </ChakraProvider>
  </Profiler>
);
```

### 12.3 유지보수성 향상
```jsx
// 컴포넌트 분리 패턴
// components/UserCard/index.js
export { default } from './UserCard';

// components/UserCard/UserCard.jsx
export { default } from './UserCard';

// components/UserCard/UserCard.stories.js (Storybook)
export default {
  title: 'Components/UserCard',
  component: UserCard,
};

// components/UserCard/UserCard.test.js
// 테스트 코드
```

이 상세 가이드를 통해 Chakra UI를 활용한 전문적이고 확장 가능한 React 애플리케이션을 구축할 수 있습니다. 각 섹션의 예제 코드는 실제 프로덕션 환경에서 바로 활용할 수 있도록 구성되었습니다.