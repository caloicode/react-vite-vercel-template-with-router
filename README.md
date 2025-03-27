
# React Template Setup Guide
**React-Vite-Vercel with Router**

This repository contains a customized React template optimized for fast setup with Vite, including configurations for React Router and deployment on Vercel. 

### Manual Installation Steps

*Some modules in this repository may be deprecated, follow these steps for a manual installation:*

```bash
 npm create vite@latest filename --template react
 npm i
```

### Basic File Structure
- node_modules/
- public/
    - assets/
    - fonts/
- src/
    - components/
    - pages/
    - `App.jsx`
    - `main.jsx`
    - `App.css`
- `index.html`


**Notes:**  
*The style.css file must be linked to the index.html file:*  
```jsx
<link rel="stylesheet" href="src/style.css">
```  

Include in the `main.jsx`:
```jsx
`import './App.css'`
```

When referencing assets from components, use relative paths:  
```jsx
<img src="../assets/image.jpg"/>
```

When referencing from the public folder,  you can use an absolute path starting with `/`
```jsx
<img src="/image.jpg">
```

### Adding a React Router ###
Installation:
```bash
npm i react-router-dom
```

Update the `App.jsx` file to include Browser Router for routing *(see sample code)*:
```jsx
import { BrowserRouter, Routes, Route } from "react-router-dom";
import Home from "./pages/Home";
import About from "./pages/About";
import Contact from "./pages/Contact";

function App() {
  return (
    <>
      <BrowserRouter>
        <Routes>
          <Route index element={<Home />} />

          <Route path="/home" element={<Home />} />
          <Route path="/about" element={<About />} />
          <Route path="/contact" element={<Contact />} />
        </Routes>
      </BrowserRouter>
    </>
  );
}

export default App;

```
### Enable Live Preview on Different Devices ###
To enable live preview on different devices via your local network, add the following script in the `package.json`:
```json 
"scripts": {
  "dev": "vite --host"
}
```
### Deployment on Vercel ###
Add deploy script to the `package.json`:
```json
"scripts": {
  "deploy": "vercel --prod"
}
```
Create a `vercel.json` file in the project root with the following content to make React Router work during deployment:
```json
{
  "rewrites": [
    { "source": "/(.*)", "destination": "/" }
  ]
}
```
This configuration ensures that all routing will be handled by the React app, preventing issues with browser navigation after deployment.
### Tailwind CSS Installation ###
Follow the steps provided here: [TailwindCSS-Vite Setup](https://tailwindcss.com/docs/installation/using-vite).
#### Defining a Custom Class ###
```css
@import "tailwindcss";

@layer components {
 .centered-container {
  @apply flex justify-center items-center w-screen h-screen bg-pink-500;
 }
}
```
If you have dark mode implemented, make sure to add this code below `@import "tailwindcss";`: 
```css
@custom-variant dark (&:where(.dark, .dark *));
```
