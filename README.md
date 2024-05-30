## Vue 3 TSC ToDo App with Vite

This is a simple Todo application built with Vue 3 and TypeScript. It allows users to create, edit, delete, and filter todo items. The application supports light and dark themes and stores data in the browser's local storage. This project was adapted from a tutorial by [Tyler Potts](https://youtu.be/qhjxAP1hFuI) huge thanks to that video for showing me the ropes.

## Features

- Create new todo items
- Edit existing todo items
- Delete todo items
- Mark todo items as done or not done
- Filter todo items based on their completion status
- Sort todo items by creation date in ascending or descending order
- Toggle between light and dark themes
- Persistent data storage using local storage

## Project Structure

```
vue-todo/
├── public/
├── src/
│   ├── assets/
│   ├── components/
│   ├── App.vue
│   ├── main.ts
├── index.html
├── package.json
├── tsconfig.json
├── vite.config.ts
```

- `public/`: Static assets
- `src/assets/`: Project-specific assets such as images, fonts, etc.
- `src/components/`: Vue components
- `src/App.vue`: Main application component
- `src/main.ts`: Entry point for the application
- `index.html`: Main HTML file
- `package.json`: Project metadata and dependencies
- `tsconfig.json`: TypeScript configuration
- `vite.config.ts`: Vite configuration

## Installation and Setup

To run this application locally, follow these steps:

### Prerequisites

- [Node.js](https://nodejs.org/en/) (version 14 or higher)
- [npm](https://www.npmjs.com/) (version 6 or higher) or [yarn](https://yarnpkg.com/)

### Clone the Repository

```bash
git clone https://github.com/faithl3s5/vue3-todo-app.git
cd vue-todo
```

### Install Dependencies

Using npm:

```bash
npm install
```

Or using yarn:

```bash
yarn install
```

## Running the Application

### Development Server

To start the development server, run:

```bash
npm run dev
```

Or using yarn:

```bash
yarn dev
```

This will start the application on `http://localhost:5173` (default port).

### Build for Production

To build the application for production, run:

```bash
npm run build
```

Or using yarn:

```bash
yarn build
```

The built files will be output to the `dist` directory.

### Preview the Production Build

To preview the production build locally, run:

```bash
npm run preview
```

Or using yarn:

```bash
yarn preview
```

## Usage

### Adding a Todo

1. Enter the todo content in the input field under "CREATE TODO".
2. Click the "Add todo" button or press Enter.

### Editing a Todo

1. Click on the todo content you want to edit.
2. Modify the content and click outside the input box to save.

### Deleting a Todo

1. Click the "Delete" button next to the todo you want to remove.

### Marking a Todo as Done/Not Done

1. Check or uncheck the checkbox next to the todo content.

### Filtering Todos

1. Use the "Show Done Only" or "Show Not Done Only" checkboxes to filter todos based on their completion status.

### Sorting Todos

1. Click the "Sorted: ASC/DESC by time" text to toggle between ascending and descending order.

### Toggling Theme

1. Click the "Theme: LIGHT/DARK" text to toggle between light and dark themes.

## Contributing

1. Fork the repository.
2. Create a new branch (`git checkout -b feature/your-feature`).
3. Commit your changes (`git commit -am 'Add some feature'`).
4. Push to the branch (`git push origin feature/your-feature`).
5. Create a new Pull Request.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
