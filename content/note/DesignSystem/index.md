---
title: 디자인/프론트엔드를 위한 UI개발 DesignSystem Guide
version: "0.0.1"
latestUpdate: "2025-04-08"
description: UI개발을 위한 디자인시스템 가이드를 작성했습니다. 가이드는 저의 경험에 따라 매번 업데이트 됩니다.
---

> 재사용 가능한 컴포넌트 설계와 상태 관리는 많은 개발자들이 어려워 하는 부분입니다.
> 이는 복잡한 주제이며, 경험과 실습을 통해 점진적으로 익혀나가는 것이 일반적입니다.
> 지속적인 학습과 실제 프로젝트에 적용해보는 과정을 통해 점차 개선될 수 있습니다.

## 프로세스

1. 최초 컨셉의 재활용 컴포넌트를 업로드 한다.
2. 각종 테스트를 적용한다.
3. 새로운 적용을 해본다.
4. 타임라인을 공유한다.

## 기본구성

> react component를 예시로 작성 됨.

### Todo

1. Component Function
2. Styling
3. Variant
4. State

### Component Function

> 필요한 컴포넌트를 제작합니다.
> 외부에서도 사용할 수 있도록 react의 고유 기능인 `{chidren}`을 사용하여 컴포넌트 내부에 새로운 Markup을 넣어 재활용 가능하게 사용하는 방법입니다.

```tsx
function Button({ children }) {
  return <button>{children}</button>
}
```

### Styling

> button에 css를 적용합니다.
> css를 적용하는 방법은 크게 `tailwind.css`, `CSS Module`, `CSS-in-JS` 방식이 있습니다.
> 사이트를 새로 구축해 `DesignSystem`을 만드는 경우 러닝커브가 낮은 순으로 채용 되는 경우가 많습니다.

- 예를들어 `퍼블리셔`와 분업 하여 작업하는 경우 기존 CSS와 사용법이 가장 비슷한 `CSS Module` 을 이용합니다.
- tailwind와 react 환경의 이해도 가 있는 경우 tailwind를 이용해 컴포넌트 단위로 분업 하여 작업할 수 있습니다.
- `퍼블리셔` 포지션이 따로 없으며 `프론트엔드-쥬니어` 가 있는 경우 조금 더 JS 친화적인 CSS-in-JS방식을 선택하여 사용할 수 있습니다. (단, 기존 방식 보다는 러닝 커브와 정교한 코드 컨벤션이 없다면 복잡도가 증가할 가능성이 있습니다.)

#### Tailwind

```tsx
function Button({ children }) {
  return <button className="font-bold py-2 px-4 rounded">{children}</button>
}
```

#### React CSS Module

```tsx
import styles from "./Button.module.css"

function Button({ children }) {
  return <button className={styles.button}>{children}</button>
}
```

#### Styled-Component

```tsx
import styled from "styled-components"

const StyledButton = styled.button`
  background-color: #95a5a6;
  padding: 2px 4px;
  border-radius: 5px;

  &:hover {
    background-color: #7f8c8d};
  }
`

function Button({ children }) {
  return <StyledButton>{children}</StyledButton>
}
```

### Variant

> 디자이너가 주는 다양한 버튼의 디자인을 적용하는 방법입니다.
> 예제로는 primary, outline이 들어간다고 가정 하였습니다.

#### Tailwind

```tsx
type ButtonProps = {
  children: React.ReactNode
  variant: "primary" | "outline"
}

function Button({ children, variant }: ButtonProps) {
  return (
    <button
      className={`
			font-bold py-2 px-4 rounded
			${variant === "primary" ? "font-bold py-2 px-4 rounded" : ""}
			${
        variant === "outline"
          ? "bg-transparent border border-blue-500 text-blue-500"
          : ""
      }
		`}
    >
      {children}
    </button>
  )
}
```

#### React CSS Module

```tsx
import styles from "./Button.module.css"

type ButtonProps = {
  children: React.ReactNode
  variant: "primary" | "outline"
}

function Button({ children, variant }: ButtonProps) {
  return (
    <button
      className={`
			${styles.button} 
			${variant === "primary" ? styles.primary : ""}
			${variant === "outline" ? styles.outline : ""}
		`}
    >
      {children}
    </button>
  )
}
```

#### Styled-Component

```tsx
import styled from "styled-components"

type ButtonProps = {
  children: React.ReactNode
  variant: "primary" | "outline"
}

const StyledButton = styled.button<{ variant: "primary" | "outline" }>`
  ${props =>
    props.variant === "primary" &&
    css`
      background-color: #95a5a6;
      padding: 2px 4px;
      border-radius: 5px;

      &:hover {
        background-color: #7f8c8d;
      }
    `}
  ${props =>
    props.variant === "outline" &&
    css`
      background-color: transparent;
      color: #3498db;
      border: 1px solid #3498db;
      &:hover {
        background-color: #3498db;
        color: white;
      }
    `}
`

function Button({ children, variant }: ButtonProps) {
  return <StyledButton variant={variant}>{children}</StyledButton>
}
```

### State

> 컴포넌트에 필요한 `state(상태)`를 적용하는것은 `props`를 더 만들어서 받아 주게 됩니다.

#### Tailwind

```tsx
function Button({ children, variant, disabled = false }) {
  return (
    <button
      className={`
				font-bold py-2 px-4 rounded
				${
          variant === "outline"
            ? "bg-transparent border border-blue-500 text-blue-500"
            : "bg-blue-500 text-white"
        }
			`}
      disabled={disabled}
    >
      {children}
    </button>
  )
}
```
