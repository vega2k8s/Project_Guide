# Figma 라이브러리 기반 React 화면 설계 가이드
*체계적인 디자인 시스템 구축을 통한 효율적 개발 워크플로우*

## 1. Figma 라이브러리 설계 전략

### 1.1 라이브러리 구조 설계 원칙

**계층적 컴포넌트 시스템**
- **Atoms (원자)**: 가장 기본적인 UI 요소
  - Button, Input, Icon, Typography, Color Tokens
  - 더 이상 분해할 수 없는 최소 단위
  - 모든 상위 컴포넌트의 기반이 되는 요소

- **Molecules (분자)**: 원자들의 조합
  - Search Bar (Input + Button + Icon)
  - Form Field (Label + Input + Error Message)
  - Navigation Item (Icon + Text + Badge)
  - 특정 기능을 수행하는 의미있는 조합

- **Organisms (유기체)**: 분자들의 복합체
  - Header (Logo + Navigation + User Menu)
  - Product Card (Image + Title + Price + Action Button)
  - Data Table (Header + Rows + Pagination)
  - 독립적으로 작동하는 완성된 UI 블록

- **Templates (템플릿)**: 레이아웃 구조
  - Page Layout (Header + Content + Footer)
  - Dashboard Layout (Sidebar + Main + Widget Areas)
  - Modal Layout (Overlay + Container + Actions)
  - 콘텐츠 없는 페이지 구조 정의

**Design Token 시스템**
- **Color Tokens**: Primary, Secondary, Semantic, Neutral 팔레트
- **Typography Tokens**: Font Family, Size, Weight, Line Height 체계
- **Spacing Tokens**: 4px 기반 일관된 간격 시스템
- **Border Radius Tokens**: 컴포넌트별 모서리 둥글기 정의
- **Shadow Tokens**: Elevation 시스템을 위한 그림자 레벨

### 1.2 컴포넌트 변형(Variants) 설계 전략

**상태 기반 변형**
- **Interactive States**: Default, Hover, Active, Focus, Disabled
- **Size Variants**: XS, SM, MD, LG, XL
- **Theme Variants**: Light, Dark
- **Type Variants**: Primary, Secondary, Tertiary, Destructive

**props 매핑 전략**
- Figma의 Component Properties → React Props 1:1 대응
- Boolean Properties → React Boolean Props
- Instance Swap Properties → React Children 또는 Icon Props
- Text Properties → React String Props

### 1.3 반응형 설계 체계

**Breakpoint 시스템**
- **Mobile First**: 320px부터 시작
- **Tablet**: 768px 이상
- **Desktop**: 1024px 이상
- **Large Desktop**: 1440px 이상

**Auto Layout 활용 전략**
- **Flexible Containers**: Hug Contents vs Fill Container
- **Direction Control**: Horizontal vs Vertical Stacking
- **Gap System**: 일관된 간격 시스템
- **Padding System**: 컴포넌트 내부 여백 표준화

---

## 2. 라이브러리별 설계 접근법

### 2.1 Material Design 기반 설계

**Material UI (MUI) 호환 설계**
- **Material Design 3 (M3) 원칙 준수**
  - Dynamic Color System 활용
  - Elevation을 통한 계층 표현
  - Motion과 State Layer 고려

- **Component Anatomy 매핑**
  - Container → MUI Box/Paper 컴포넌트
  - Content → Typography 컴포넌트
  - Actions → Button/IconButton 컴포넌트
  - Feedback → Alert/Snackbar 컴포넌트

- **Theme Provider 고려사항**
  - Custom Theme 토큰을 Figma Variables로 정의
  - Palette, Typography, Spacing 일관성 유지
  - Component Override 최소화를 위한 표준 준수

### 2.2 Chakra UI 기반 설계

**Simple, Modular, Accessible 철학 반영**
- **Style Props 시스템 호환**
  - Margin, Padding → m, p props 매핑
  - Color → bg, color props 매핑
  - Size → w, h props 매핑

- **Compound Components 설계**
  - Modal → Modal + ModalOverlay + ModalContent + ModalHeader...
  - Accordion → Accordion + AccordionItem + AccordionButton...
  - Menu → Menu + MenuButton + MenuList + MenuItem...

### 2.3 Ant Design 기반 설계

**Enterprise-Grade UI 고려사항**
- **Data Dense Interface 최적화**
  - 테이블, 폼, 대시보드 중심 설계
  - 정보 밀도와 가독성 균형
  - 복잡한 인터랙션 패턴 지원

- **Form Design System**
  - Form.Item 구조 반영
  - Validation State 시각화
  - Field Grouping과 Layout 패턴

---

## 3. 화면 설계 워크플로우

### 3.1 설계 단계별 프로세스

**1단계: 리서치 및 기획**
- **사용자 여정 매핑**: 주요 태스크 플로우 정의
- **정보 구조 설계**: 콘텐츠 우선순위와 계층 구조
- **기능 요구사항 분석**: 필요한 컴포넌트와 인터랙션 식별

**2단계: 와이어프레임 설계**
- **Layout Grid 정의**: 12컬럼 또는 16컬럼 그리드 시스템
- **Content Blocks 배치**: 주요 콘텐츠 영역 구분
- **Navigation Flow**: 페이지 간 연결과 사용자 동선

**3단계: Visual Design**
- **Design Token 적용**: 색상, 타이포그래피, 간격 체계화
- **Component Library 활용**: 기존 컴포넌트 재사용 우선
- **Brand Identity 반영**: 브랜드 가이드라인과 일치성 확보

**4단계: 프로토타이핑**
- **Interactive Prototype**: 주요 사용자 플로우 시연
- **Micro-interactions**: 세부 인터랙션과 피드백 정의
- **Error Handling**: 예외 상황과 에러 상태 설계

