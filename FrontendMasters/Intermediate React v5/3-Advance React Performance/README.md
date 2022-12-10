# Code splitting

when loading application in browsers, we have to take care of the size of our application, we should only load the minimal things the first time and not everything.

to do so, we use "lazy" and "suspense".

for example the Details and SearchParams components will not be loaded until they are requested.

we put the lazy loaded components inside a Suspense component, and we add a fallback which is what is displayed until the lazy components are loaded.

```jsx
import { useState, lazy, Suspense } from "react";

const Details = lazy(() => import("./Details"));
const SearchParams = lazy(() => import("./SearchParams"));

const App = () => {
  const adoptedPet = useState(null);
  return (
    <div>
      <BrowserRouter>
        <AdoptedPetContext.Provider value={adoptedPet}>
          <QueryClientProvider client={queryClient}>
            <Suspense
              fallback={
                <div className="loading-pane">
                  <h2 className="loader">🌀</h2>
                </div>
              }
            >
              <header>
                <Link to="/">Adopt Me!</Link>
              </header>
              <Routes>
                <Route path="/details/:id" element={<Details />} />
                <Route path="/" element={<SearchParams />} />
              </Routes>
            </Suspense>
          </QueryClientProvider>
        </AdoptedPetContext.Provider>
      </BrowserRouter>
    </div>
  );
};
```

and we can do the same for example for Modals, we can load them only if they are requested

```jsx
const Modal = lazy(() => import("./Modal"));
```

# Server side rendering

we add a file named ClientApp.jsx, and we put in there everything that will be rendered in the browser (like google analytics or windows or alert)

```jsx
import { hydrateRoot } from "react-dom/client";
import { BrowserRouter } from "react-router-dom";
import App from "./App";

hydrateRoot(
  document.getElementById("root"),
  <BrowserRouter>
    <App />
  </BrowserRouter>
  //document.getElementById("root")
);
```

and index.html now will load ClientApp.jsx

```html
<script type="module" src="./ClientApp.jsx"></script>
```

must watch the video
