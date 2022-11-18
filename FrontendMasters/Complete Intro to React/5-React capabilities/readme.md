# React router

- React router is not part of the React package, is a total dependancy.

- to install it

```
 npm install react-router-dom@6.4.1
```

- We can use multiple BrowserRouter to define different react routes in a single application

```jsx
import { createRoot } from "react-dom/client";
import { BrowserRouter, Routes, Route } from "react-router-dom";
import Details from "./Details";
import SearchParams from "./SearchParams";

const App = () => {
  return (
    <BrowserRouter>
      <div>
        <h1>Adopt Me!</h1>
        <Routes>
          <Route path="/details/:id" element={<Details />}></Route>
          <Route path="/" element={<SearchParams />}></Route>
        </Routes>
      </div>
    </BrowserRouter>
  );
};

const container = document.getElementById("root");
const root = createRoot(container);
root.render(<App />);
```

- we use Link instead of ahref to load only the components we need, and not the entire page

```jsx
import { Link } from "react-router-dom";

//....

<Link to={`/details/${id}`} className="pet">
  <div className="image-container">
    <img src={hero} alt={name} />
  </div>
  <div className="info">
    <h1>{name}</h1>
    <h2>{`${animal} — ${breed} — ${location}`}</h2>
  </div>
</Link>;
```

- in order to get the params from the url we use "useParam" hook

```jsx
import { Link } from "react-router-dom";

const { id } = useParams();
```

# React query

react query is used almost anyware right now, it minimize the amount of useEffect in our project, which is a good thing

- to install it

```
npm install @tanstack/react-query@4.10.1
```

- to configure our clientQuery, in our project we do it in our App component since is the parent components of all the components

```jsx
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";

const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      staleTime: Infinity, // we define how much time we want the cache to be kept, if we see infinity the cache will remain as long as the session of the user, if want only 10 min : 1000 * 60 * 10 (since the time is defined in miliseconds)
      cacheTime: Infinity,
    },
  },
});
```

- in order to use react query we need to handle errors in our fetchs

```jsx
const fetchPet = async ({ queryKey }) => {
  const id = queryKey[1];
  const apiRes = await fetch(`http://pets-v2.dev-apis.com/pets?id=${id}`);

  if (!apiRes.ok) {
    throw new Error(`details/${id} fetch not ok`);
  }

  return apiRes.json();
};

export default fetchPet;
```

- we use React query like this

```jsx
import { useQuery } from "@tanstack/react-query";
import fetchPet from "./fetchPet";

const results = useQuery(["details", id], fetchPet); // the first parameter is used for cache purposes, react query cheks if he had a query named details with the a given id, then don't make an http request she just uses the cache
if (results.isLoading) {
  return (
    <div className="loading-pane">
      <h2 className="loader">🌀</h2>
    </div>
  );
}

const pet = results.data.pets[0];
```

# Uncontrolled Form

with uncontrolled forms, we don't use states to track the individual inputs of a form, but instead we get the values of a form when the user submit it, using "onSubmit", and FormData object

```jsx
<form
        onSubmit={(e) => {
          e.preventDefault();
          const formData = new FormData(e.target);
          const obj = {
            animal: formData.get("animal") ?? "",
            breed: formData.get("breed") ?? "",
            location: formData.get("location") ?? "",
          };
          setRequestParams(obj);
        }}
      >

      <input id="Location" name="Location" placeholder="Location" />

```

# Class components

```jsx
import { Component } from "react";

class Carousel extends Component {
  state = {
    active: 0,
  };

  static defaultProps = {
    images: ["http://pets-images.dev-apis.com/pets/none.jpg"],
  };

  render() {
    const { active } = this.state;
    const { images } = this.props;
    return (
      <div className="carousel">
        <img src={images[active]} alt="animal" />
        <div className="carousel-smaller">
          {images.map((photo, index) => (
            // eslint-disable-next-line
            <img
              key={photo}
              src={photo}
              className={index === active ? "active" : ""}
              alt="animal thumbnail"
            />
          ))}
        </div>
      </div>
    );
  }
}

export default Carousel;
```
