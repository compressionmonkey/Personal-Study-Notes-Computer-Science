## Session 2: References, Heap, Object Identity

### Core model
- Primitives → stack (copied by value)
- Objects/Arrays → heap (variables hold references/pointers)
- Assignment of objects copies the reference, not the data

### Object identity
- `===` checks reference equality (same heap address)
- `{ x:1 } === { x:1 }` → false (different addresses)
- `a === b` after `b = a` → true (same address)

### Shallow copy
- `{ ...original }` / `Object.assign({}, original)`
  → new top-level object ✓
  → nested objects still shared ✗
- React reconciler: sees new reference → triggers re-render
- Safe only when mutations stay at the top level

### Closures
- Function + captured lexical environment (variable bindings at creation time)
- Closure keeps ALL captured variables alive (GC cannot collect them)
- Each React render = new scope = new variable bindings

### Stale closure
- Effect/callback captures var at creation; var updates later; closure sees old value
- Symptom: `setInterval` logging stale state
- Fix 1: add to dependency array (re-create closure on change)
- Fix 2: use `useRef` to read current value without re-creating effect

### Memory leaks in React
- Root cause: live reference chain prevents GC
  window/global → timer/listener → closure → component scope
- Common causes: setInterval, addEventListener, fetch without AbortController
-  Fix: always return cleanup fn from useEffect
  `return () => clearInterval(id)`
- Detection: Chrome DevTools → Memory → Heap Snapshot (look for detached nodes, retained closures)