### 3.2 컴포넌트 문서화 전략

**Component Specification**
- **Purpose**: 컴포넌트 사용 목적과 적용 상황
- **Variants**: 모든 변형과 상태 정의
- **Props**: 속성과 기본값, 필수/선택 구분
- **Usage Guidelines**: 사용법과 제약사항
- **Accessibility Notes**: 접근성 고려사항

**Design-Dev Handoff 최적화**
- **Auto Layout 표준화**: 개발자가 이해하기 쉬운 구조
- **Naming Convention**: 일관된 네이밍으로 혼란 방지
- **Asset Export**: 최적화된 이미지와 아이콘 제공

---

## 4. 반응형 설계 전략

### 4.1 모바일 우선 설계 원칙

**Progressive Enhancement**
- **Core Functionality**: 모든 디바이스에서 작동하는 기본 기능
- **Enhanced Experience**: 큰 화면에서 추가되는 기능과 콘텐츠
- **Touch-First Interaction**: 터치 인터페이스 우선 고려

**Content Prioritization**
- **Primary Actions**: 가장 중요한 액션을 쉽게 접근 가능한 위치
- **Secondary Content**: 접기/펼치기 또는 별도 화면으로 처리
- **Progressive Disclosure**: 정보를 단계적으로 노출

### 4.2 브레이크포인트 전환 전략

**Layout Transformation**
- **Navigation Pattern**: 탭 → 사이드바 → 상단 네비게이션
- **Content Layout**: 단일 컬럼 → 다중 컬럼 → 복합 레이아웃
- **Typography Scale**: 모바일 최적화 → 데스크톱 확장

**Component Adaptation**
- **Card Layout**: 리스트 뷰 → 그리드 뷰
- **Table Design**: 카드 형태 → 전통적 테이블
- **Form Layout**: 세로 배치 → 가로 배치

---

## 5. 사용자 경험 설계 고려사항

### 5.1 인터랙션 설계 원칙

**Feedback Systems**
- **Immediate Feedback**: 사용자 액션에 대한 즉각적 반응 (0.1초 내)
- **Progress Indication**: 로딩과 진행 상황의 명확한 표시
- **Error Recovery**: 오류 발생 시 복구 방법 안내

**State Management**
- **Loading States**: 스켈레톤, 스피너, 진행률 표시
- **Empty States**: 빈 화면에 대한 안내와 액션 유도
- **Error States**: 사용자 친화적 오류 메시지와 해결 방안

### 5.2 접근성 설계 고려사항

**Universal Design**
- **Color Contrast**: WCAG 2.1 AA 레벨 대비비 준수 (4.5:1 이상)
- **Typography**: 최소 16px 본문 크기, 명확한 계층 구조
- **Touch Target**: 최소 44px × 44px 터치 영역 확보

**Assistive Technology**
- **Screen Reader**: 의미있는 레이블과 구조적 마크업
- **Keyboard Navigation**: 논리적 탭 순서와 포커스 표시
- **Voice Control**: 음성 명령으로 조작 가능한 인터페이스

---

## 6. 실제 설계 예시

### 6.1 E-commerce 제품 목록 페이지 설계

**페이지 구조 분석**
```
Header (Organism)
├── Logo (Atom)
├── Navigation (Molecule)
├── Search Bar (Molecule)
└── User Menu (Molecule)

Filter Sidebar (Organism)
├── Category Filter (Molecule)
├── Price Range (Molecule)
└── Brand Filter (Molecule)

Product Grid (Organism)
├── Product Card (Molecule) × N
│   ├── Product Image (Atom)
│   ├── Product Info (Molecule)
│   └── Action Buttons (Molecule)
└── Pagination (Molecule)

Footer (Organism)
```

**컴포넌트 변형 정의**
- **Product Card Variants**
  - Size: Compact, Standard, Detailed
  - State: Default, Hover, Wishlist, Out of Stock
  - Layout: Grid View, List View

### 6.2 대시보드 페이지 설계

**레이아웃 패턴**
```
App Shell (Template)
├── Top Bar (Organism)
├── Side Navigation (Organism)
├── Main Content (Template)
│   ├── Stats Cards (Organism)
│   ├── Charts Section (Organism)
│   └── Data Table (Organism)
└── Notification Panel (Organism)
```

**반응형 적응 전략**
- **Desktop (1024px+)**: 사이드바 + 메인 콘텐츠
- **Tablet (768px-1023px)**: 접을 수 있는 사이드바
- **Mobile (~767px)**: 하단 탭 네비게이션

---

## 7. 실제 코드 구현 예시

### 7.1 Design Token 시스템 구현

```javascript
// tokens/colors.js - Figma Variables에서 추출
export const colors = {
  // Primary Palette
  primary: {
    50: '#f0f9ff',
    100: '#e0f2fe',
    500: '#0ea5e9',  // Main brand color
    600: '#0284c7',  // Hover state
    700: '#0369a1',  // Active state
    900: '#0c4a6e',  // Text on light bg
  },
  
  // Semantic Colors
  semantic: {
    success: '#10b981',
    warning: '#f59e0b', 
    error: '#ef4444',
    info: '#3b82f6',
  },
  
  // Neutral Palette
  neutral: {
    0: '#ffffff',
    50: '#f8fafc',
    100: '#f1f5f9',
    500: '#64748b',
    900: '#0f172a',
  }
};

// tokens/typography.js
export const typography = {
  fontFamily: {
    primary: ['Inter', 'system-ui', 'sans-serif'],
    mono: ['JetBrains Mono', 'monospace'],
  },
  
  fontSize: {
    xs: '0.75rem',    // 12px
    sm: '0.875rem',   // 14px  
    base: '1rem',     // 16px
    lg: '1.125rem',   // 18px
    xl: '1.25rem',    // 20px
    '2xl': '1.5rem',  // 24px
    '3xl': '1.875rem', // 30px
  },
  
  fontWeight: {
    normal: '400',
    medium: '500', 
    semibold: '600',
    bold: '700',
  },
  
  lineHeight: {
    tight: '1.25',
    normal: '1.5',
    relaxed: '1.75',
  }
};

// tokens/spacing.js
export const spacing = {
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
};
```

