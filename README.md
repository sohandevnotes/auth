# 📚 Table of Contents
1. 🚀 Step 1: Create Vite Project  
2. 📁 Step 2: Navigate Into Project  
3. ⚛️ Step 3: Install React  
4. 🎨 Step 4: Install Tailwind CSS  
5. 🌈 Step 5: Install DaisyUI  
6. ✒️ Step 6: Add Urbanist Font  
7. 🛣️ Step 7: Install React Router  
8. 🏗️ Step 8: Create Layout & Pages  
9. 🧭 Step 9: Create Routes  
10. 🔌 Step 10: Enable Router in main.jsx  
11. 🔔 Step 11: Add Toast Notifications  
12. 🔥 Step 12: Firebase Setup  
13. 👤 Step 13: Create Auth Context  
14. 🛡️ Step 14: Create Auth Provider  
15. 🛡️ Step 15: Create useAuth Hook  
16. 🛡️ Step 16: Create Login.jsx Page  
17. 🛡️ Step 17: Create Signup.jsx Page  
18. 🛡️ Step 18: Add Login & Signup Routes  
________________________________________

## 🚀 Step 1: Create Vite Project
```bash
npm create vite@latest my-project
````

🎉 Project created successfully!

---

## 📁 Step 2: Navigate Into Project

```bash
cd my-project
```

---

## ⚛️ Step 3: Install React

```bash
npm install
```

---

## 🎨 Step 4: Install Tailwind CSS

```bash
npm install tailwindcss
```

### Update **vite.config.ts**

(Path: `my-project/vite.config.ts`)

```js
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import tailwindcss from "@tailwindcss/vite";

export default defineConfig({
  plugins: [react(), tailwindcss()],
});
```

### Update **index.css**

(Path: `my-project/src/index.css`)

```css
@import "tailwindcss";
```

---

## 🌈 Step 5: Install DaisyUI

```bash
npm i -D daisyui@latest
```

Add plugin in **index.css**
(Path: `my-project/src/index.css`)

```css
@plugin "daisyui" {
  themes: light --default, dark --prefersdark;
  themes: light --default;
}
```

---

## ✒️ Step 6: Add Urbanist Font

(Path: `my-project/src/index.css`)

```css
@import url('https://fonts.googleapis.com/css2?family=Urbanist:ital,wght@0,100..900;1,100..900&display=swap');

body {
  font-family: "Urbanist", sans-serif;
  font-optical-sizing: auto;
  font-style: normal;
}
```

---

## 🛣️ Step 7: Install React Router

```bash
npm i react-router
```

---

## 🏗️ Step 8: Create Layout & Pages

### **MainLayout.jsx**

(Path: `my-project/src/layouts/MainLayout.jsx`)

```jsx
import React from "react";
import { Outlet } from "react-router";

const MainLayout = () => {
  return (
    <div>
      <Outlet />
    </div>
  );
};

export default MainLayout;
```

### **Home.jsx**

(Path: `my-project/src/pages/Home/Home.jsx`)

```jsx
import React from "react";

const Home = () => {
  return (
    <div>
      <h1>Home</h1>
    </div>
  );
};

export default Home;
```

---

## 🧭 Step 9: Create Routes

(Path: `my-project/src/routes/routes.jsx`)

```jsx
import { createBrowserRouter } from "react-router";
import MainLayout from "../layouts/MainLayout";
import Home from "../pages/Home/Home";

export const router = createBrowserRouter([
  {
    path: "/",
    Component: MainLayout,
    children: [{ index: true, Component: Home }],
  },
]);
```

---

## 🔌 Step 10: Enable Router in main.jsx

(Path: `my-project/src/main.jsx`)

```jsx
import React from "react";
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import { RouterProvider } from "react-router";
import { router } from "./routes/routes";
import "./index.css";

