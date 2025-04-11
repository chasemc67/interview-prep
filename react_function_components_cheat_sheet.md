# React Function Components Crash Course

A concise guide to React function components, hooks, and patterns commonly used in modern React development.

---

## 1. Basic Component Structure

```tsx
// Basic function component
function Greeting() {
  return <h1>Hello, React!</h1>;
}

// Arrow function component
const Greeting = () => {
  return <h1>Hello, React!</h1>;
};

// Component with props
interface GreetingProps {
  name: string;
  age?: number; // Optional prop
}

const Greeting = ({ name, age = 18 }: GreetingProps) => {
  return (
    <div>
      <h1>Hello, {name}!</h1>
      {age && <p>You are {age} years old</p>}
    </div>
  );
};
```

## 2. useState Hook

```tsx
import { useState } from "react";

function Counter() {
  // Basic state
  const [count, setCount] = useState(0);

  // State with type
  const [user, setUser] = useState<{ name: string; age: number } | null>(null);

  // State with complex object
  const [formData, setFormData] = useState({
    username: "",
    email: "",
    password: "",
  });

  // Update state
  const increment = () => {
    setCount((prevCount) => prevCount + 1);
  };

  // Update nested state
  const updateForm = (field: string, value: string) => {
    setFormData((prev) => ({
      ...prev,
      [field]: value,
    }));
  };

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
}
```

## 3. useEffect Hook

```tsx
import { useEffect, useState } from "react";

function DataFetcher() {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);

  // Basic effect (runs on mount)
  useEffect(() => {
    console.log("Component mounted");
  }, []);

  // Effect with cleanup
  useEffect(() => {
    const timer = setInterval(() => {
      console.log("Tick");
    }, 1000);

    return () => {
      clearInterval(timer);
    };
  }, []);

  // Effect with dependencies
  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await fetch("https://api.example.com/data");
        const json = await response.json();
        setData(json);
      } catch (error) {
        console.error("Error fetching data:", error);
      } finally {
        setLoading(false);
      }
    };

    fetchData();
  }, []); // Empty dependency array = run once on mount

  if (loading) return <div>Loading...</div>;
  return <div>{JSON.stringify(data)}</div>;
}
```

## 4. useRef Hook

```tsx
import { useRef, useEffect } from "react";

function TextInput() {
  const inputRef = useRef<HTMLInputElement>(null);

  useEffect(() => {
    // Focus input on mount
    inputRef.current?.focus();
  }, []);

  return <input ref={inputRef} type="text" />;
}

// useRef for storing mutable values
function Timer() {
  const intervalRef = useRef<number>();

  useEffect(() => {
    intervalRef.current = window.setInterval(() => {
      console.log("Tick");
    }, 1000);

    return () => {
      if (intervalRef.current) {
        clearInterval(intervalRef.current);
      }
    };
  }, []);

  return <div>Timer running...</div>;
}
```

## 5. useCallback and useMemo

```tsx
import { useCallback, useMemo, useState } from "react";

function ExpensiveComponent() {
  const [count, setCount] = useState(0);
  const [items] = useState([1, 2, 3, 4, 5]);

  // Memoized callback
  const handleClick = useCallback(() => {
    setCount((prev) => prev + 1);
  }, []); // Empty dependency array = stable function

  // Memoized value
  const sum = useMemo(() => {
    console.log("Calculating sum...");
    return items.reduce((a, b) => a + b, 0);
  }, [items]); // Recalculate when items change

  return (
    <div>
      <p>Count: {count}</p>
      <p>Sum: {sum}</p>
      <button onClick={handleClick}>Increment</button>
    </div>
  );
}
```

## 6. Custom Hooks

```tsx
import { useState, useEffect } from "react";

// Custom hook for fetching data
function useFetch<T>(url: string) {
  const [data, setData] = useState<T | null>(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState<Error | null>(null);

  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await fetch(url);
        const json = await response.json();
        setData(json);
      } catch (err) {
        setError(err as Error);
      } finally {
        setLoading(false);
      }
    };

    fetchData();
  }, [url]);

  return { data, loading, error };
}

// Using the custom hook
function UserProfile({ userId }: { userId: string }) {
  const { data: user, loading, error } = useFetch<User>(`/api/users/${userId}`);

  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error: {error.message}</div>;
  if (!user) return <div>No user found</div>;

  return (
    <div>
      <h1>{user.name}</h1>
      <p>{user.email}</p>
    </div>
  );
}
```

