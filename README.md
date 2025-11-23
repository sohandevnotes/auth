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

---

## 🚀 Step 1: Create Vite Project

```bash
npm create vite@latest my-project
```

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

### Update `vite.config.ts`

```ts
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import tailwindcss from "@tailwindcss/vite";

export default defineConfig({
  plugins: [react(), tailwindcss()],
});
```

### Update `index.css`

```css
@import "tailwindcss";
```

---

## 🌈 Step 5: Install DaisyUI

```bash
npm i -D daisyui@latest
```

### Add plugin in `index.css`

```css
@plugin "daisyui" {
  themes: light --default, dark --prefersdark;
  themes: light --default;
}
```

---

## ✒️ Step 6: Add Urbanist Font

```css
@import url('https://fonts.googleapis.com/css2?family=Urbanist:ital,wght@0,100..900;1,100..900&display=swap');

body {
  font-family: "Urbanist", sans-serif;
  font-optical-sizing: auto;
  font-style: normal;
}
```

---

## 🛣️ Step 7: Install React Router & Loading Spinner

```bash
npm i react-router react-spinners
```

---

## 🏗️ Step 8: Create Layout & Pages

### `MainLayout.jsx`

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

### `Home.jsx`

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

### `Container.jsx`

```jsx
const Container = ({ children }) => {
  return (
    <div className='max-w-screen-2xl mx-auto xl:px-20 md:px-10 sm:px-2 px-4'>
      {children}
    </div>
  )
}

export default Container
```

### `Button.jsx`

```jsx
const Button = ({ label, onClick, disabled, outline, small, icon: Icon }) => {
  return (
    <button
      disabled={disabled}
      onClick={onClick}
      className={`
        relative
        disabled:opacity-70
        disabled:cursor-not-allowed
        rounded-lg
        hover:opacity-80
        transition
        cursor-pointer
        px-4
        w-full
        ${outline ? 'bg-white' : 'bg-lime-500'}
        ${outline ? 'border-black' : 'border-lime-500'}
        ${outline ? 'text-black' : 'text-white'}
        ${small ? 'text-sm' : 'text-md'}
        ${small ? 'py-1' : 'py-3'}
        ${small ? 'font-light' : 'font-semibold'}
        ${small ? 'border' : 'border-2'}
      `}
    >
      {Icon && (
        <Icon size={24} className='absolute left-4 top-3' />
      )}
      {label}
    </button>
  )
}

export default Button
```

### `LoadingSpinner.jsx`

```jsx
import { ScaleLoader } from 'react-spinners'

const LoadingSpinner = ({ smallHeight }) => {
  return (
    <div
      className={`${smallHeight ? 'h-[250px]' : 'h-[70vh]'}
      flex flex-col justify-center items-center`}
    >
      <ScaleLoader size={100} color='lime' />
    </div>
  )
}

export default LoadingSpinner
```

### `ErrorPage.jsx`

```jsx
import { useNavigate } from 'react-router'
import Button from "../../components/Shared/Button";

const ErrorPage = () => {
  const navigate = useNavigate()

  return (
    <section className='bg-white '>
      <div className='container flex items-center min-h-screen px-6 py-12 mx-auto'>
        <div className='flex flex-col items-center max-w-sm mx-auto text-center'>
          <h1 className='mt-3 text-2xl font-semibold text-gray-800 md:text-3xl'>
            Something Went Wrong!
          </h1>

          <p className='mt-4 text-gray-500'>Here are some helpful links:</p>

          <div className='flex items-center w-full mt-6 gap-x-3 sm:w-auto'>
            <button
              onClick={() => navigate(-1)}
              className='flex items-center justify-center w-1/2 px-5 py-1 text-sm text-gray-700 border rounded-lg hover:bg-gray-100'
            >
              <span>Go back</span>
            </button>

            <Button label='Take Me Home' onClick={() => navigate('/')} />
          </div>
        </div>
      </div>
    </section>
  )
}

export default ErrorPage
```

---

## 🧭 Step 9: Create Routes

```jsx
import { createBrowserRouter } from "react-router";
import MainLayout from "../layouts/MainLayout";
import Home from "../pages/Home/Home";
import ErrorPage from "../pages/Error/ErrorPage";
import LoadingSpinner from "../components/Shared/LoadingSpinner";

export const router = createBrowserRouter([
  {
    path: "/",
    Component: MainLayout,
    errorElement: <ErrorPage />,
    hydrateFallbackElement: <LoadingSpinner />,
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

Add to `main.jsx`:

```jsx
import { Toaster } from "react-hot-toast";

<Toaster position="top-right" reverseOrder={false} />
```

---

## 🔥 Step 12: Firebase Setup

```bash
npm install firebase
```

### `firebase.config.js`

```jsx
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

### `.env`

```ini
VITE_FIREBASE_API_KEY=YOUR_API_KEY
VITE_FIREBASE_AUTH_DOMAIN=YOUR_PROJECT.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=YOUR_PROJECT_ID
VITE_FIREBASE_STORAGE_BUCKET=YOUR_PROJECT.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=YOUR_SENDER_ID
VITE_FIREBASE_APP_ID=YOUR_APP_ID
```

---

## 👤 Step 13: Create Auth Context

```jsx
import { createContext } from "react";
export const AuthContext = createContext(null);
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

## 🛡️ Step 15: Create useAuth Hook

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

```jsx
import { createBrowserRouter } from "react-router";
import MainLayout from "../layouts/MainLayout";
import Home from "../pages/Home/Home";
import ErrorPage from "../pages/Error/ErrorPage";
import LoadingSpinner from "../components/Shared/LoadingSpinner";
import Login from "../pages/Login/Login";
import SignUp from "../pages/Signup/Signup";

export const router = createBrowserRouter([
  {
    path: "/",
    Component: MainLayout,
    errorElement: <ErrorPage />,
    hydrateFallbackElement: <LoadingSpinner />,
    children: [
      { index: true, Component: Home },
      { path: "/login", Component: Login },
      { path: "/signup", Component: SignUp },
    ],
  },
]);
```

Just tell me!
