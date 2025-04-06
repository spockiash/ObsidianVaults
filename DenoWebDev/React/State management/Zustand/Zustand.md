Zustand is state management library for React. It works with [[Zustand Store|store]] architecture to centralize state management. Instead of using `useState` inside each React component it enables creation of shared state for the components.

# Store creation
## Create store with `create()`
More information can be found [[Zustand Store#Creation APIs|here]] .
When creating the store with this function we use it like this:
```ts
const useSomeStore = create(stateCreatorFn)
```
In practical terms we first define some type and then pass it to the create function as a type specification:
```ts
import { create } from "zustand"

type NavbarStore {
	isOpen: boolean
	toggle: () => void
	close: () => void
	open: () => void
}

export const useNavbar = create<NavbarStore>((set) => ({
	isOpen: false,
	toggle: () => set((state) => ({ isOpen: !state.isOpen })),
	close: () => set({ isOpen: false }),
	open: () => set({ isOpen: true })
}))
```
Then we define custom `stateCreatorFn` as arrow function with `set` function passed as a parameter.
We then assign default values to the store variables and functions inside the lambda body:
```ts
isOpen: false //assign default value to the variable in store
close: () => set({ isOpen: false }),
```
When assigning values to a function we can pass either custom body or reference to some other function defined outside the body.

# Using store
The most basic situation is where we have store with hook created with the `create()` function. Then we can access the function defined inside the store like this:
```ts
const isOpen = useNavbar((state) => state.isOpen) //inside react component
```
We call the created store (named `usedNavbar` in our case) and then we pass it an argument formed with arrow function. This arrow function is called *selector*, it allows to select the function from a store and assign it to constant. React will then re-render only the relevant parts.
