# Simple navbar with `create` demo
When dealing with simple setups the `create()` function is the best in the simplest function. For example we can define navigation bar setup with this:
```ts
// src/store/navbar.ts
import { create } from "zustand"

type NavbarStore = {
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
Then we can use it in our component like this:
```tsx
import { useNavbar } from "../store/navbar.ts";

export default function Navbar() {
    const isOpen = useNavbar((state) => state.isOpen)
    const toggle = useNavbar((state) => state.toggle)

    return (
        <nav className={`navbar ${isOpen ? 'open' : 'collapsed'}`}>
            <div className="navbar-header">
                <h2 className="navbar-title">My App</h2>
                <button type="button" onClick={toggle}>
                {isOpen ? '<<<' : '>>>'}
                </button>
            </div>

            {isOpen && (
                <ul className="navbar-menu">
                <li><a href="#">Counter</a></li>
                <li><a href="#">About</a></li>
                <li><a href="#">Contact</a></li>
                </ul>
            )}
        </nav>
  )
}
```
