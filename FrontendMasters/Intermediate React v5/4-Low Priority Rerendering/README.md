# Deferred Values

```jsx
// replace react import
import { useContext, useDeferredValue, useMemo, useState } from "react";

// under pets declaration
const deferredPets = useDeferredValue(pets);
const renderedPets = useMemo(
  () => <Results pets={deferredPets} />,
  [deferredPets]
);

// replace <Results /> line
{
  renderedPets;
}
```

# UseTransition
