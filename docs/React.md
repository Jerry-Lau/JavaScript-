# React Design Principles


### Meet React
- A library for creating user interfaces.
- Renders your UI and responds to events.
- AKA: the V in MVC.

### Rethinking best practices
- Prerequisite
  Combine DOM generation and display logic.
- React's design
  Re-render the whole app on every update.
- React's implementation
  Virtual DOM and synthetic events.

### 1.Building components, not templates

- React Component = A highly cohesive building block for UIs loosely coupled with other components.

- React components are reusable, composable and unit testable.

- Framework cannot know how to separate your concerns for you, it should only provide powerful and expressive tools for you to do it correctly. The tool is React component.

### 2.Re-render the whole app on every update (the key design decision that makes React awesome)

- With React, when data changes, React re-renders the entire component. That is, React components are idempotent funcitons. They describe your UI at any point in time, just like a server-rendered app.

- Re-rendering on every change makes things simple. Every place data is displayed is guaranteed to be up-to-date.

- No magical data binding.

- No model dirty checking.

- No more explicit DOM operations - everything is declarative.

- Re-rendering on every change? that seems expensive.

### 3.Virtual DOM
#### Makes re-rendering on every change fast.

- You can't just throw out the DOM and rebuild it on each update. It's too slow and you'll lose form state and scroll position.

- On every update, React builds a new virtual DOM subtree, diffs it with the old one, computes the minimal set of DOM mutations and puts them in a queue, and batch executes all updates.

- It's fast, because the DOM is slow.

- Batched reads and writes for optimal DOM performance.

- Automatic top-level event delegation (with cross-browser HTML5 events).

### Key takeaways

- Components, not templates

- Re-render, don't mutate

- Virtual DOM is simple and fast.
