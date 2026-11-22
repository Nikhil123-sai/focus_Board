# FocusBoard

A responsive single-user task management and focus dashboard built with React, TypeScript, Vite, and Tailwind CSS.

## Features

- **Derived Overview Statistics**: Live calculation of total tasks, in-progress tasks, completed tasks, and completion rate percentage from the active task state.
- **Full Task CRUD**: Create tasks with required-title validation, edit existing tasks in a dedicated modal form, update task statuses (`To do`, `In progress`, `Completed`) inline, and delete tasks with an explicit confirmation dialog.
- **Combined Search & Filtering**: Case-insensitive title search, status tabs (`All`, `To do`, `In progress`, `Completed`) with live counts, and priority dropdown (`All`, `High`, `Medium`, `Low`) working together.
- **Focus Notes Carousel**: Three interactive Focus Notes slides with Previous/Next navigation, clickable slide indicators, keyboard arrow support, and quick filter actions.
- **Browser Persistence**: Safely reads and writes task state to `localStorage` (`focusboard_tasks_v1`), preserving user updates (including empty task lists) across page reloads without overwriting saved state with sample data.
- **Responsive Design**: Adaptive layout across desktop (`1440px`), tablet (`768px`), and mobile (`390px`) viewports with a collapsible mobile navigation drawer and touch-friendly task cards.
- **Accessibility**: Semantic landmarks (`<aside>`, `<header>`, `<main>`, `<nav>`), dialog ARIA roles with Escape-to-close, explicit accessible labels, `focus-visible` outlines, and `prefers-reduced-motion` support.

## State Management Choice

FocusBoard uses **React Context + `useReducer`** paired with pure, unit-tested state transformation helpers in `src/utils/taskLogic.ts`.

Why this approach:
- **Single source of truth**: All components (sidebar view counts, overview statistics, toolbar tab counters, and task list rows/cards) subscribe to one centralized reducer state.
- **Predictable immutable mutations**: Actions (`ADD_TASK`, `UPDATE_TASK`, `UPDATE_STATUS`, `DELETE_TASK`, `SET_FILTERS`, `RESET_DEMO_DATA`) return fresh arrays and objects without mutating existing state.
- **Automatic derived values**: Statistics and filtered results are memoized (`useMemo`) directly from `state.tasks` and `state.filters` rather than stored separately.
- **Zero extra runtime dependency overhead**: Ideal for a focused single-user frontend application without server-cache synchronization needs.

## Getting Started

```bash
npm install
npm run dev
```

### Run Unit Tests

```bash
npx --yes tsx --test src/utils/taskLogic.test.ts
```

### Production Build

```bash
npm run build
```

## Known Limitations

- Single-user client-side persistence via browser `localStorage` (no backend sync or multi-device cloud storage).
- User profile display (`Alex Morgan`) and workspace breadcrumb are single-user workspace defaults rather than authenticated multi-user accounts.
