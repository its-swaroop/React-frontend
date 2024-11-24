# **React - The Complete Guide 2024 (incl. Next.js, Redux) - Study Notes**  

These notes are derived from *"React - The Complete Guide 2024"* by Maximilian Schwarzmüller on Udemy. 

<br/>
<br/>

### Section 1: Getting Started  

#### **Overview of React**  
- **What is React?**
  - A JavaScript library for building user interfaces, focused on the view layer of an application.
  - Component-based architecture for building reusable UI pieces.

- **Key Features:**
  - Declarative programming: React updates the DOM efficiently with its virtual DOM system.
  - Component-based structure: Encourages reusable and composable UI blocks.
  - Unidirectional data flow: Data flows downwards, simplifying state management.

#### **Setup for React Development**  
- Install Node.js and npm (Node Package Manager).
- Create a React app using `npx create-react-app my-app`.
- Project structure:
  - **src/**: Source files for components and logic.
  - **public/**: Static assets and HTML template.

#### **Writing the First React Component**  
- A component is a JavaScript function that returns JSX:
  ```jsx
  const Welcome = () => {
    return <h1>Welcome to React!</h1>;
  };
  ```
- Use components within the `App.js` file to render them.

---

### Section 2: React Basics and Working with Components  

#### **JSX (JavaScript XML)**  
- **What is JSX?**
  - Syntax extension that looks like HTML but is written in JavaScript.
  - Example:
    ```jsx
    const element = <h1>Hello, JSX!</h1>;
    ```
- JSX is not required but highly recommended for readability.

#### **Component Basics**  
- **Types of Components:**
  - Functional Components: Use plain functions and React Hooks.
  - Class Components: Include lifecycle methods and state.

- **Props (Properties):**
  - Data passed from parent to child components.
  - Immutable within the child.
  - Example:
    ```jsx
    const Greeting = ({ name }) => <h1>Hello, {name}!</h1>;
    ```

#### **Component Nesting:**
  ```jsx
  const App = () => (
    <div>
      <Greeting name="John" />
      <Greeting name="Doe" />
    </div>
  );
  ```

---

### Section 3: Working with State and Events  

#### **State in React**  
- **What is State?**
  - A local, mutable data store within a component.
  - Managed via the `useState` hook in functional components.
  - Example:
    ```jsx
    const [count, setCount] = useState(0);
    ```

#### **Handling Events**  
- Use inline functions or separate handler methods.
  ```jsx
  <button onClick={() => setCount(count + 1)}>Click Me</button>
  ```

- **Passing Data through State:**
  - Lifting state to a parent component for child-to-child communication.

---

### Section 4: Rendering Lists and Conditional Content  

#### **Rendering Lists**  
- Use the `map()` function to render a list of items.
  ```jsx
  const names = ['Alice', 'Bob', 'Charlie'];
  return names.map(name => <h2 key={name}>{name}</h2>);
  ```

- **Keys in Lists:**
  - Unique identifiers for efficient rendering and updates.

#### **Conditional Rendering**  
- Use conditional operators (`if`, `?`, `&&`) to display content dynamically.
  ```jsx
  {isLoggedIn ? <h1>Welcome!</h1> : <h1>Please log in</h1>}
  ```

---

### Section 5: Styling React Components  

#### **Styling Approaches**  
1. **CSS Stylesheets:**  
   Link a stylesheet and apply class names.
   ```jsx
   <div className="my-style"></div>
   ```

2. **Inline Styles:**  
   Use the `style` attribute with an object.
   ```jsx
   <div style={{ backgroundColor: 'blue', color: 'white' }}></div>
   ```

3. **CSS Modules:**  
   - Scope styles locally to components using `.module.css` files.
     ```jsx
     import styles from './Button.module.css';
     <button className={styles.primary}>Click Me</button>;
     ```

4. **Styled Components:**  
   - Use libraries like `styled-components` for CSS-in-JS.

---

### Section 6: Debugging React Apps  

#### **Tools for Debugging**  
- **React Developer Tools:**
  - Inspect component hierarchy and state/props in real-time.

- **Browser DevTools:**
  - Inspect DOM, debug JavaScript, and monitor network requests.

#### **Common Debugging Techniques**  
- Console logs for state/props inspection.
- Breakpoints in browser DevTools for function analysis.
- Error boundaries to catch rendering errors.

---

### Section 7: Advanced Components & Reusability  

#### **Component Composition**  
- Combine small components to create larger UIs.
  ```jsx
  const Page = () => (
    <Header />
    <Content />
    <Footer />
  );
  ```

#### **Prop Drilling and Context API**  
- **Prop Drilling:**
  - Passing data down multiple layers of components.
  - Solution: Use the Context API.

- **Context API:**
  - Provide global data access without prop drilling.
    ```jsx
    const ThemeContext = React.createContext();
    const App = () => (
      <ThemeContext.Provider value="dark">
        <Content />
      </ThemeContext.Provider>
    );
    ```

---
### Section 8: Working with Refs & Portals - Self Notes  

#### **Refs in React**  
- **What are Refs?**
  - Refs provide a way to access DOM nodes or React elements directly.
  - Useful for manipulating DOM directly when necessary (e.g., focus input fields, media playback).  

- **How to Create Refs:**
  - Use `React.createRef()` in class components.
  - For functional components, use the `useRef` hook.

- **Usage Examples:**
  ```jsx
  const inputRef = React.createRef();
  <input ref={inputRef} />;
  inputRef.current.focus(); // Access the DOM node
  ```

- **When to Use Refs:**
  - Managing focus, text selection, or media playback.
  - Triggering imperative animations.
  - Integrating third-party DOM libraries.

#### **Portals in React**  
- **What are Portals?**
  - A way to render children into a DOM node outside the parent component’s DOM hierarchy.
  - Commonly used for modals, tooltips, and overlays.

- **How to Use Portals:**
  - Use `ReactDOM.createPortal(child, containerNode)`.
  ```jsx
  ReactDOM.createPortal(
    <ModalContent />,
    document.getElementById('modal-root')
  );
  ```

- **Advantages:**
  - Decouples modal/overlay content from the parent component’s styling.
  - Still maintains React context even outside the DOM hierarchy.

#### **Practical Implementation in Code:**  
- **Example 1: Managing Input Focus with Refs**  
  ```jsx
  import React, { useRef } from 'react';

  const InputFocus = () => {
    const inputRef = useRef();

    const focusHandler = () => {
      inputRef.current.focus();
    };

    return (
      <div>
        <input ref={inputRef} type="text" />
        <button onClick={focusHandler}>Focus Input</button>
      </div>
    );
  };

  export default InputFocus;
  ```

- **Example 2: Modal with Portals**  
  ```jsx
  import ReactDOM from 'react-dom';

  const Modal = ({ onClose, children }) => {
    return ReactDOM.createPortal(
      <div className="modal">
        <div className="content">
          {children}
          <button onClick={onClose}>Close</button>
        </div>
      </div>,
      document.getElementById('modal-root')
    );
  };

  export default Modal;
  ```

#### **Best Practices:**  
- **For Refs:**
  - Avoid overusing refs; prefer React’s declarative approach.
  - Use refs as a last resort for direct DOM manipulations.

- **For Portals:**
  - Ensure accessibility: manage keyboard focus and ARIA attributes.
  - Properly handle unmounting to avoid memory leaks.