### 7.2 Atomic Design 기반 컴포넌트 구현

```jsx
// components/atoms/Button/Button.jsx
import React from 'react';
import PropTypes from 'prop-types';
import { colors, spacing } from '../../../tokens';
import './Button.css';

const Button = ({
  children,
  variant = 'primary',
  size = 'medium',
  disabled = false,
  loading = false,
  icon,
  onClick,
  type = 'button',
  fullWidth = false,
  ...rest
}) => {
  const getButtonStyles = () => {
    const baseStyles = {
      fontFamily: 'Inter, system-ui, sans-serif',
      fontWeight: '500',
      borderRadius: '0.5rem',
      border: 'none',
      cursor: disabled || loading ? 'not-allowed' : 'pointer',
      transition: 'all 0.2s ease-in-out',
      display: 'inline-flex',
      alignItems: 'center',
      justifyContent: 'center',
      gap: spacing[2],
      width: fullWidth ? '100%' : 'auto',
      opacity: disabled ? 0.6 : 1,
    };

    // Size variants (Figma Variants → CSS)
    const sizeStyles = {
      small: {
        padding: `${spacing[2]} ${spacing[3]}`,
        fontSize: '0.875rem',
        lineHeight: '1.25',
      },
      medium: {
        padding: `${spacing[3]} ${spacing[4]}`,
        fontSize: '1rem', 
        lineHeight: '1.5',
      },
      large: {
        padding: `${spacing[4]} ${spacing[6]}`,
        fontSize: '1.125rem',
        lineHeight: '1.5',
      },
    };

    // Variant styles (Figma Component Properties → CSS)
    const variantStyles = {
      primary: {
        backgroundColor: colors.primary[500],
        color: colors.neutral[0],
        '&:hover': {
          backgroundColor: colors.primary[600],
        },
        '&:active': {
          backgroundColor: colors.primary[700],
        },
      },
      secondary: {
        backgroundColor: colors.neutral[100],
        color: colors.neutral[900],
        border: `1px solid ${colors.neutral[200]}`,
        '&:hover': {
          backgroundColor: colors.neutral[200],
        },
      },
      outline: {
        backgroundColor: 'transparent',
        color: colors.primary[500],
        border: `1px solid ${colors.primary[500]}`,
        '&:hover': {
          backgroundColor: colors.primary[50],
        },
      },
      ghost: {
        backgroundColor: 'transparent',
        color: colors.primary[500],
        '&:hover': {
          backgroundColor: colors.primary[50],
        },
      },
      destructive: {
        backgroundColor: colors.semantic.error,
        color: colors.neutral[0],
        '&:hover': {
          backgroundColor: '#dc2626',
        },
      },
    };

    return {
      ...baseStyles,
      ...sizeStyles[size],
      ...variantStyles[variant],
    };
  };

  return (
    <button
      type={type}
      style={getButtonStyles()}
      onClick={onClick}
      disabled={disabled || loading}
      className={`button button--${variant} button--${size} ${fullWidth ? 'button--full-width' : ''}`}
      {...rest}
    >
      {loading && (
        <div className="button__spinner" />
      )}
      {icon && !loading && (
        <span className="button__icon">{icon}</span>
      )}
      <span className="button__text">{children}</span>
    </button>
  );
};

Button.propTypes = {
  children: PropTypes.node.isRequired,
  variant: PropTypes.oneOf(['primary', 'secondary', 'outline', 'ghost', 'destructive']),
  size: PropTypes.oneOf(['small', 'medium', 'large']),
  disabled: PropTypes.bool,
  loading: PropTypes.bool,
  icon: PropTypes.node,
  onClick: PropTypes.func,
  type: PropTypes.oneOf(['button', 'submit', 'reset']),
  fullWidth: PropTypes.bool,
};

export default Button;
```

### 7.3 Molecule 컴포넌트 - Form Field

