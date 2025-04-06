Zustand store is a centralized container for state and actions (functions that modify the state). Zustand separates the logic for store creation from hooks that are used to React interactions. Zustand provides different API functions for store creation like `create` or `createStore`.

# Creation APIs
## `create`
The function `create()` is used to create a React hook bound to a store. This is the most common way to use Zustand. It creates a hook that can be called in React components:
```ts
const useStore = create((set) => ({
	count: 0,
	increment: () => set((state) => ({ count: state.count + 1 })),
}))
```
## `createStore`
The function `createStore()` creates a store without react hook bindings. The hook can be bound later using function `useStore()`  provided by Zustand API.
Here is how to create the store:
```ts
import { createStore } from 'zustand/vanilla'

const counterStore = createStore((set) => ({
  count: 0,
  increment: () => set((state) => ({ count: state.count + 1 })),
}))
```
And here is how it could be used:
```ts
import { useStore } from 'zustand'
const count = useStore(counterStore, (state) => state.count)
```
This is used when separation of store logic from react is desirable and for creation of reusable stores or stores with multiple instances.
## `createWithEqualityFn`
This function is used to define custom equality check for selecting state. This allows to override zustands shallow compare behavior when deciding when to re-render.
```ts
import { createWithEqualityFn } from 'zustand/traditional'

const useStore = createWithEqualityFn((set) => ({
  count: 0,
  increment: () => set((state) => ({ count: state.count + 1 })),
}))
```
It is used the same way as `create` but it allows developer to pass custom comparison function. This is useful when we need precise control over React re-renders based on state changes.

# Internal store
When creating the store with [[Zustand Store#`create`|create()]] API Zustand in the background creates internal store. The resulting object is self-contained "hook+store" combo, this is perfect for most situations:
```ts
export const useCounter = create(...) // Hook + internal store
```
It is used like this:
```ts
const count = useCounter(state => state.count)
```
# Explicit store
When creating the store with [[Zustand Store#`createStore`|createStore()]] the result is store instance where we have explicit access to the store instance.