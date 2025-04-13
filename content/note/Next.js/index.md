---
title: Fullstack 개발을 위한 Next.js 실무 GUIDE
version: "0.0.1"
latestUpdate: "2025-04-08"
description: 25년 개발자들이 가장 선호하는 풀스택 프레임워크의 Dcoument를 실무에 가장 필요한 내용들로 GUIDE 작성을 했습니다.
---

# Routing

> `app`폴더 밑에 파일 제작 하는 방식에 대한 설명과 비지니스로직 입니다.
> `page.jsx` 와 `layout.jsx` 또는 `templates.jsx` `<link>`와 `useRouter()` 등의 설명을 합니다.

```tsx
<Layout>
  <Template>
    <ErrorBoundary fallback={<Error />}>
      <Suspense fallback={<Loading />}>
        <ErrorBoundary fallback={<NotFound />}>
          <Page />
        </ErrorBoundary>
      </Suspense>
    </ErrorBoundary>
  </Template>
</Layout>
```

## 🥯 Defining Routes

웹 화면의 route를 next.js에서 만드는 방법을 설명 합니다.

### 🧁 app/dashboard

📁`app/dashboard` 👉 `http://site.com/dashboard`

## 🥯 Pages

Routes를 만든 다음 폴더 아래에 indexpage를 만드는 방법에 대한 설명입니다.
🔰 page.js는 `Server Components` 가 기본입니다.

### 🧁 page.tsx

📁`app/dashboard/page.jsx`

**파일 예시**

```jsx
export default function Page() {
  return <h1>Hello, Next.js!</h1>
}
```

## 🥯 Layouts and Templates

routes폴더 아래에 생성할 수 있는 `layout.jsx`, `templates.jsx` 에 관한 내용입니다.
routes별로 공통의 레이아웃을 제작할 수 있습니다.
🔰 Layout.js는 Metaata를 넣거나 Nav Links를 넣을 때 유용합니다.
🔰 Template.js는 페이지 내부의 내부 filter나 search form에 유용합니다.

### 🧁 Layouts.tsx

폴더에 `layout.js`를 넣어서 사용

- `header` 와 `footer`와 같은 공통 양식 기입
- 각각의 페이지마다 존재하는 `sidebar`

### 🧁 Templates.tsx

폴더에 `template.js`를 넣어서 사용

- 비슷한 구조를 가진 여러 페이지에 대해 공통 래퍼를 제공하고 싶지만, 각 페이지마다 독립적인 인스턴스를 원할 때 사용합니다.
- 상태가 유지되지 않고 DOM 요소가 다시 생성됩니다.
- 페이지 전환 시 새로운 인스턴스가 마운트되고 이전 인스턴스는 언마운트됩니다.

## 🥯 Linking and Navigating

페이지와 페이지 사이를 움직이는 4가지의 방법에 대해 설명합니다.
`<Link>`, `useRouter`, `redirect`, `History API`
그리고 Routing 과 Navigation의 작동방식에 대한 설명이 있습니다.

### **🧁 `<Link>`**

기본적인 링크 방식입니다.
markup에 사용하면 좋습니다.

```jsx
import Link from "next/link"

export default function Page() {
  return <Link href="/dashboard">Dashboard</Link>
}
```

### **🧁 `useRouter()`**

비지니스로직에서 원하는 페이지로 이동할 때 사용하는 hook 입니다.
History API와 관련이 있습니다.
특징 : CSR에서만 사용 가능

```jsx
"use client"

import { useRouter } from "next/navigation"

export default function Page() {
  const router = useRouter()

  return (
    <button type="button" onClick={() => router.push("/dashboard")}>
      Dashboard
    </button>
  )
}
```

### **🧁 `redirect()`**

서버컴포넌트의 dataFetching 실패 시 redirect를 지원하는 함수입니다.
특징 : SSR에서 사용 가능

```tsx
import { redirect } from "next/navigation"

async function AuthCheck() {
  const user = await getUser() // 서버에서 사용자 정보를 가져오는 함수

  if (!user) {
    redirect("/login")
  }

  return <ProtectedComponent />
}
```