```jsx
// components/molecules/FormField/FormField.jsx
import React from 'react';
import PropTypes from 'prop-types';
import { colors, spacing, typography } from '../../../tokens';

const FormField = ({
  label,
  children,
  error,
  helperText,
  required = false,
  disabled = false,
  layout = 'vertical', // vertical, horizontal
}) => {
  const fieldId = React.useId();

  const getLabelStyles = () => ({
    display: 'block',
    marginBottom: layout === 'vertical' ? spacing[2] : 0,
    marginRight: layout === 'horizontal' ? spacing[4] : 0,
    fontSize: typography.fontSize.sm,
    fontWeight: typography.fontWeight.medium,
    color: disabled ? colors.neutral[400] : colors.neutral[700],
    minWidth: layout === 'horizontal' ? '120px' : 'auto',
  });

  const getContainerStyles = () => ({
    display: 'flex',
    flexDirection: layout === 'vertical' ? 'column' : 'row',
    alignItems: layout === 'horizontal' ? 'flex-start' : 'stretch',
    marginBottom: spacing[4],
  });

  const getInputContainerStyles = () => ({
    flex: layout === 'horizontal' ? 1 : 'none',
    display: 'flex',
    flexDirection: 'column',
  });

  const getHelperTextStyles = (isError = false) => ({
    marginTop: spacing[1],
    fontSize: typography.fontSize.xs,
    color: isError ? colors.semantic.error : colors.neutral[500],
    lineHeight: typography.lineHeight.normal,
  });

  return (
    <div style={getContainerStyles()}>
      {label && (
        <label htmlFor={fieldId} style={getLabelStyles()}>
          {label}
          {required && (
            <span style={{ color: colors.semantic.error, marginLeft: spacing[1] }}>
              *
            </span>
          )}
        </label>
      )}
      
      <div style={getInputContainerStyles()}>
        {React.cloneElement(children, {
          id: fieldId,
          disabled,
          'aria-invalid': !!error,
          'aria-describedby': error ? `${fieldId}-error` : helperText ? `${fieldId}-helper` : undefined,
        })}
        
        {error && (
          <div
            id={`${fieldId}-error`}
            role="alert"
            style={getHelperTextStyles(true)}
          >
            {error}
          </div>
        )}
        
        {helperText && !error && (
          <div
            id={`${fieldId}-helper`}
            style={getHelperTextStyles(false)}
          >
            {helperText}
          </div>
        )}
      </div>
    </div>
  );
};

FormField.propTypes = {
  label: PropTypes.string,
  children: PropTypes.element.isRequired,
  error: PropTypes.string,
  helperText: PropTypes.string,
  required: PropTypes.bool,
  disabled: PropTypes.bool,
  layout: PropTypes.oneOf(['vertical', 'horizontal']),
};

export default FormField;
```

### 7.4 Organism 컴포넌트 - Product Card

```jsx
// components/organisms/ProductCard/ProductCard.jsx
import React from 'react';
import PropTypes from 'prop-types';
import Button from '../../atoms/Button/Button';
import { colors, spacing } from '../../../tokens';
import { HeartIcon, StarIcon, ShoppingCartIcon } from '../../../icons';

const ProductCard = ({
  product,
  variant = 'standard',
  onAddToCart,
  onToggleWishlist,
  onViewDetails,
  isWishlisted = false,
  layout = 'grid', // grid, list
}) => {
  const getCardStyles = () => ({
    backgroundColor: colors.neutral[0],
    borderRadius: '0.75rem',
    border: `1px solid ${colors.neutral[200]}`,
    overflow: 'hidden',
    transition: 'all 0.2s ease-in-out',
    cursor: 'pointer',
    display: 'flex',
    flexDirection: layout === 'grid' ? 'column' : 'row',
    '&:hover': {
      boxShadow: '0 10px 25px rgba(0, 0, 0, 0.1)',
      transform: 'translateY(-2px)',
    },
  });

  const getImageContainerStyles = () => ({
    position: 'relative',
    width: layout === 'grid' ? '100%' : '200px',
    height: layout === 'grid' ? '200px' : '150px',
    backgroundColor: colors.neutral[50],
    overflow: 'hidden',
  });

  const getContentStyles = () => ({
    padding: spacing[4],
    display: 'flex',
    flexDirection: 'column',
    gap: spacing[3],
    flex: 1,
  });

  const getPriceStyles = () => ({
    display: 'flex',
    alignItems: 'center',
    gap: spacing[2],
  });

  const formatPrice = (price) => {
    return new Intl.NumberFormat('ko-KR', {
      style: 'currency',
      currency: 'KRW',
    }).format(price);
  };

  const renderRating = (rating, reviewCount) => (
    <div style={{ display: 'flex', alignItems: 'center', gap: spacing[1] }}>
      <div style={{ display: 'flex', gap: spacing[0.5] }}>
        {[...Array(5)].map((_, index) => (
          <StarIcon
            key={index}
            size={14}
            color={index < rating ? colors.semantic.warning : colors.neutral[300]}
            filled={index < rating}
          />
        ))}
      </div>
      <span style={{ 
        fontSize: '0.875rem', 
        color: colors.neutral[500],
        marginLeft: spacing[1]
      }}>
        ({reviewCount})
      </span>
    </div>
  );

  return (
    <article style={getCardStyles()} onClick={onViewDetails}>
      {/* 상품 이미지 영역 */}
      <div style={getImageContainerStyles()}>
        <img
          src={product.imageUrl}
          alt={product.name}
          style={{
            width: '100%',
            height: '100%',
            objectFit: 'cover',
          }}
          loading="lazy"
        />
        
        {/* 할인 배지 */}
        {product.discountPercentage > 0 && (
          <div style={{
            position: 'absolute',
            top: spacing[2],
            left: spacing[2],
            backgroundColor: colors.semantic.error,
            color: colors.neutral[0],
            padding: `${spacing[1]} ${spacing[2]}`,
            borderRadius: '0.25rem',
            fontSize: '0.75rem',
            fontWeight: '600',
          }}>
            -{product.discountPercentage}%
          </div>
        )}
        
        {/* 위시리스트 버튼 */}
        <button
          onClick={(e) => {
            e.stopPropagation();
            onToggleWishlist(product.id);
          }}
          style={{
            position: 'absolute',
            top: spacing[2],
            right: spacing[2],
            backgroundColor: colors.neutral[0],
            border: 'none',
            borderRadius: '50%',
            width: '32px',
            height: '32px',
            display: 'flex',
            alignItems: 'center',
            justifyContent: 'center',
            cursor: 'pointer',
            boxShadow: '0 2px 8px rgba(0, 0, 0, 0.1)',
          }}
          aria-label={isWishlisted ? '위시리스트에서 제거' : '위시리스트에 추가'}
        >
          <HeartIcon
            size={16}
            color={isWishlisted ? colors.semantic.error : colors.neutral[400]}
            filled={isWishlisted}
          />
        </button>
      </div>

      {/* 상품 정보 영역 */}
      <div style={getContentStyles()}>
        {/* 브랜드명 */}
        <div style={{
          fontSize: '0.875rem',
          color: colors.neutral[500],
          fontWeight: '500',
        }}>
          {product.brand}
        </div>

        {/* 상품명 */}
        <h3 style={{
          margin: 0,
          fontSize: layout === 'grid' ? '1rem' : '1.125rem',
          fontWeight: '600',
          color: colors.neutral[900],
          lineHeight: '1.4',
          display: '-webkit-box',
          WebkitLineClamp: 2,
          WebkitBoxOrient: 'vertical',
          overflow: 'hidden',
        }}>
          {product.name}
        </h3>

        {/* 평점 */}
        {product.rating > 0 && renderRating(product.rating, product.reviewCount)}

        {/* 가격 */}
        <div style={getPriceStyles()}>
          {product.originalPrice && product.originalPrice > product.price && (
            <span style={{
              fontSize: '0.875rem',
              color: colors.neutral[400],
              textDecoration: 'line-through',
            }}>
              {formatPrice(product.originalPrice)}
            </span>
          )}
          <span style={{
            fontSize: layout === 'grid' ? '1.125rem' : '1.25rem',
            fontWeight: '700',
            color: colors.neutral[900],
          }}>
            {formatPrice(product.price)}
          </span>
        </div>

        {/* 재고 상태 */}
        <div style={{
          padding: `${spacing[1]} ${spacing[2]}`,
          borderRadius: '0.25rem',
          fontSize: '0.75rem',
          fontWeight: '600',
          alignSelf: 'flex-start',
          backgroundColor: product.inStock 
            ? `${colors.semantic.success}15` 
            : `${colors.semantic.error}15`,
          color: product.inStock 
            ? colors.semantic.success 
            : colors.semantic.error,
        }}>
          {product.inStock ? '재고 있음' : '품절'}
        </div>

        {/* 액션 버튼 */}
        <div style={{
          marginTop: 'auto',
          paddingTop: spacing[2],
        }}>
          <Button
            variant="primary"
            size={layout === 'grid' ? 'medium' : 'large'}
            fullWidth={layout === 'grid'}
            disabled={!product.inStock}
            icon={<ShoppingCartIcon size={16} />}
            onClick={(e) => {
              e.stopPropagation();
              onAddToCart(product);
            }}
          >
            {product.inStock ? '장바구니 담기' : '품절'}
          </Button>
        </div>
      </div>
    </article>
  );
};

ProductCard.propTypes = {
  product: PropTypes.shape({
    id: PropTypes.oneOfType([PropTypes.string, PropTypes.number]).isRequired,
    name: PropTypes.string.isRequired,
    brand: PropTypes.string.isRequired,
    price: PropTypes.number.isRequired,
    originalPrice: PropTypes.number,
    discountPercentage: PropTypes.number,
    imageUrl: PropTypes.string.isRequired,
    rating: PropTypes.number,
    reviewCount: PropTypes.number,
    inStock: PropTypes.bool.isRequired,
  }).isRequired,
  variant: PropTypes.oneOf(['compact', 'standard', 'detailed']),
  onAddToCart: PropTypes.func.isRequired,
  onToggleWishlist: PropTypes.func.isRequired,
  onViewDetails: PropTypes.func.isRequired,
  isWishlisted: PropTypes.bool,
  layout: PropTypes.oneOf(['grid', 'list']),
};

export default ProductCard;
```

