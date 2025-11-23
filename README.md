# 📚 Table of Contents

1. 🚀 Create Vite Project
2. 📁 Navigate Into Project
3. ⚛️ Install React
4. 🎨 Install Tailwind CSS
5. 🌈 Install DaisyUI
6. ✒️ Add Urbanist Font
7. 🛣️ Install React Router
8. 🏗️ Create Layout & Pages
9. 🧭 Create Routes
10. 🔌 Enable Router in `main.jsx`
11. 🔔 Add Toast Notifications
12. 🔥 Firebase Setup
13. 👤 Create Auth Context
14. 🛡️ Create Auth Provider
15. 🛡️ Create `useAuth` Hook
16. 🛡️ Create Login Page
17. 🛡️ Create Signup Page
18. 🛡️ Add Login & Signup Routes
19. 🛡️ Update AuthProvider (createUser)
20. 🛡️ Signup Page with React Hook Form
21. 📦 Install Axios
22. 🖼️ Image Upload Utility
23. 🔄 Final Signup Logic With Image Upload

---

# 🚀 Step 1: Create Vite Project

```bash
npm create vite@latest my-project
```

# 📁 Step 2: Navigate Into Project

```bash
cd my-project
```

# ⚛️ Step 3: Install React

```bash
npm install
```

# 🎨 Step 4: Install Tailwind CSS

```bash
npm install tailwindcss
```

### `vite.config.ts`

```ts
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import tailwindcss from "@tailwindcss/vite";

export default defineConfig({
  plugins: [react(), tailwindcss()],
});
```

### `src/index.css`

```css
@import "tailwindcss";
```

# 🌈 Step 5: Install DaisyUI

```bash
npm i -D daisyui@latest
```

### `src/index.css`

```css
@plugin "daisyui" {
  themes: light --default, dark --prefersdark;
  themes: light --default;
}
```

# ✒️ Step 6: Add Urbanist Font

### `src/index.css`

```css
@import url('https://fonts.googleapis.com/css2?family=Urbanist:wght@100;900&display=swap');

body {
  font-family: "Urbanist", sans-serif;
}
```

# 🛣️ Step 7: Install React Router, Icons & Spinners

```bash
npm i react-router react-icons react-spinners
```

# 🏗️ Step 8: Create Layout & Pages

### `src/layouts/MainLayout.jsx`

```jsx
import { Outlet } from "react-router";

const MainLayout = () => (
  <div>
    <Outlet />
  </div>
);

export default MainLayout;
```

### `src/pages/Home/Home.jsx`

```jsx
const Home = () => (
  <div>
    <h1>Home</h1>
  </div>
);

export default Home;
```

### `src/components/Shared/Container.jsx`

```jsx
const Container = ({ children }) => (
  <div className='max-w-screen-2xl mx-auto xl:px-20 md:px-10 sm:px-2 px-4'>
    {children}
  </div>
);

export default Container;
```

### `src/components/Shared/Button.jsx`

```jsx
const Button = ({ label, onClick, disabled, outline, small, icon: Icon }) => (
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
      ${outline ? "bg-white" : "bg-lime-500"}
      ${outline ? "border-black" : "border-lime-500"}
      ${outline ? "text-black" : "text-white"}
      ${small ? "text-sm" : "text-md"}
      ${small ? "py-1" : "py-3"}
      ${small ? "font-light" : "font-semibold"}
      ${small ? "border" : "border-2"}
    `}
  >
    {Icon && <Icon size={24} className="absolute left-4 top-3" />}
    {label}
  </button>
);

export default Button;
```

### `src/components/Shared/LoadingSpinner.jsx`

```jsx
import { ScaleLoader } from 'react-spinners';

const LoadingSpinner = ({ smallHeight }) => (
  <div className={`${smallHeight ? "h-[250px]" : "h-[70vh]"} flex justify-center items-center`}>
    <ScaleLoader size={100} color='lime' />
  </div>
);

export default LoadingSpinner;
```

### `src/pages/Error/ErrorPage.jsx`

```jsx
import { useNavigate } from "react-router";
import Button from "../../components/Shared/Button";

const ErrorPage = () => {
  const navigate = useNavigate();

  return (
    <section className="bg-white">
      <div className="flex items-center min-h-screen px-6 py-12 mx-auto">
        <div className="text-center max-w-sm mx-auto">
          <p className="p-3 text-sm font-medium text-lime-500 rounded-full bg-blue-50">
            ⚠️
          </p>

          <h1 className="mt-3 text-3xl font-semibold text-gray-800">
            Something Went Wrong!
          </h1>

          <p className="mt-4 text-gray-500">Here are some helpful links:</p>

          <div className="flex items-center w-full mt-6 gap-x-3">
            <button
              onClick={() => navigate(-1)}
              className="px-5 py-2 text-sm text-gray-700 border rounded-lg hover:bg-gray-100"
            >
              🔙 Go Back
            </button>

            <Button label="Take Me Home" onClick={() => navigate("/")} />
          </div>
        </div>
      </div>
    </section>
  );
};

