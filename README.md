## 📚 Table of Contents
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
15. 🛡️ Step 15: Create Login.jsx Page
16. 🛡️ Step 16: Create Signup.jsx Page
17. 🛡️ Step 17: Add Login & Signup Routes

---

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

Update `vite.config.ts`:

```ts
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import tailwindcss from "@tailwindcss/vite";

export default defineConfig({
  plugins: [react(), tailwindcss()],
});
```

Update `index.css`:

```css
/* src/index.css */
@import "tailwindcss";
```

---

## 🌈 Step 5: Install DaisyUI

```bash
npm i -D daisyui@latest
```

Add plugin in `index.css`:

```css
/* src/index.css */
 @plugin "daisyui" {
   themes: light --default, dark --prefersdark;
   themes: light --default;
 }
```

---

## ✒️ Step 6: Add Urbanist Font

```css
/* src/index.css */
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

**MainLayout.jsx**

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

**Home.jsx**

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

Enable in `main.jsx`:

```jsx
import { Toaster } from "react-hot-toast";

<Toaster position="top-right" reverseOrder={false} />
```

---

## 🔥 Step 12: Firebase Setup

```bash
npm install firebase
```

**firebase.config.js**

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

**.env**

```
VITE_FIREBASE_API_KEY=AIzaSyC6utz_eFX05NaoQUpALmPn1z0rCDU6_iE
VITE_FIREBASE_AUTH_DOMAIN=ankur-48a58.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=ankur-48a58
VITE_FIREBASE_STORAGE_BUCKET=ankur-48a58.firebasestorage.app
VITE_FIREBASE_MESSAGING_SENDER_ID=749073347715
VITE_FIREBASE_APP_ID=1:749073347715:web:8f1bcbe21b39b2ffbe57b6
```

---

## 👤 Step 13: Create Auth Context

```jsx
import { createContext } from 'react'
export const AuthContext = createContext(null)
```

---

## 🛡️ Step 14: Create Auth Provider

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

## 🛡️ Step 15: Create Login.jsx Page

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

## 🛡️ Step 16: Create Signup.jsx Page

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

## 🛡️ Step 17: Add Login & Signup Routes

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