### 7.5 Template 컴포넌트 - Page Layout

```jsx
// components/templates/PageLayout/PageLayout.jsx
import React from 'react';
import PropTypes from 'prop-types';
import Header from '../../organisms/Header/Header';
import Footer from '../../organisms/Footer/Footer';
import Sidebar from '../../organisms/Sidebar/Sidebar';
import { colors, spacing } from '../../../tokens';

const PageLayout = ({
  children,
  variant = 'default', // default, sidebar, full-width
  sidebarContent,
  headerProps = {},
  footerProps = {},
  containerMaxWidth = '1280px',
}) => {
  const getLayoutStyles = () => ({
    minHeight: '100vh',
    display: 'flex',
    flexDirection: 'column',
    backgroundColor: colors.neutral[50],
  });

  const getMainStyles = () => ({
    flex: 1,
    display: 'flex',
    flexDirection: variant === 'sidebar' ? 'row' : 'column',
  });

  const getContentStyles = () => ({
    flex: 1,
    padding: variant === 'full-width' ? 0 : spacing[6],
    maxWidth: variant === 'full-width' ? '100%' : containerMaxWidth,
    margin: variant === 'full-width' ? 0 : '0 auto',
    width: '100%',
    '@media (max-width: 768px)': {
      padding: spacing[4],
    },
  });

  const getSidebarStyles = () => ({
    width: '280px',
    backgroundColor: colors.neutral[0],
    borderRight: `1px solid ${colors.neutral[200]}`,
    '@media (max-width: 1024px)': {
      display: 'none', // 모바일에서 사이드바 숨김
    },
  });

  return (
    <div style={getLayoutStyles()}>
      <Header {...headerProps} />
      
      <main style={getMainStyles()}>
        {variant === 'sidebar' && sidebarContent && (
          <aside style={getSidebarStyles()}>
            {sidebarContent}
          </aside>
        )}
        
        <div style={getContentStyles()}>
          {children}
        </div>
      </main>
      
      <Footer {...footerProps} />
    </div>
  );
};

PageLayout.propTypes = {
  children: PropTypes.node.isRequired,
  variant: PropTypes.oneOf(['default', 'sidebar', 'full-width']),
  sidebarContent: PropTypes.node,
  headerProps: PropTypes.object,
  footerProps: PropTypes.object,
  containerMaxWidth: PropTypes.string,
};

export default PageLayout;
```

