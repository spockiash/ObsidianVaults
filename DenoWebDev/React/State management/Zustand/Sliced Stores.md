Stores can be sliced into segments called slices. They can be combined together in bounded store. For example we can have first store:
```ts
export const createFishSlice = (set) => ({
  fishes: 0,
  addFish: () => set((state) => ({ fishes: state.fishes + 1 })),
})
```
Then second store:
```ts
export const createBearSlice = (set) => ({
  bears: 0,
  addBear: () => set((state) => ({ bears: state.bears + 1 })),
  eatFish: () => set((state) => ({ fishes: state.fishes - 1 })),
})
```
And we then combine them like this:
```ts
import { create } from 'zustand'
import { createBearSlice } from './bearSlice'
import { createFishSlice } from './fishSlice'

export const useBoundStore = create((...a) => ({
  ...createBearSlice(...a),
  ...createFishSlice(...a),
}))
```
The `...a` is shorthand for triple of parameters `set`, `get` and `api`. Zustand behind the scenes constructs the combined store according to those.
## Adding types into sliced stores
We can add types for better code clarity like this:
```ts
export type Person = {
    firstname: string
    lastname: string
    email: string
    phone: string
    birthday: string
    gender: string
    website: string
    image: string
  }
  
  export type PersonSlice = {
    person: Person | null
    setPerson: (p: Person) => void
  }
  
  export const createPersonSlice = (set: (arg0: { person: Person; }) => void): PersonSlice => ({
    person: null,
    setPerson: (person) => set({ person }),
  })
```
The only boilerplate here is the type setup. Zustand also has state management API for creating slices, but they provide more boilerplate.