## 7. Context API

```tsx
import { createContext, useContext, useState, ReactNode } from "react";

// Create context
interface ThemeContextType {
  theme: "light" | "dark";
  toggleTheme: () => void;
}

const ThemeContext = createContext<ThemeContextType | undefined>(undefined);

// Context provider component
function ThemeProvider({ children }: { children: ReactNode }) {
  const [theme, setTheme] = useState<"light" | "dark">("light");

  const toggleTheme = () => {
    setTheme((prev) => (prev === "light" ? "dark" : "light"));
  };

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

// Custom hook for using context
function useTheme() {
  const context = useContext(ThemeContext);
  if (context === undefined) {
    throw new Error("useTheme must be used within a ThemeProvider");
  }
  return context;
}

// Using the context
function ThemeToggle() {
  const { theme, toggleTheme } = useTheme();

  return (
    <button onClick={toggleTheme}>
      Switch to {theme === "light" ? "dark" : "light"} mode
    </button>
  );
}
```

## 8. Common Patterns

```tsx
// Conditional rendering
function UserGreeting({ isLoggedIn }: { isLoggedIn: boolean }) {
  return (
    <div>{isLoggedIn ? <h1>Welcome back!</h1> : <h1>Please sign in</h1>}</div>
  );
}

// List rendering
function TodoList({ todos }: { todos: string[] }) {
  return (
    <ul>
      {todos.map((todo, index) => (
        <li key={index}>{todo}</li>
      ))}
    </ul>
  );
}

// Form handling
function LoginForm() {
  const [formData, setFormData] = useState({
    email: "",
    password: "",
  });

  const handleSubmit = (e: React.FormEvent) => {
    e.preventDefault();
    // Handle form submission
  };

  const handleChange = (e: React.ChangeEvent<HTMLInputElement>) => {
    const { name, value } = e.target;
    setFormData((prev) => ({
      ...prev,
      [name]: value,
    }));
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="email"
        name="email"
        value={formData.email}
        onChange={handleChange}
      />
      <input
        type="password"
        name="password"
        value={formData.password}
        onChange={handleChange}
      />
      <button type="submit">Login</button>
    </form>
  );
}
```

## 9. Performance Optimization

```tsx
// React.memo for preventing unnecessary re-renders
const MemoizedComponent = React.memo(function MyComponent({
  data,
}: {
  data: string;
}) {
  return <div>{data}</div>;
});

// useMemo for expensive calculations
function ExpensiveCalculation({ items }: { items: number[] }) {
  const result = useMemo(() => {
    return items.reduce((sum, item) => sum + item, 0);
  }, [items]);

  return <div>Result: {result}</div>;
}

// useCallback for stable function references
function ParentComponent() {
  const [count, setCount] = useState(0);

  const handleClick = useCallback(() => {
    setCount((prev) => prev + 1);
  }, []);

  return <ChildComponent onClick={handleClick} />;
}
```

## 10. Error Boundaries

```tsx
import { Component, ErrorInfo, ReactNode } from "react";

interface Props {
  children: ReactNode;
}

interface State {
  hasError: boolean;
  error: Error | null;
}

class ErrorBoundary extends Component<Props, State> {
  public state: State = {
    hasError: false,
    error: null,
  };

  public static getDerivedStateFromError(error: Error): State {
    return { hasError: true, error };
  }

  public componentDidCatch(error: Error, errorInfo: ErrorInfo) {
    console.error("Uncaught error:", error, errorInfo);
  }

  public render() {
    if (this.state.hasError) {
      return <h1>Sorry.. there was an error</h1>;
    }

    return this.props.children;
  }
}

// Usage
function App() {
  return (
    <ErrorBoundary>
      <MyComponent />
    </ErrorBoundary>
  );
}
```