### 7.6 반응형 Grid 시스템 구현

```jsx
// components/layout/Grid/Grid.jsx
import React from 'react';
import PropTypes from 'prop-types';
import { spacing } from '../../../tokens';

const Grid = ({
  children,
  columns = { xs: 1, sm: 2, md: 3, lg: 4, xl: 4 },
  gap = 6,
  className = '',
  ...rest
}) => {
  const getGridStyles = () => ({
    display: 'grid',
    gap: spacing[gap],
    gridTemplateColumns: `repeat(${columns.xs}, 1fr)`,
    width: '100%',
    
    // 반응형 그리드 컬럼
    '@media (min-width: 640px)': {
      gridTemplateColumns: `repeat(${columns.sm || columns.xs}, 1fr)`,
    },
    '@media (min-width: 768px)': {
      gridTemplateColumns: `repeat(${columns.md || columns.sm || columns.xs}, 1fr)`,
    },
    '@media (min-width: 1024px)': {
      gridTemplateColumns: `repeat(${columns.lg || columns.md || columns.sm || columns.xs}, 1fr)`,
    },
    '@media (min-width: 1280px)': {
      gridTemplateColumns: `repeat(${columns.xl || columns.lg || columns.md || columns.sm || columns.xs}, 1fr)`,
    },
  });

  return (
    <div
      style={getGridStyles()}
      className={`grid ${className}`}
      {...rest}
    >
      {children}
    </div>
  );
};

const GridItem = ({
  children,
  span = { xs: 1, sm: 1, md: 1, lg: 1, xl: 1 },
  className = '',
  ...rest
}) => {
  const getItemStyles = () => ({
    gridColumn: `span ${span.xs}`,
    
    '@media (min-width: 640px)': {
      gridColumn: `span ${span.sm || span.xs}`,
    },
    '@media (min-width: 768px)': {
      gridColumn: `span ${span.md || span.sm || span.xs}`,
    },
    '@media (min-width: 1024px)': {
      gridColumn: `span ${span.lg || span.md || span.sm || span.xs}`,
    },
    '@media (min-width: 1280px)': {
      gridColumn: `span ${span.xl || span.lg || span.md || span.sm || span.xs}`,
    },
  });

  return (
    <div
      style={getItemStyles()}
      className={`grid-item ${className}`}
      {...rest}
    >
      {children}
    </div>
  );
};

Grid.propTypes = {
  children: PropTypes.node.isRequired,
  columns: PropTypes.shape({
    xs: PropTypes.number,
    sm: PropTypes.number,
    md: PropTypes.number,
    lg: PropTypes.number,
    xl: PropTypes.number,
  }),
  gap: PropTypes.number,
  className: PropTypes.string,
};

GridItem.propTypes = {
  children: PropTypes.node.isRequired,
  span: PropTypes.shape({
    xs: PropTypes.number,
    sm: PropTypes.number,
    md: PropTypes.number,
    lg: PropTypes.number,
    xl: PropTypes.number,
  }),
  className: PropTypes.string,
};

export { Grid, GridItem };
```

### 7.7 실제 페이지 구현 - 제품 목록 페이지

