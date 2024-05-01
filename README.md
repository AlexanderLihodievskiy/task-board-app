# Vue-test-kanban

Kanban-style Task Board web application. The application should allow users to create, view, and organize tasks using the drag-and-drop feature.

## Features

- **Task Creation**: Users can add new task cards, specifying a title and description.
- **Task Editing and Deletion**: Each card can be edited or deleted.
- **Drag-and-Drop**: Users can drag cards between columns or within a single column to change their status or priority.
- **Local Data Storage**: The application state (task list, their statuses, and positions) is stored in localStorage, so data persists between sessions.
- **Adaptability**: The interface is displayed correctly on various devices.

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur).

## Customize configuration

See [Vite Configuration Reference](https://vitejs.dev/config/).

To get the project from GitHub, you need to clone the repository. You can do this by running the following command in your terminal:

```sh
git clone https://github.com/AlexanderLihodievskiy/vue-test-kanban.git
```

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```

### Lint with [ESLint](https://eslint.org/)

```sh
npm run lint
```

### Format with [Prettier]
```sh
npm run format
```