# useRef

we use useRef to store a DOM element in a variable between renders

```jsx
const renderTarget = useRef();
<div ref={renderTarget} className="scene"></div>; // this div will be stored in a renderTarget variable

// we can use this element stored in the variable using current
renderTarget.current.appendChild(renderer.domElement); // we append to the div
```

# useReducer

useState and useReducer are basically the same, we useReducer to handle a more complex state in a component

# useMemo

is used for performance.

we use it, to tell react do not call something when a component re-render, for example 'the expensiveMathOperation function' will not be called unless the count variable changes.

we use useMemo only to cache expensive traitements.

```jsx
const [count, setCount] = useState(35);
const value = useMemo(() => expensiveMathOperation(count), [count]);

// use effect make the component re-render but the expensiveMathOperation will not be called
useEffect(() => {
  requestAnimationFrame(animate);
  function animate() {
    setLeft(left + 1);
  }
}, [left]);
```

# useCallback

is used for performance.

we use it to store a callback function that will not change frequently to not cause a child component to re-render for example.

```jsx
  const aUsefulCallback = () => {};
  const memoizedCallback = useCallback(aUsefulCallback, []);

  return (
   //....
      <UseRefComponent cb={memoizedCallback} />
    </div>
  );
```

and in the child component we have to use the function meme

```jsx
//UseRefComponent

const UseRefMemo = memo(function UseRef() {
  //....
});
```

we can useMemo instead of use callback

```jsx
const aUsefulCallback = () => {};
const memoizedCallback = useMemo(() => aUsefulCallback, []);

  return (
   //....
      <UseRefComponent cb={memoizedCallback} />
    </div>
  );
```

# useLayoutEffect

useEffect allows you perform side effects from a function component. When useEffect is called, React knows to render your side effect only after changes are made to the DOM
By default, React runs the effect after every render - including the first render. This is to say that useEffect is effected only after the component is rendered.

But if you need your side effect to fire synchronously after the DOM mutation, that is, before the next browser paint without the user ever noticing any flickering or visual inconsistency then you need to use useLayoutEffect

useLayoutEffect fires synchronously after the DOM mutation and before the browser get to paint the new changes. This hook is especially useful for performing DOM measurement like scroll height, scroll width, scroll position and other style on any DOM element.

```jsx
useLayoutEffect(() => {
  setWidth(el.current.clientWidth);
  setHeight(el.current.clientHeight);
});
```

# useId

useId is a React Hook for generating unique IDs that can be passed to accessibility attributes.

```jsx
function LabelInputPair() {
  const id = useId();
  return (
    <div style={{ marginBottom: '50px' }}>
      <label htmlFor={id}>
        Click on this label and it'll highlight the input {id}
      </label>
      <br />
      <input type="text" id={id} placeholder={`input id ${id}`} />
    </div>
  );
}
```