export default ErrorPage;
```

# 🧭 Step 9: Create Routes

### `src/routes/routes.jsx`

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

# 🔌 Step 10: Enable Router in `main.jsx`

### `src/main.jsx`

```jsx
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
Perfect! Let’s continue and complete the **full project with paths for every step**. I’ll keep the same minimal icon-based Markdown style with file paths.

---

# 🔔 Step 11: Add Toast Notifications

```bash
npm install react-hot-toast
```

### `src/main.jsx` (update)

```jsx
import { Toaster } from "react-hot-toast";

<Toaster position="top-right" reverseOrder={false} />
```

# 🔥 Step 12: Firebase Setup

```bash
npm install firebase
```

### `src/firebase/firebase.config.js`

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

### `.env`

```env
VITE_FIREBASE_API_KEY=YOUR_API_KEY
VITE_FIREBASE_AUTH_DOMAIN=YOUR_PROJECT.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=YOUR_PROJECT_ID
VITE_FIREBASE_STORAGE_BUCKET=YOUR_PROJECT.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=YOUR_SENDER_ID
VITE_FIREBASE_APP_ID=YOUR_APP_ID
```

# 👤 Step 13: Create Auth Context

### `src/providers/AuthContext.jsx`

```jsx
import { createContext } from "react";
export const AuthContext = createContext(null);
```

# 🛡️ Step 14: Create Auth Provider

### `src/providers/AuthProvider.jsx`

```jsx
import React from "react";
import { AuthContext } from "./AuthContext";
import { getAuth } from "firebase/auth";
import app from "../firebase/firebase.config";

const auth = getAuth(app);

const AuthProvider = ({ children }) => {
  const authInfo = {};
  return <AuthContext.Provider value={authInfo}>{children}</AuthContext.Provider>;
};

export default AuthProvider;
```

# 🛡️ Step 15: Create `useAuth` Hook

### `src/hooks/useAuth.jsx`

```jsx
import { useContext } from "react";
import { AuthContext } from "../providers/AuthContext";

const useAuth = () => useContext(AuthContext);
export default useAuth;
```

# 🛡️ Step 16: Create Login Page

### `src/pages/Login/Login.jsx`

```jsx
const Login = () => <div><h1>Login</h1></div>;
export default Login;
```

# 🛡️ Step 17: Create Signup Page

### `src/pages/Signup/Signup.jsx`

```jsx
const SignUp = () => <div><h1>SignUp</h1></div>;
export default SignUp;
```

# 🛡️ Step 18: Add Login & Signup Routes

### `src/routes/routes.jsx` (update)

```jsx
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

# 🛡️ Step 19: Update AuthProvider for `createUser`

### `src/providers/AuthProvider.jsx` (update)

```jsx
import React, { useState } from "react";
import { AuthContext } from "./AuthContext";
import {
  createUserWithEmailAndPassword,
  getAuth,
  updateProfile,
} from "firebase/auth";
import app from "../firebase/firebase.config";

const auth = getAuth(app);

const AuthProvider = ({ children }) => {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);

  const createUser = (email, password) => {
    setLoading(true);
    return createUserWithEmailAndPassword(auth, email, password);
  };

  const updateUserProfile = (name, photo) => {
    return updateProfile(auth.currentUser, {
      displayName: name,
      photoURL: photo,
    });
  };

  const authInfo = {
    user,
    setUser,
    loading,
    setLoading,
    createUser,
    updateUserProfile,
  };

  return (
    <AuthContext.Provider value={authInfo}>{children}</AuthContext.Provider>
  );
};

export default AuthProvider;
```

# 🛡️ Step 20: Signup Page With React Hook Form

### `src/pages/Signup/Signup.jsx` (update)

```jsx
import { Link } from "react-router";
import { FcGoogle } from "react-icons/fc";
import { TbFidgetSpinner } from "react-icons/tb";
import { useForm } from "react-hook-form";
import useAuth from "../../hooks/useAuth";

