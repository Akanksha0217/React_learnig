# Skeleton Loading in React

## What is a Skeleton Loader?

A **Skeleton Loader** is a placeholder UI that mimics the structure of the actual content while data is loading.

Instead of displaying a blank screen or only a loading spinner, a skeleton loader shows grey boxes or animated placeholders representing the content that will appear.

---

# Why Do We Need a Skeleton Loader?

When data is fetched from an API, it takes some time to load.

Without a Skeleton Loader:

- Users may see a blank screen.
- Users don't know what content is loading.
- The application may feel slow.

With a Skeleton Loader:

- Users can see the layout immediately.
- The application feels faster.
- It provides a better user experience.

---

# Example Without Skeleton Loader

```jsx
function App() {
  const [movies, setMovies] = useState([]);

  if (movies.length === 0) {
    return <h2>Loading...</h2>;
  }

  return <MovieList />;
}
```

### Output

```
Loading...
```

---

# Example With Skeleton Loader

```jsx
function App() {
  const [movies, setMovies] = useState([]);

  if (movies.length === 0) {
    return <MovieSkeleton />;
  }

  return <MovieList />;
}
```

### Output While Loading

```
-----------------------
█████████████████████

██████████████

██████████████████
-----------------------
```

After loading

```
Movie 1
Movie 2
Movie 3
```

---

# Basic Skeleton Component

```jsx
function Skeleton() {
  return (
    <div className="skeleton"></div>
  );
}
```

---

# CSS for Skeleton

```css
.skeleton {
  width: 200px;
  height: 20px;
  background-color: #ddd;
  border-radius: 4px;
}
```

Output

```
████████████████
```

---

# Animated Skeleton

```css
.skeleton {
  width: 200px;
  height: 20px;
  background: linear-gradient(
    90deg,
    #eeeeee 25%,
    #dddddd 50%,
    #eeeeee 75%
  );
  background-size: 200% 100%;
  animation: loading 1.5s infinite;
}

@keyframes loading {
  from {
    background-position: 200% 0;
  }

  to {
    background-position: -200% 0;
  }
}
```

This creates a smooth shimmer effect.

---

# Real React Example

```jsx
function MovieSkeleton() {
  return (
    <>
      <div className="poster"></div>
      <div className="title"></div>
      <div className="description"></div>
    </>
  );
}
```

Output

```
██████

████████████

█████████████████
```

---

# Fetching API Example

```jsx
function Movies() {
  const [movies, setMovies] = useState(null);

  useEffect(() => {
    fetch("/movies")
      .then((res) => res.json())
      .then((data) => setMovies(data));
  }, []);

  if (!movies) {
    return <MovieSkeleton />;
  }

  return <MovieList movies={movies} />;
}
```

Flow

```
Page Opens
      ↓
API Request Sent
      ↓
Skeleton Displayed
      ↓
API Response Received
      ↓
Actual Data Displayed
```

---

# Skeleton vs Loading Spinner

## Spinner

```jsx
<h2>Loading...</h2>
```

Output

```
Loading...
```

---

## Skeleton

```jsx
<MovieSkeleton />
```

Output

```
████████████

██████████████████

██████████████
```

Skeleton provides a better visual representation of the upcoming content.

---

# Skeleton with Suspense

```jsx
<Suspense fallback={<MovieSkeleton />}>
  <MovieList />
</Suspense>
```

Flow

```
Component Starts Loading
        ↓
MovieSkeleton Appears
        ↓
Component Loads
        ↓
Movie List Appears
```

---

# Netflix Example

When Netflix loads:

- Movie posters appear as grey boxes.
- Titles appear as grey lines.
- After the API responds, the real posters and titles replace the placeholders.

This is a Skeleton Loader.

---

# Popular Skeleton Libraries

### React Loading Skeleton

Install

```bash
npm install react-loading-skeleton
```

Example

```jsx
import Skeleton from "react-loading-skeleton";
import "react-loading-skeleton/dist/skeleton.css";

function App() {
  return (
    <>
      <Skeleton height={200} />
      <Skeleton count={3} />
    </>
  );
}
```

---

# Advantages

- Improves user experience.
- Makes the application feel faster.
- Prevents blank screens.
- Shows the expected layout before data loads.
- Commonly used in modern web applications.

---

# Disadvantages

- Requires additional UI design.
- Slightly increases development time.
- If overused, it may not improve user experience.

---

# Skeleton vs Spinner

| Skeleton Loader | Loading Spinner |
|-----------------|-----------------|
| Shows page layout | Shows only a loading icon or text |
| Better user experience | Basic loading indication |
| Makes app feel faster | Can make waiting feel longer |
| Common in modern apps | Common in simple apps |

---

# Interview Questions

## 1. What is a Skeleton Loader?

A Skeleton Loader is a placeholder UI that represents the layout of the content while data is loading.

---

## 2. Why do we use Skeleton Loaders?

To improve user experience by showing the page structure instead of a blank screen or simple loading text.

---

## 3. What is the difference between a Skeleton Loader and a Spinner?

A Spinner only indicates loading, while a Skeleton Loader previews the layout of the content.

---

## 4. Can Skeleton Loaders be used with Suspense?

Yes.

```jsx
<Suspense fallback={<MovieSkeleton />}>
  <MovieList />
</Suspense>
```

---

## 5. When should you use a Skeleton Loader?

- While waiting for API responses.
- While lazy-loaded components are loading.
- In dashboards, e-commerce sites, and streaming applications.
- When displaying lists, cards, or images.

---

## 6. Which library is commonly used for Skeleton Loaders in React?

```text
react-loading-skeleton
```

---

# Real-World Examples

Many popular applications use Skeleton Loaders:

- Netflix
- YouTube
- Facebook
- Instagram
- LinkedIn
- Amazon

---

# Key Points

- A Skeleton Loader is a placeholder UI shown while content is loading.
- It improves perceived performance and user experience.
- It is commonly used with API calls and `Suspense`.
- It displays the layout of the page before actual data is available.
- Skeleton Loaders are generally preferred over simple loading spinners in modern applications.