```jsx
// pages/ProductListPage/ProductListPage.jsx
import React, { useState, useEffect, useMemo } from 'react';
import { useSearchParams } from 'react-router-dom';
import PageLayout from '../../components/templates/PageLayout/PageLayout';
import ProductCard from '../../components/organisms/ProductCard/ProductCard';
import { Grid } from '../../components/layout/Grid/Grid';
import Button from '../../components/atoms/Button/Button';
import FormField from '../../components/molecules/FormField/FormField';
import { colors, spacing } from '../../tokens';
import { 
  FilterIcon, 
  GridIcon, 
  ListIcon, 
  SearchIcon 
} from '../../icons';

const ProductListPage = () => {
  const [searchParams, setSearchParams] = useSearchParams();
  const [products, setProducts] = useState([]);
  const [loading, setLoading] = useState(true);
  const [layout, setLayout] = useState('grid');
  const [filters, setFilters] = useState({
    category: searchParams.get('category') || '',
    priceRange: searchParams.get('priceRange') || '',
    brand: searchParams.get('brand') || '',
    search: searchParams.get('search') || '',
  });

  // 상품 데이터 로딩 (실제로는 API 호출)
  useEffect(() => {
    const loadProducts = async () => {
      setLoading(true);
      try {
        // API 호출 시뮬레이션
        await new Promise(resolve => setTimeout(resolve, 1000));
        
        // 더미 데이터
        const mockProducts = Array.from({ length: 12 }, (_, index) => ({
          id: index + 1,
          name: `상품 ${index + 1}`,
          brand: '브랜드명',
          price: Math.floor(Math.random() * 100000) + 10000,
          originalPrice: Math.floor(Math.random() * 120000) + 50000,
          discountPercentage: Math.floor(Math.random() * 30),
          imageUrl: `https://picsum.photos/300/300?random=${index}`,
          rating: Math.floor(Math.random() * 5) + 1,
          reviewCount: Math.floor(Math.random() * 1000),
          inStock: Math.random() > 0.2,
        }));
        
        setProducts(mockProducts);
      } catch (error) {
        console.error('상품 로딩 실패:', error);
      } finally {
        setLoading(false);
      }
    };

    loadProducts();
  }, [filters]);

  // 필터링된 상품 목록
  const filteredProducts = useMemo(() => {
    return products.filter(product => {
      if (filters.search && !product.name.toLowerCase().includes(filters.search.toLowerCase())) {
        return false;
      }
      // 추가 필터 로직...
      return true;
    });
  }, [products, filters]);

  // 필터 변경 핸들러
  const handleFilterChange = (key, value) => {
    const newFilters = { ...filters, [key]: value };
    setFilters(newFilters);
    
    // URL 업데이트
    const newSearchParams = new URLSearchParams();
    Object.entries(newFilters).forEach(([k, v]) => {
      if (v) newSearchParams.set(k, v);
    });
    setSearchParams(newSearchParams);
  };

  // 상품 액션 핸들러들
  const handleAddToCart = (product) => {
    console.log('장바구니 추가:', product);
    // 실제로는 카트 상태 업데이트
  };

  const handleToggleWishlist = (productId) => {
    console.log('위시리스트 토글:', productId);
    // 실제로는 위시리스트 상태 업데이트
  };

  const handleViewDetails = (product) => {
    console.log('상품 상세 보기:', product);
    // 실제로는 상품 상세 페이지로 이동
  };

  // 사이드바 콘텐츠
  const sidebarContent = (
    <div style={{ padding: spacing[6] }}>
      <h3 style={{ 
        margin: `0 0 ${spacing[6]} 0`,
        fontSize: '1.25rem',
        fontWeight: '600',
        color: colors.neutral[900],
      }}>
        필터
      </h3>

      {/* 검색 */}
      <FormField label="상품 검색">
        <input
          type="text"
          placeholder="상품명을 입력하세요"
          value={filters.search}
          onChange={(e) => handleFilterChange('search', e.target.value)}
          style={{
            width: '100%',
            padding: `${spacing[3]} ${spacing[4]}`,
            border: `1px solid ${colors.neutral[300]}`,
            borderRadius: '0.5rem',
            fontSize: '1rem',
          }}
        />
      </FormField>

      {/* 카테고리 필터 */}
      <FormField label="카테고리">
        <select
          value={filters.category}
          onChange={(e) => handleFilterChange('category', e.target.value)}
          style={{
            width: '100%',
            padding: `${spacing[3]} ${spacing[4]}`,
            border: `1px solid ${colors.neutral[300]}`,
            borderRadius: '0.5rem',
            fontSize: '1rem',
          }}
        >
          <option value="">전체</option>
          <option value="electronics">전자제품</option>
          <option value="clothing">의류</option>
          <option value="books">도서</option>
        </select>
      </FormField>

      {/* 가격 범위 */}
      <FormField label="가격 범위">
        <select
          value={filters.priceRange}
          onChange={(e) => handleFilterChange('priceRange', e.target.value)}
          style={{
            width: '100%',
            padding: `${spacing[3]} ${spacing[4]}`,
            border: `1px solid ${colors.neutral[300]}`,
            borderRadius: '0.5rem',
            fontSize: '1rem',
          }}
        >
          <option value="">전체</option>
          <option value="0-50000">5만원 이하</option>
          <option value="50000-100000">5-10만원</option>
          <option value="100000+">10만원 이상</option>
        </select>
      </FormField>

      {/* 필터 초기화 */}
      <Button
        variant="outline"
        fullWidth
        onClick={() => {
          setFilters({ category: '', priceRange: '', brand: '', search: '' });
          setSearchParams({});
        }}
        style={{ marginTop: spacing[4] }}
      >
        필터 초기화
      </Button>
    </div>
  );

  // 메인 콘텐츠
  const mainContent = (
    <div>
      {/* 페이지 헤더 */}
      <div style={{
        display: 'flex',
        justifyContent: 'space-between',
        alignItems: 'center',
        marginBottom: spacing[8],
        flexWrap: 'wrap',
        gap: spacing[4],
      }}>
        <div>
          <h1 style={{
            margin: 0,
            fontSize: '2rem',
            fontWeight: '700',
            color: colors.neutral[900],
            marginBottom: spacing[2],
          }}>
            전체 상품
          </h1>
          <p style={{
            margin: 0,
            color: colors.neutral[600],
            fontSize: '1.125rem',
          }}>
            {filteredProducts.length}개의 상품을 찾았습니다
          </p>
        </div>

        {/* 레이아웃 토글 */}
        <div style={{
          display: 'flex',
          gap: spacing[2],
          padding: spacing[1],
          backgroundColor: colors.neutral[100],
          borderRadius: '0.5rem',
        }}>
          <Button
            variant={layout === 'grid' ? 'primary' : 'ghost'}
            size="small"
            icon={<GridIcon size={16} />}
            onClick={() => setLayout('grid')}
          >
            격자
          </Button>
          <Button
            variant={layout === 'list' ? 'primary' : 'ghost'}
            size="small"
            icon={<ListIcon size={16} />}
            onClick={() => setLayout('list')}
          >
            목록
          </Button>
        </div>
      </div>

      {/* 상품 목록 */}
      {loading ? (
        <div style={{
          display: 'flex',
          justifyContent: 'center',
          alignItems: 'center',
          height: '400px',
          fontSize: '1.125rem',
          color: colors.neutral[500],
        }}>
          상품을 불러오는 중...
        </div>
      ) : filteredProducts.length === 0 ? (
        <div style={{
          textAlign: 'center',
          padding: spacing[12],
          color: colors.neutral[500],
        }}>
          <h3 style={{ marginBottom: spacing[4] }}>상품이 없습니다</h3>
          <p>다른 검색어나 필터를 시도해보세요.</p>
        </div>
      ) : (
        <Grid
          columns={
            layout === 'grid' 
              ? { xs: 1, sm: 2, md: 2, lg: 3, xl: 4 }
              : { xs: 1, sm: 1, md: 1, lg: 1, xl: 1 }
          }
          gap={6}
        >
          {filteredProducts.map(product => (
            <ProductCard
              key={product.id}
              product={product}
              layout={layout}
              onAddToCart={handleAddToCart}
              onToggleWishlist={handleToggleWishlist}
              onViewDetails={handleViewDetails}
            />
          ))}
        </Grid>
      )}
    </div>
  );

  return (
    <PageLayout
      variant="sidebar"
      sidebarContent={sidebarContent}
      headerProps={{
        showSearch: true,
        onSearch: (term) => handleFilterChange('search', term),
      }}
    >
      {mainContent}
    </PageLayout>
  );
};

