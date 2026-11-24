# React Books Project

A simple reading list app built with React. You can add books, rename them, and delete them. Data is stored in a local JSON file served by `json-server`, and all requests are made with Axios.

## Features

- View a list of books, each with a cover image
- Add a new book by title
- Edit a book's title inline
- Delete a book
- Shared state managed with React Context

## Tech Stack

- [React 19](https://react.dev/)
- [Vite](https://vitejs.dev/) for the dev server and build
- [Axios](https://axios-http.com/) for HTTP requests
- [json-server](https://github.com/typicode/json-server) as a fake REST API
- [Bulma](https://bulma.io/) for base styling
- ESLint for linting

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) 18 or newer
- npm

### Installation

```bash
git clone https://github.com/ejlucko/React-Books-Project.git
cd React-Books-Project
npm install
```

### Running the App

The app needs two processes running, so open two terminal windows.

**Terminal 1: start the API server (port 3001)**

```bash
npm run server
```

**Terminal 2: start the React app (port 3000)**

```bash
npm start
```

Then open [http://localhost:3000](http://localhost:3000) in your browser.

## Available Scripts

| Command | Description |
| --- | --- |
| `npm start` | Starts the Vite dev server on port 3000 |
| `npm run server` | Starts json-server on port 3001, watching `db.json` |
| `npm run build` | Creates a production build |
| `npm run preview` | Previews the production build locally |
| `npm run lint` | Runs ESLint |

## API Endpoints

json-server exposes these routes at `http://localhost:3001`. You can also test them with the requests in `api.http` (works with the VS Code REST Client extension).

| Method | Endpoint | Description |
| --- | --- | --- |
| GET | `/books` | Get all books |
| POST | `/books` | Add a book (`{ "title": "..." }`) |
| PUT | `/books/:id` | Update a book's title |
| DELETE | `/books/:id` | Delete a book |

## Project Structure

```
src/
├── components/
│   ├── BookCreate.js   # Form for adding a book
│   ├── BookEdit.js     # Form for editing a title
│   ├── BookList.js     # Renders all books
│   └── BookShow.js     # A single book with edit and delete buttons
├── context/
│   └── books.js        # Context provider with all Axios calls and book state
├── hooks/
│   └── use-books-context.js  # Custom hook for reading the books context
├── App.js
├── index.js
└── index.css
db.json                 # Data file used by json-server
```

## How It Works

`context/books.js` holds the list of books in state and exposes `fetchBooks`, `createBook`, `editBookById`, and `deleteBookById`. Each function sends the request with Axios and then updates local state. Components read this shared state through the `useBooksContext` hook, so no props need to be passed down through the tree.

## Notes

- Changes you make in the app are saved to `db.json` by json-server.
- If the book list is empty or nothing loads, make sure `npm run server` is running.