const SignUp = () => {
  const { createUser, loading } = useAuth();

  // React Hook Form
  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm();
  console.log(errors);

  const handelSignUp = async (data) => {
    const { name, image, email, password } = data;
    console.log({ name, image, email, password });

    const imageFile = image[0];
    const formData = new FormData();
    formData.append("image", imageFile);
  };

  return (
    <div className="flex justify-center items-center min-h-screen bg-white">
      <div className="flex flex-col max-w-md p-6 rounded-md sm:p-10 bg-gray-100 text-gray-900">
        <div className="mb-8 text-center">
          <h1 className="my-3 text-4xl font-bold">Sign Up</h1>
          <p className="text-sm text-gray-400">Welcome to PlantNet</p>
        </div>
        <form
          onSubmit={handleSubmit(handelSignUp)}
          noValidate=""
          action=""
          className="space-y-6 ng-untouched ng-pristine ng-valid"
        >
          <div className="space-y-4">
            <div>
              <label htmlFor="email" className="block mb-2 text-sm">
                Name
              </label>
              <input
                type="text"
                id="name"
                placeholder="Enter Your Name Here"
                className="w-full px-3 py-2 border rounded-md border-gray-300 focus:outline-lime-500 bg-gray-200 text-gray-900"
                data-temp-mail-org="0"
                {...register("name", {
                  required: "Name is required",
                  maxLength: {
                    value: 20,
                    message: "Name cannot be too long",
                  },
                })}
              />
              {errors.name && (
                <p className="text-red-500 text-xs mt-1">
                  {errors.name.message}
                </p>
              )}
            </div>
            {/* Image */}
            <div>
              <label
                htmlFor="image"
                className="block mb-2 text-sm font-medium text-gray-700"
              >
                Profile Image
              </label>
              <input
                name="image"
                type="file"
                id="image"
                accept="image/*"
                className="block w-full text-sm text-gray-500
      file:mr-4 file:py-2 file:px-4
      file:rounded-md file:border-0
      file:text-sm file:font-semibold
      file:bg-lime-50 file:text-lime-700
      hover:file:bg-lime-100
      bg-gray-100 border border-dashed border-lime-300 rounded-md cursor-pointer
      focus:outline-none focus:ring-2 focus:ring-lime-400 focus:border-lime-400
      py-2"
                {...register("image")}
              />

              <p className="mt-1 text-xs text-gray-400">
                PNG, JPG or JPEG (max 2MB)
              </p>
            </div>
            <div>
              <label htmlFor="email" className="block mb-2 text-sm">
                Email address
              </label>
              <input
                type="email"
                id="email"
                placeholder="Enter Your Email Here"
                className="w-full px-3 py-2 border rounded-md border-gray-300 focus:outline-lime-500 bg-gray-200 text-gray-900"
                data-temp-mail-org="0"
                {...register("email", {
                  required: "Email is required",
                  pattern: {
                    value: /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/,
                    message: "Please enter a valid email",
                  },
                })}
              />
              {errors.email && (
                <p className="text-red-500 text-xs mt-1">
                  {errors.email.message}
                </p>
              )}
            </div>
            <div>
              <div className="flex justify-between">
                <label htmlFor="password" className="text-sm mb-2">
                  Password
                </label>
              </div>
              <input
                type="password"
                autoComplete="new-password"
                id="password"
                placeholder="*******"
                className="w-full px-3 py-2 border rounded-md border-gray-300 focus:outline-lime-500 bg-gray-200 text-gray-900"
                {...register("password", {
                  required: "Password is required",
                  minLength: {
                    value: 6,
                    message: "Password mast be at least 6 char",
                  },
                })}
              />
              {errors.password && (
                <p className="text-red-500 text-xs mt-1">
                  {errors.password.message}
                </p>
              )}
            </div>
          </div>

          <div>
            <button
              type="submit"
              className="bg-lime-500 w-full rounded-md py-3 text-white"
            >
              {loading ? (
                <TbFidgetSpinner className="animate-spin m-auto" />
              ) : (
                "Continue"
              )}
            </button>
          </div>
        </form>
        <div className="flex items-center pt-4 space-x-1">
          <div className="flex-1 h-px sm:w-16 dark:bg-gray-700"></div>
          <p className="px-3 text-sm dark:text-gray-400">
            Signup with social accounts
          </p>
          <div className="flex-1 h-px sm:w-16 dark:bg-gray-700"></div>
        </div>
        <div className="flex justify-center items-center space-x-2 border m-3 p-2 border-gray-300 border-rounded cursor-pointer">
          <FcGoogle size={32} />

          <p>Continue with Google</p>
        </div>
        <p className="px-6 text-sm text-center text-gray-400">
          Already have an account?{" "}
          <Link
            to="/login"
            className="hover:underline hover:text-lime-500 text-gray-600"
          >
            Login
          </Link>
          .
        </p>
      </div>
    </div>
  );
};

export default SignUp;
```

# 📦 Step 21: Install Axios

```bash
npm i axios
```

# 🖼️ Step 22: Image Upload Utility

### `src/utils/imageUpload.js`

```jsx
import axios from "axios";

export const imageupload = async (imageData) => {
  const formData = new FormData();
  formData.append("image", imageData);

  const { data } = await axios.post(
    `https://api.imgbb.com/1/upload?&key=${import.meta.env.VITE_IMGBB_API_KEY}`,
    formData
  );

  return data?.data?.display_url;
};
```

# 🔄 Step 23: Final Signup Logic With Image Upload

### `src/pages/Signup/Signup.jsx` (update `handleSignUp`)

```jsx
import { imageupload } from "../../utils/imageUpload";

const handleSignUp = async (data) => {
  const { name, image, email, password } = data;
  try {
    await createUser(email, password);
    const imgURL = await imageupload(image[0]);
    // Optionally call updateUserProfile(name, imgURL)
    // navigate("/"); toast.success("Signup Successful");
  } catch (err) {
    console.log(err);
  }
};
```