export default ProductListPage;
```

### 7.8 Figma Dev Mode 연동 최적화

```jsx
// utils/figmaTokens.js - Figma Variables를 JavaScript로 동기화
export const figmaTokens = {
  // Figma에서 추출한 실제 토큰 값들
  colors: {
    'color/primary/500': '#0ea5e9',
    'color/neutral/0': '#ffffff',
    'color/neutral/900': '#0f172a',
    // ... 기타 색상 토큰들
  },
  
  spacing: {
    'spacing/xs': '4px',
    'spacing/sm': '8px',
    'spacing/md': '16px',
    // ... 기타 간격 토큰들
  },
  
  typography: {
    'typography/heading/large': {
      fontFamily: 'Inter',
      fontSize: '24px',
      fontWeight: '600',
      lineHeight: '32px',
    },
    // ... 기타 타이포그래피 토큰들
  },
};

// Figma 토큰을 CSS Custom Properties로 변환
export const generateCSSCustomProperties = () => {
  const properties = [];
  
  Object.entries(figmaTokens.colors).forEach(([key, value]) => {
    const cssVar = `--${key.replace(/\//g, '-')}`;
    properties.push(`${cssVar}: ${value};`);
  });
  
  Object.entries(figmaTokens.spacing).forEach(([key, value]) => {
    const cssVar = `--${key.replace(/\//g, '-')}`;
    properties.push(`${cssVar}: ${value};`);
  });
  
  return `:root {\n  ${properties.join('\n  ')}\n}`;
};
```

---

## 8. 성능 최적화 및 접근성 고려사항

### 8.1 이미지 최적화 전략

```jsx
// components/atoms/OptimizedImage/OptimizedImage.jsx
import React, { useState } from 'react';
import PropTypes from 'prop-types';

const OptimizedImage = ({
  src,
  alt,
  width,
  height,
  sizes = '(max-width: 768px) 100vw, (max-width: 1024px) 50vw, 25vw',
  placeholder = 'blur',
  priority = false,
  ...rest
}) => {
  const [isLoaded, setIsLoaded] = useState(false);
  const [hasError, setHasError] = useState(false);

  // WebP 지원 여부에 따른 이미지 포맷 선택
  const getOptimizedSrc = (originalSrc) => {
    if (typeof window !== 'undefined') {
      const canvas = document.createElement('canvas');
      const supportsWebP = canvas.toDataURL('image/webp').indexOf('data:image/webp') === 0;
      
      if (supportsWebP && originalSrc.includes('picsum.photos')) {
        return `${originalSrc}&format=webp`;
      }
    }
    return originalSrc;
  };

  const handleLoad = () => {
    setIsLoaded(true);
  };

  const handleError = () => {
    setHasError(true);
  };

  if (hasError) {
    return (
      <div
        style={{
          width,
          height,
          backgroundColor: '#f3f4f6',
          display: 'flex',
          alignItems: 'center',
          justifyContent: 'center',
          color: '#6b7280',
          fontSize: '14px',
        }}
        {...rest}
      >
        이미지를 불러올 수 없습니다
      </div>
    );
  }

  return (
    <div style={{ position: 'relative', width, height }}>
      {/* 플레이스홀더 */}
      {!isLoaded && placeholder === 'blur' && (
        <div
          style={{
            position: 'absolute',
            top: 0,
            left: 0,
            right: 0,
            bottom: 0,
            backgroundColor: '#f3f4f6',
            background: 'linear-gradient(90deg, #f3f4f6 25%, #e5e7eb 50%, #f3f4f6 75%)',
            backgroundSize: '200% 100%',
            animation: 'shimmer 2s infinite linear',
          }}
        />
      )}
      
      <img
        src={getOptimizedSrc(src)}
        alt={alt}
        width={width}
        height={height}
        sizes={sizes}
        loading={priority ? 'eager' : 'lazy'}
        onLoad={handleLoad}
        onError={handleError}
        style={{
          width: '100%',
          height: '100%',
          objectFit: 'cover',
          opacity: isLoaded ? 1 : 0,
          transition: 'opacity 0.3s ease-in-out',
        }}
        {...rest}
      />
    </div>
  );
};

OptimizedImage.propTypes = {
  src: PropTypes.string.isRequired,
  alt: PropTypes.string.isRequired,
  width: PropTypes.oneOfType([PropTypes.string, PropTypes.number]),
  height: PropTypes.oneOfType([PropTypes.string, PropTypes.number]),
  sizes: PropTypes.string,
  placeholder: PropTypes.oneOf(['blur', 'empty']),
  priority: PropTypes.bool,
};

export default OptimizedImage;
```

이 가이드를 통해 Figma 라이브러리를 기반으로 한 체계적인 React 화면 설계가 가능합니다. 핵심은 Figma의 Design Token 시스템을 React 코드와 1:1로 매핑하여 일관성 있는 디자인 시스템을 구축하는 것입니다.