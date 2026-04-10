# 🎬 MovieDux: Advanced React Hooks & State Orchestration

I developed **MovieDux** as a React-based cinema discovery project. While the UI presents a sleek movie browsing experience, the core of the project is a technical deep-dive into **React Functional Components**, **Hook-driven state management**, and **dynamic data filtering**.

The application operates as a self-contained ecosystem using a local JSON "database," focusing on the architectural challenges of synchronizing state across multiple views and managing complex user interactions.

---

## 🏗️ Architecture & Technical Design

The project follows a **Unidirectional Data Flow** pattern, where `App.js` serves as the "Single Source of Truth."

### 📂 Directory Structure
```text
Movie-Site-React/
├── public/
│   ├── images/          # Local movie posters & assets
│   ├── movies.json      # Central static data repository
│   └── index.html       # Entry point
├── src/
│   ├── components/
│   │   ├── Header.js      # Stateless branding component
│   │   ├── Footer.js      # Stateless informational component
│   │   ├── MovieCard.js   # Logic-heavy presentational component
│   │   ├── MoviesGrid.js  # State-managed filtering engine
│   │   └── Watchlist.js   # Filtered view of the global state
│   ├── App.js           # Core Orchestrator (State & Routing)
│   ├── styles.css       # Global design system & utility classes
│   └── index.js         # React DOM initialization
└── package.json         # Dependency manifest
```

### 🧠 Core Logic & Hooks Usage
1.  **Global State Management (`App.js`)**:
    * Uses `useState` to maintain the master list of `movies` and a `watchlist` (an array of IDs).
    * Uses `useEffect` with an empty dependency array to simulate a database fetch on mount.
    * Implements a `toggleWatchlist` function that handles both addition and removal logic, passed down via props.
2.  **Filter Orchestration (`MoviesGrid.js`)**:
    * Manages three distinct local states (`searchTerm`, `genre`, `rating`).
    * Implements a **composite filtering logic** that ensures all three criteria must be met simultaneously before rendering.
3.  **UI Resilience (`MovieCard.js`)**:
    * Features an `onError` handler for images to prevent broken layouts if a poster is missing.
    * Uses dynamic template literals to apply CSS classes based on numerical rating thresholds.

---

## ✨ Feature Deep-Dive

### 🔍 Advanced Filtering System
The `MoviesGrid` doesn't just display data; it processes it. Users can slice the data by:
* **Textual Matching**: Real-time search that filters as you type.
* **Category Selection**: Dropdown filtering for specific genres (Action, Drama, etc.).
* **Performance Metrics**: A custom "Rating" filter that categorizes movies into "Good" (8+), "Ok" (5-8), and "Bad" (<5).

### 🏷️ Smart Watchlist
The Watchlist isn't just a separate page; it's a dynamic view of the master data.
* The `Watchlist` component maps over the ID array and uses `.find()` to retrieve full movie objects from the master list.
* The "In Watchlist" toggle state is synchronized globally; removing a movie from the Watchlist view immediately updates its status in the main Grid.

### 🎨 Dynamic Styling
* **Rating Indicators**: Ratings are color-coded using a helper function (`getRatingClass`) to provide immediate visual feedback.
* **Conditional Rendering**: The UI adapts based on whether a movie is currently in the user's list, changing the toggle label and state.

---

## 🛠️ Tech Stack & Skills Covered

| Category | Technology | Concepts Applied |
| :--- | :--- | :--- |
| **Framework** | React 18+ | Functional Components, Props, Lifting State |
| **State** | Hooks | `useState`, `useEffect`, Array Manipulation |
| **Routing** | React Router v6 | `BrowserRouter`, `Routes`, `Link` |
| **Data** | JSON / Fetch | Asynchronous Data Loading, Local API Simulation |
| **Styling** | CSS3 | Flexbox, Grid, Dynamic Class Binding |

---

## 🔍 Code Review & Best Practices

* **Locality of Behavior**: The `MovieCard` handles its own internal logic (rating classes and image errors), keeping the `MoviesGrid` clean.
* **Pure Functions**: Filtering logic (`matchesGenre`, `matchesRating`) is decoupled from the JSX for better readability and testability.
* **Robust State Updates**: The watchlist toggle uses the **functional update pattern** (`prev => ...`) to ensure state integrity during rapid user interactions.

---

## 🚀 How to Run

1. **Clone the project**
   ```bash
   git clone https://github.com/seanwhs/Movie-Site-React.git
   ```
2. **Install node modules**
   ```bash
   npm install
   ```
3. **Execute**
   ```bash
   npm start
   ```

---

**Developed by Sean**
*A project dedicated to exploration of the React Hook.*
