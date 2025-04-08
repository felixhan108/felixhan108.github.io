---
title: React-CheetBook::자주 사용하는 블록묶음 모음음
version: "0.0.1"
latestUpdate: "2025-04-08"
description: 리액트에서 자주 사용하는 블록 묶음을 모아봤습니다.
---

> https://react.dev/learn 으로 부터 확보한 cheet book

# Displaying data

```javascript
const user = {
  name: "Han Sungsoo",
  imageUrl: "https://picsum.photos/200",
  imageSize: 90,
}

export default function Profile() {
  return (
    <>
      <h1>{user.name}</h1>
      <img
        className="avater"
        src={user.imageUrl}
        alt={"Photo of " + user.name}
        style={{
          width: user.imageSize,
          height: user.imageSize,
        }}
      />
    </>
  )
}
```

# Conditional rendering

```javascript
let content
if (isLoginedIn) {
  content = <AdminPanel />
} else {
  content = <LoginForm />
}
return <div>{content}</div>
```

# Other works

```javascript
return <div>{isLoggedIn ? <AdminPanel /> : <LoginForm />}</div>
```

## or

```javascript
return <div>{isLoggedIn && <AdminPanel />}</div>
```

# Rendering List

```jsx
const listItems = producst.map(product =>
	<li key={prroduct.id}>
		{product.title}
	</li>
);

return(
	<ul>{listItems}</li>
)
```

## or

```jsx
const products = [
  { title: 'Cabbage', isFruit: false, id: 1 },
  { title: 'Garlic', isFruit: false, id: 2 },
  { title: 'Apple', isFruit: true, id: 3 },
];

export default function ShoppingList() {
	const listItems = producst.map(product =>
		<li
			key={product.id}
			style={{
				color: product.isFruit ? 'magenta' : 'darkgreen'
			}}>
			{product.title}
		</li>
	);
	return (
		<ul>{listItems}</li>
	)
}
```

# Responding to events

```jsx
function MyButton() {
  function handleClick() {
    alert("You clicked me!")
  }
  return <button onClick={handleClick}>Click me</button>
}
```

# Updating the screen

```jsx
import { useState } from "react"

function MyButton() {
  const [count, setCount] = useState(0)
  function handleClick() {
    setCount(count + 1)
  }
  return <button onClick={handleClick}>Clicked {count} times</button>
}
```

# Thinking in React

## Step 1: Break the UI into a component hierarchy

## Step 2: Build a static version in React

## Step 3: Find the minimal but complete representation of UI state

## Step 4: Identify where your state should live

## Step 5: Add inverse data flow

```jsx
import { useState } from 'react';

function FilterableProductTable({ products }){
	const [firlterText, setFilterText] = useState('');
	const [inStockOnly, setInStockOnly] = useState(false);

	return(
		<div>
			<SearchBar />
			<ProductTable />
		</div>
	) // return
} // FilterableProductTable

function ProductCategoryRow({ category }){
	return(
		<tr>
			<th colSpan="2">
				{category}
			</th>
		</tr>
	) // return
} // ProductCategoryRow

function ProductRow({ product }){
	const name = product.stocked ? product.name :
		<span style={{ color:'red' }}?
			{{ product.name }}
		</span>;

	return (
		<tr>
			<td>{name}</td>
			<td>{product.price}</td>
		</tr>
	) // return
} // ProductRow

```

```jsx

function ProductTable({ products, filterText, inStockOnly }){
	const rows = [];
	let lastCategory = null;
	products.forEach((product) => {
		if (
			product.name.toLowerCase().indexOf(filterText.toLowerCase()) === -1
		) {
			return;
		} // if
		if (product.category !== lastCategory){
			rows.push(
				<ProductCategoryRow
					category={product.category}
					key={product.category}
				/>
			); // rows.push
		} // if
		rows.push(
			<ProductRow
				product={product}
				key={product.name} />
		); // rows.push
		lastCategory = product.category;
	}); // products.forEach

	return (
		<table>
	      <thead>
	        <tr>
	          <th>Name</th>
	          <th>Price</th>
	        </tr>
	      </thead>
	      <tbody>{rows}</tbody>
	    </table>
	)
}

function SeacrchBar({
	filterText,
	inStockOnly,
	onFilterTextChange,
	onInStockOnlychange}){
	}) {
		return (
			<form>
				<input
					type="text"
					value={filterText} placeholder="search..."
					onChange={(e) => onFilterTextChange(e.target.value)} />
				/>
			</form>
		) // return
	} // SearchBar
```
