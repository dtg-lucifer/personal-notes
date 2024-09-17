---
tags:
  - frontend
  - state-management
  - reactjs
  - nextjs
---
### Zustand: An In-Depth Guide

**Zustand** is a small, fast, and scalable state management solution for React applications. Unlike Redux, which can be complex and requires boilerplate code, Zustand provides a simpler API and more intuitive approach to managing state.

### Key Features of Zustand

- **Simplicity**: Minimal API and less boilerplate compared to Redux.
- **Performance**: Optimized for performance, leveraging React's useEffect and useReducer hooks internally.
- **Scalability**: Suitable for both small and large applications.
- **No Boilerplate**: Direct and straightforward state management without action types and reducers.

### How Zustand Differs from Redux

1. **API Simplicity**: Zustand provides a minimal API, making it easier to learn and use compared to Redux.
2. **Less Boilerplate**: No need for action types, action creators, or reducers. Zustand uses a more direct approach.
3. **Local and Global State**: Can handle both local and global state seamlessly.
4. **Ease of Use**: Setting up a Zustand store is simpler and more intuitive than Redux.
5. **Direct State Updates**: State can be updated directly within the store, avoiding the need for dispatch functions.

#### Middleware

Zustand supports middleware to enhance the store.

```jsx
import create from 'zustand'; 
import { devtools, persist } from 'zustand/middleware';  

const useStore = create(   
	persist(     
		devtools((set) => ({       
			count: 0,       
			increment: () => set((state) => ({ count: state.count + 1 })),       
			decrement: () => set((state) => ({ count: state.count - 1 })),     
	})),     
	{ name: 'counter-storage' } // persist options   
	) 
);
```
#### Asynchronous Actions

You can handle asynchronous actions in Zustand using async/await.

```jsx
import create from 'zustand';  

const useStore = create((set) => ({   
	count: 0,   
	increment: () => set((state) => ({ count: state.count + 1 })),   
	fetchData: async () => {     
		const response = await fetch('https://api.example.com/data');     
		const data = await response.json();     
		set({ count: data.count });   
	}, 
}));
```

### Example Project

Let's create a simple project with Zustand for managing a todo list.

1. **Install Zustand**:
    
```bash
npm i zustand
```
    
2. **Create the Store**:
    
    ```jsx
// store.js 
import create from 'zustand';  
const useTodoStore = create((set) => ({   
	todos: [],   
	addTodo: (todo) => set((state) => ({ todos: [...state.todos, todo] })),   
	removeTodo: (id) => set((state) => ({ todos: state.todos.filter(todo => todo.id !== id) })), 
}));
	
export default useTodoStore;
```
    
3. **Create Components**:
```jsx
// TodoList.js 
import React from 'react'; 
import useTodoStore from './store';  

function TodoList() {   
	const { todos, removeTodo } = useTodoStore();    
	
	return (     
		<ul>       
			{todos.map((todo) =>
				<li key={todo.id}>          
					{todo.text}          
					<button onClick={() => removeTodo(todo.id)}>Remove</button>        
				</li>      
			))}    
		</ul>  
	);
}

export default TodoList;
```

```jsx
// AddTodo.js 
import React, { useState } from 'react'; 
import useTodoStore from './store';  

function AddTodo() {   
	const [text, setText] = useState('');   
	const addTodo = useTodoStore((state) => state.addTodo);
	    
	const handleSubmit = (e) => {     
		e.preventDefault();     
		addTodo({       
			id: Math.random().toString(36).substr(2, 9),
			text,     
		});     
		setText('');   
	};    
	
	return (     
		<form onSubmit={handleSubmit}>       
			<input         
				type="text"         
				value={text}         
				onChange={(e) => setText(e.target.value)}       
			/>       
			<button type="submit">Add Todo</button>     
		</form>   
	); 
}  

export default AddTodo; 
```


4. **Integrate Components**:

```jsx
// App.js 
import React from 'react'; 
import TodoList from './TodoList'; 
import AddTodo from './AddTodo';  

function App() {   
	return (     
		<div>       
			<h1>Todo List</h1>       
			<AddTodo />       
			<TodoList />     
		</div>   
	); 
}  

export default App;
```

### Handling Asynchronous Tasks and Loading State

1. **Creating the Store**: Define your store with asynchronous actions and a loading state.

```jsx
import create from 'zustand';  

const useStore = create((set) => ({   
	count: 0,   
	loading: false,   
	increment: (by = 1) => set((state) => ({ count: state.count + by })),   
	decrement: (by = 1) => set((state) => ({ count: state.count - by })),   
	fetchData: async () => {     
		set({ loading: true });     
		try {       
			const response = await fetch('https://api.example.com/data');       
			const data = await response.json();       
			set({ count: data.count });     
		} catch (error) {       
			console.error('Failed to fetch data', error);     
		} finally {       
			set({ loading: false });     
		}   
	}, 
}));  

export default useStore;
```
    
2. **Using the Store in Components**: Update your components to reflect the loading state and trigger asynchronous actions.
    
```jsx
import React from 'react'; 
import useStore from './store';  

function Counter() {   
	const { count, increment, decrement, fetchData, loading } = useStore();    
	
	return (     
		<div>       
			<h1>{count}</h1>       
			<button onClick={() => increment(1)}>Increment</button>       
			<button onClick={() => decrement(1)}>Decrement</button>       
			<button onClick={fetchData} disabled={loading}>         
				{loading ? 'Loading...' : 'Fetch Data'}       
			</button>     
		</div>   
	); 
}  

export default Counter;
```