createRoot(document.getElementById("root")).render(
  <StrictMode>
    <RouterProvider router={router} />
  </StrictMode>
);
```

---

## 🔔 Step 11: Add Toast Notifications

```bash
npm install react-hot-toast
```

Enable in **main.jsx**:
(Path: `my-project/src/main.jsx`)

```jsx
import { Toaster } from "react-hot-toast";

<Toaster position="top-right" reverseOrder={false} />
```

---

## 🔥 Step 12: Firebase Setup

```bash
npm install firebase
```

### **firebase.config.js**

(Path: `my-project/src/firebase/firebase.config.js`)

```js
import { initializeApp } from "firebase/app";

const firebaseConfig = {
  apiKey: import.meta.env.VITE_FIREBASE_API_KEY,
  authDomain: import.meta.env.VITE_FIREBASE_AUTH_DOMAIN,
  projectId: import.meta.env.VITE_FIREBASE_PROJECT_ID,
  storageBucket: import.meta.env.VITE_FIREBASE_STORAGE_BUCKET,
  messagingSenderId: import.meta.env.VITE_FIREBASE_MESSAGING_SENDER_ID,
  appId: import.meta.env.VITE_FIREBASE_APP_ID,
};

const app = initializeApp(firebaseConfig);
export default app;
```

### **.env**

(Path: `my-project/.env`)

```
VITE_FIREBASE_API_KEY=YOUR_API_KEY
VITE_FIREBASE_AUTH_DOMAIN=YOUR_PROJECT.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=YOUR_PROJECT_ID
VITE_FIREBASE_STORAGE_BUCKET=YOUR_PROJECT.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=YOUR_SENDER_ID
VITE_FIREBASE_APP_ID=YOUR_APP_ID
```

---

## 👤 Step 13: Create Auth Context

(Path: `my-project/src/providers/AuthContext.jsx`)

```js
import { createContext } from "react";
export const AuthContext = createContext(null);
```

---

## 🛡️ Step 14: Create Auth Provider

(Path: `my-project/src/providers/AuthProvider.jsx`)

```jsx
import React from "react";
import { AuthContext } from "./AuthContext";
import { getAuth } from "firebase/auth";
import app from "../firebase/firebase.config";

const auth = getAuth(app);

const AuthProvider = ({ children }) => {
  const authInfo = {};

  return (
    <AuthContext.Provider value={authInfo}>{children}</AuthContext.Provider>
  );
};

export default AuthProvider;
```

---

## 🛡️ Step 15: Create useAuth Hook

(Path: `my-project/src/hooks/useAuth.jsx`)

```jsx
import { useContext } from "react";
import { AuthContext } from "../providers/AuthContext";

const useAuth = () => {
  const auth = useContext(AuthContext);
  return auth;
};

export default useAuth;
```

---

## 🛡️ Step 16: Create Login.jsx Page

(Path: `my-project/src/pages/Login/Login.jsx`)

```jsx
import React from "react";

const Login = () => {
  return (
    <div>
      <h1>Login</h1>
    </div>
  );
};

export default Login;
```

---

## 🛡️ Step 17: Create Signup.jsx Page

(Path: `my-project/src/pages/Signup/Signup.jsx`)

```jsx
import React from "react";

const SignUp = () => {
  return (
    <div>
      <h1>SignUp</h1>
    </div>
  );
};

export default SignUp;
```

---

## 🛡️ Step 18: Add Login & Signup Routes

(Path: `my-project/src/routes/routes.jsx`)

```jsx
import { createBrowserRouter } from "react-router";
import MainLayout from "../layouts/MainLayout";
import Home from "../pages/Home/Home";
import Login from "../pages/Login/Login";
import SignUp from "../pages/Signup/Signup";

export const router = createBrowserRouter([
  {
    path: "/",
    Component: MainLayout,
    children: [
      { index: true, Component: Home },
      { path: "/login", Component: Login },
      { path: "/signup", Component: SignUp },
    ],
  },
]);
```

Just tell me!
```
