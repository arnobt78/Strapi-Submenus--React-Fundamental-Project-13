# Strapi Submenus – React Fundamental Project 13

<img width="1149" alt="Screenshot 2025-02-09 at 16 26 39" src="https://github.com/user-attachments/assets/3a8394f6-c5a8-4af3-9705-7fd5d48886b6" />

---

A hands-on project demonstrating how to build a modern, fully responsive navigation system with submenus in React. This app showcases component-driven design, React Context for state management, dynamic rendering of menu structures, and advanced CSS for a sophisticated user experience. It is an excellent resource for learning and teaching React fundamentals, state patterns, and interface design.

- **Live Demo:** [https://strapi-submenus-arnob.netlify.app/](https://strapi-submenus-arnob.netlify.app/)

---

## Table of Contents

1. [Project Summary](#project-summary)
2. [Features](#features)
3. [Technology Stack](#technology-stack)
4. [Project Structure](#project-structure)
5. [How It Works](#how-it-works)
6. [Setup & Running Instructions](#setup--running-instructions)
7. [Component Walkthrough](#component-walkthrough)
8. [Data and Context](#data-and-context)
9. [Styling & UX](#styling--ux)
10. [Teaching & Learning Notes](#teaching--learning-notes)
11. [Example Code Snippets](#example-code-snippets)
12. [Conclusion](#conclusion)

---

## Project Summary

Strapi Submenus is an educational project designed to teach and demonstrate:

- How to build a responsive navigation bar with submenus using React.
- Usage of React Context and custom hooks for global state management.
- Dynamic rendering of UI based on structured data.
- Clean, scalable, and component-driven code structure.
- Advanced CSS including 3D effects and transitions for an engaging user experience.

---

## Features

- Responsive sidebar and submenu navigation, adapting to desktop and mobile layouts.
- Dynamic submenu content rendered from a single data source.
- Global context for managing sidebar and submenu open/close state.
- Clean UI using modern CSS, including transitions and 3D submenu effects.
- Keyboard and mouse event handling for a smooth UX.
- Code structure ideal for learning and further extension.

---

## Technology Stack

- **React** (Functional components, hooks)
- **React Context API** (for global state)
- **Vite** (for fast development/build)
- **React Icons** (for iconography)
- **NanoID** (for unique IDs)
- **CSS Variables & Modern CSS** (for styling)

---

## Project Structure

```
Strapi-Submenus--React-Fundamental-Project-13/
│
├── public/
│   └── vite.svg
├── src/
│   ├── App.jsx
│   ├── Context.jsx
│   ├── Hero.jsx
│   ├── Navbar.jsx
│   ├── Sidebar.jsx
│   ├── Submenu.jsx
│   ├── data.jsx
│   └── index.css
├── index.html
├── package.json
└── README.md
```

**Key Files:**
- `App.jsx` – Main entry, renders all UI components
- `Context.jsx` – Provides global state (sidebar/submenu open, pageId, handlers)
- `Navbar.jsx` – Top navigation bar, logo, and toggle button
- `Hero.jsx` – Main hero banner/content
- `Sidebar.jsx` – Sidebar navigation with grouped links
- `Submenu.jsx` – Floating submenu based on hovered link
- `data.jsx` – Structured data source for pages and links
- `index.css` – All global and component styles
- `index.html` – Single-page app root

---

## How It Works

1. **Data-driven UI:** All navigation links and submenus are defined in `data.jsx` as an array of pages, each with its own links and icons.
2. **Global Context:** The `Context.jsx` file exposes state and handlers for opening/closing the sidebar and submenu, as well as tracking the currently active submenu (`pageId`).
3. **Sidebar & Submenu:** 
   - The sidebar displays all navigation groups and their sublinks, shown/hidden via context state and animated with CSS.
   - The submenu appears near the hovered navigation link, dynamically displaying relevant sublinks based on the current `pageId`.
4. **Responsive & Accessible:** The navigation adapts to screen size, showing the sidebar toggle on mobile and horizontal nav with submenus on desktop.
5. **Advanced CSS:** Includes 3D transforms for the submenu, smooth transitions, and responsive layouts.

---

## Setup & Running Instructions

1. **Clone the repository:**
   ```sh
   git clone https://github.com/arnobt78/Strapi-Submenus--React-Fundamental-Project-13.git
   cd Strapi-Submenus--React-Fundamental-Project-13
   ```

2. **Install dependencies:**
   ```sh
   npm install
   ```

3. **Run the development server:**
   ```sh
   npm run dev
   ```

4. **Open in your browser:**
   - Visit `http://localhost:5173` (or the URL provided in your terminal).

---

## Component Walkthrough

### App.jsx

```javascript
import Hero from './Hero';
import Navbar from './Navbar';
import Sidebar from './Sidebar';
import Submenu from './Submenu';

const App = () => (
  <main>
    <Navbar />
    <Hero />
    <Sidebar />
    <Submenu />
  </main>
);

export default App;
```

---

### Navbar.jsx

- Displays the logo and sidebar toggle button.
- Renders navigation links (from data).
- Uses context to open sidebar and set active submenu.

---

### Sidebar.jsx

```javascript
import { FaTimes } from 'react-icons/fa';
import { useGlobalContext } from './Context';
import sublinks from './data';

const Sidebar = () => {
  const { isSidebarOpen, closeSidebar } = useGlobalContext();
  return (
    <aside className={isSidebarOpen ? 'sidebar show-sidebar' : 'sidebar'}>
      <div className='sidebar-container'>
        <button className='close-btn' onClick={closeSidebar}>
          <FaTimes />
        </button>
        <div className='sidebar-links'>
          {sublinks.map(({ links, page, pageId }) => (
            <article key={pageId}>
              <h4>{page}</h4>
              <div className='sidebar-sublinks'>
                {links.map(({ url, icon, label, id }) => (
                  <a key={id} href={url}>
                    {icon}
                    {label}
                  </a>
                ))}
              </div>
            </article>
          ))}
        </div>
      </div>
    </aside>
  );
};
export default Sidebar;
```

---

### Submenu.jsx

- Listens for the current `pageId` from context.
- Dynamically renders the submenu for the active page.
- Uses advanced CSS for 3D effect and smooth appearance/disappearance.

---

### Hero.jsx

Displays a welcoming hero section:

```javascript
const Hero = () => (
  <div className='hero-container'>
    <div className='hero-center'>
      <h1>
        Manage Any Content <br /> Anywhere
      </h1>
      <p>
        Strapi is the leading open-source headless CMS. It’s 100% JavaScript and fully customizable.
      </p>
    </div>
  </div>
);
export default Hero;
```

---

## Data and Context

### `data.jsx` Example

```javascript
const sublinks = [
  {
    pageId: nanoid(),
    page: 'product',
    links: [
      {
        id: nanoid(),
        label: 'community',
        icon: <Fa500Px />,
        url: '/product/community',
      },
      // ...more links
    ],
  },
  // ...more pages
];

export default sublinks;
```

### Global Context (`Context.jsx`)

- Holds `isSidebarOpen`, `isSubmenuOpen`, `pageId`, and functions for opening/closing sidebar and submenu.
- Provides a custom hook `useGlobalContext` for easy state access in components.
- Ensures all components are synchronized and use a single source of truth for navigation state.

---

## Styling & UX

- **CSS Variables:** Used for colors, spacing, and responsive breakpoints.
- **Sidebar & Submenu:** CSS transitions and classes like `.show-sidebar` or `.show-submenu` control visibility.
- **3D Submenu Effect:**
  ```css
  .submenu {
    transform: rotateX(-90deg) translateX(-50%);
    transform-origin: top;
    perspective: 1000px;
    transition: transform 0.3s, opacity 0.2s;
    /* ... */
  }
  .show-submenu {
    opacity: 1;
    visibility: visible;
    transform: rotateX(0deg) translate(-50%);
  }
  ```
- **Responsive Design:** Media queries hide the sidebar on desktop and show nav links, and vice versa on mobile.

---

## Teaching & Learning Notes

- **React Fundamentals:** Project covers components, props, state, context, and hooks.
- **Context API:** Centralizes UI state for clean, maintainable code.
- **Dynamic Rendering:** Menus and submenus created from a single data source demonstrate scalability.
- **CSS Mastery:** Shows real-world usage of variables, transitions, and 3D transforms.
- **Event Handling:** Mouse and click events manage opening/closing of menus, ensuring an interactive UX.

---

## Example Code Snippets

### Opening the Sidebar

```javascript
const { openSidebar } = useGlobalContext();
<button className="toggle-btn" onClick={openSidebar}>Open Sidebar</button>
```

### Rendering NavLinks

```javascript
{ sublinks.map(({ page, pageId }) => (
  <button
    key={pageId}
    className="nav-link"
    onMouseOver={() => setPageId(pageId)}
  >
    {page}
  </button>
))}
```

---

## Conclusion

This project is an excellent teaching tool for React developers looking to master component-driven development, state management with context, and modern CSS techniques. It’s a scalable, real-world example of how to architect a professional navigation system. You can use it as a template for your own apps, or as a step-by-step tutorial for others.

Explore, modify, and extend – happy coding!

---