### **`Native History API`**

window에서 제공하는 `window.history.pushState` 와 `window.history.replaceState`를 사용하는 방식을 제공해줍니다.
제공해주는 예제가 있으나 `useRouter()`를 이용하는 것이 아직 까진 더 현명해 보입니다.

#### 🧁 .history.pushState 이용

```jsx
"use client"

import { useSearchParams } from "next/navigation"

export default function SortProducts() {
  const searchParams = useSearchParams()

  function updateSorting(sortOrder: string) {
    const params = new URLSearchParams(searchParams.toString())
    params.set("sort", sortOrder)
    window.history.pushState(null, "", `?${params.toString()}`)
  }

  return (
    <>
      <button onClick={() => updateSorting("asc")}>Sort Ascending</button>
      <button onClick={() => updateSorting("desc")}>Sort Descending</button>
    </>
  )
}
```

#### 🧁 useRouter() 이용

```jsx
"use client"

import { useRouter, useSearchParams } from "next/navigation"

export default function SortProducts() {
  const router = useRouter()
  const searchParams = useSearchParams()

  function updateSorting(sortOrder: string) {
    const params = new URLSearchParams(searchParams.toString())
    params.set("sort", sortOrder)

    router.push(`?${params.toString()}`, { scroll: false })
  }

  return (
    <>
      <button onClick={() => updateSorting("asc")}>Sort Ascending</button>
      <button onClick={() => updateSorting("desc")}>Sort Descending</button>
    </>
  )
}
```

## 🥯 Error Handling

예상되는 에러 상항과 예상하지 못한 상황을 `error.tsx`, `global-error.tsx` 파일을 이용해 다루는 방법에 대한 이야기 입니다.

### 🧁 error.js

레이아웃 폴더 구조 아래에 `error.js`를 사용합니다.
`error.tsx`는 'use client' 기반입니다.

- app/error.js 👉 Common
- app/dashboard/error.js 👉 Optional
- app/global-error.js 👉 Uncommon

**error.tsx를 사용하는 방법**
dashboard/page.js

```tsx
<Layout>
  <ErrorBoundary fallback={<Error />}>
    <Layout></Layout>
  </ErrorBoundary>
</Layout>
```

## Loading UI and Streaming

## Redirecting

## Route Groups

`path`가 존재하지 않지만 논리적으로 페이지를 `Group` 하는 기능

- `폴더구조 리팩토링` : 프로젝트의 다양한 기능을 주소 없이 논리적인 구조로 구분 하고 싶을때 사용
- `레이아웃 분할` : path는 나누지 않았지만 각각의 `layout.js` 가 필요할때

### Use

폴더구조에 `(괄호)`를 넣어서 작성

#### 물리적 페이지 Group

`app/shop/account/page.js` 👉 `https://{siteURL}/shop/account`
`app/marketing/about/page.js` 👉 `https://{siteURL}/about`

#### Route Groups

`app/(shop)/account/page.js`👉 `https://{siteURL}/account`
`app/(marketing)/about/page.js`👉`https://{siteURL}/about`

## Project Organization

## Dynamic Routes

주소에 있는 `params`값을 가져 옵니다.
`[folderName]`, `[id]`, `[slug]`

### a. g.

`app/blog/[slug]/page.js` 👉 `/blog/a` 👉 `{ slug : 'a" }`

## Parallel Routes

## Intercepting Routes

## Route Handlers

## Middleware

## Internationalization

# Data Fetching

> ServerComponent에서의 Data Fetching을 설명합니다.
> react-query를 이용하는것과의 차이점을 알아 보겠습니다.

# Rendering

> CSR,SSR, 그리고 Static 과 Dynamic 렌더링이 next.js에서 어떤식으로 구동되는지 알아 봅니다.

# Styling

> 지원하는 css 를 방식별로 알아 봅니다.

# Optiizations

> 최적화에 대해서 알아봅니다. Image, Fonts, Script 등을 어떻게 처리하면 되는지 알아 봅니다.
