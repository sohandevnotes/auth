# 📚 **Table of Contents**
- ✨ Create Vite Project  
- 📁 Navigate Into Project  
- ⚛️ Install React  
- 🎨 Install Tailwind CSS  
- 🌈 Install DaisyUI  
- ✒️ Add Urbanist Font  
- 🛣️ Install React Router  
- 🧭 Create Routes  
- 🔌 Enable Router  
- 🔔 Toast Notifications  
- 🔥 Firebase Setup  
- 👤 Auth Context  
- 🟦 Auth Provider  

---

# ✨ Create Vite Project  
<div style="background:linear-gradient(90deg,#ff00cc,#3333ff);padding:12px;border-radius:10px;color:white;font-weight:bold;">
🚀 Create your Vite project  
</div>

```bash
npm create vite@latest my-project
````

🎉 Project created successfully!

---

# 📁 Navigate Into Project

<div style="background:linear-gradient(90deg,#00eaff,#0066ff);padding:12px;border-radius:10px;color:black;font-weight:bold;">
📁 Move into your new project folder  
</div>

```bash
cd my-project
```

---

# ⚛️ Install React

```bash
npm install
```

---

# 🎨 Install Tailwind CSS

<div style="background:linear-gradient(90deg,#39ff14,#0aff9d);padding:12px;border-radius:10px;color:black;font-weight:bold;">
🎨 Install Tailwind + Setup  
</div>

```bash
npm install tailwindcss
```

**vite.config.ts**

```ts
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import tailwindcss from "@tailwindcss/vite";

export default defineConfig({
  plugins: [react(), tailwindcss()],
});
```

**index.css**

```css
@import "tailwindcss";
```

---

# 🌈 Install DaisyUI

<div style="background:linear-gradient(90deg,#ff7a00,#ff006a);padding:12px;border-radius:10px;color:white;font-weight:bold;">
🌸 Add DaisyUI  
</div>

```bash
npm i -D daisyui@latest
```

```css
/* src/index.css */
 @plugin "daisyui" {
   themes: light --default, dark --prefersdark;
   themes: light --default;
 }
```

---

# ✒️ Add Urbanist Font

<div style="background:linear-gradient(90deg,#00f0ff,#9d00ff);padding:12px;border-radius:10px;color:white;font-weight:bold;">
✒️ Add Google Font — Urbanist  
</div>

```css
/* Import Urbanist font */
@import url('https://fonts.googleapis.com/css2?family=Urbanist:ital,wght@0,100..900;1,100..900&display=swap');

/* Apply to body */
body {
    font-family: "Urbanist", sans-serif;
    font-optical-sizing: auto;
    font-style: normal;
}
```

---

# 🛣️ Install React Router

```bash
npm i react-router
```

---

# 🧭 Create Routes

```jsx
// src/routes/routes.jsx
import { createBrowserRouter } from "react-router";

export const router = createBrowserRouter([
  {
    path: "/",
    element: <div>Hello World</div>,
  },
]);
```

---

# 🔌 Enable Router

```jsx
// src/main.jsx
import React from "react";
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

# 🔔 Toast Notifications

```bash
npm install react-hot-toast
```

```jsx
import { Toaster } from "react-hot-toast";

<Toaster position="top-right" reverseOrder={false} />
```

---

# 🔥 Firebase Setup

```bash
npm install firebase
```

```js
// src/firebase/firebase.config.js
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

---

# 👤 Auth Context

```jsx
// src/providers/AuthContext.jsx
import { createContext } from 'react'
export const AuthContext = createContext(null)
```

---

# 🟦 Auth Provider

```jsx
// src/providers/AuthProvider.jsx
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
