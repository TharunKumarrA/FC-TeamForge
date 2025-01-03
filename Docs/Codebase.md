# Codebase Documentation for FC-TeamForge

## Overview
FC-TeamForge is a web application designed to simplify football team creation by automating team balancing and providing tools to manage players and substitutes. This documentation provides an in-depth look at the codebase structure, functionality, and the interaction between the frontend, backend, and database.

---

## Architecture
The project is divided into two main parts:

1. **Frontend** (Vue.js with Vite):
   - Manages the user interface and handles client-side operations.

2. **Backend** (Node.js with Express.js):
   - Provides APIs for managing player data and team generation.
   - Connects to a MySQL database for data storage.

---

## Folder Structure
```
TharunKumarrA-FC-TeamForge/
├── frontend/
│   ├── index.html
│   ├── public/
│   │   ├── images/
│   │   ├── constants.js
│   ├── src/
│   │   ├── components/
│   │   │   └── NewPlayer.vue
│   │   ├── static/
│   │   ├── App.css
│   │   └── NewPlayer.css
│   └── main.js
├── Docs/
│   └── Design.md
│   └── Codebase.md (this file)
└── backend/
    ├── server.js
    ├── Algorithm.js
    ├── sqlconnect.js
    ├── nodemon.json
    ├── package.json
    └── README.md
```
## Frontend Documentation

### Folder Breakdown
- `index.html`:
  Serves as the entry point for the web application. It links the Vue.js app and includes the necessary meta tags, scripts, and styles for rendering the frontend.
- `public/`
    - Contains static assets such as images and constants for the application.
- `src/`
  - `components/`: Vue components, such as NewPlayer.vue, responsible for individual parts of the UI.
      - `NewPlayer.vue`: Handles the form for adding a new player.
  - `static/`: Stores CSS stylesheets for the components.
  - `App.vue`: : Root component of the app containing global layouts and logic.
  - `main.js`: Entry point for the Vue.js application, initializes the app and renders the main component.

### Key Features
- Dynamic Forms: Allows users to add player details dynamically.
- Team Generation UI: Provides an interface for selecting players and generating balanced teams.

### Third-Party Dependencies

**axios**: For making HTTP requests to the backend.

**fontawesome**: Used for adding icons to enhance the UI.

---

## Backend Documentation
### Folder Breakdown

- `server.js`:
    - The main entry point for the backend server.
    - Defines API endpoints for the frontend to interact with.

- `Algorithm.js`:
    - Contains logic for generating balanced teams based on player roles and formations.

- `sqlconnect.js`:
    - Manages the connection to the MySQL database and performs database operations (e.g., adding players, fetching player data).

- `nodemon.json`:
    - Configuration for Nodemon to restart the server automatically during development.

- `package.json`:
    - Contains metadata and dependencies for the backend.

### API Endpoints

1. `POST /api/addPlayer`:
    - Adds a new player to the database.
    - Expects player details (name, role, etc.) in the request body.

2. `GET /api/players`:
    - Fetches the list of players from the database.

3. `POST /api/teams`:
    - Generates balanced teams based on the selected players and formation.

### Database Operations

- The backend uses sqlconnect.js to interact with the MySQL database. Key operations include:
    - Adding player records.
    - Retrieving players for team generation.

-----

## Interaction Flow

### Frontend-Backend Communication
1. Adding a Player:
  - The frontend sends a `POST` request to `/api/addPlayer` with player details.
  - he backend saves the player to the database and responds with a success status.

2. Fetching Players:
  - The frontend sends a `GET` request to `/api/players` to retrieve the list of available players.
  - The backend queries the database and returns the data in JSON format.

3. Team Generation:
  - The frontend sends a `POST` request to `/api/teams` with selected players and formation.
  - The backend processes the request using `Algorithm.js` and responds with balanced teams.



## Setup Instructions

### Prerequisites
- Node.js (v16 or later)
- npm
- MySQL (for the player database)

### Frontend Setup

1. Clone the repository:
```bash
git clone https://github.com/TharunKumarrA/FC-TeamForge.git
cd FC-TeamForge/frontend
```

2. Install dependencies:
```bash
npm install
```

3. Start the development server:
```bash
npm run dev
```

### Backend Setup

Clone the backend repository:

```bash
git clone https://github.com/Thanus-Kumaar/FC-TeamForge-server.git
cd FC-TeamForge-server
```

2. Install dependencies:

```bash
npm install
```

3. Start the server:

```bash
node server.js
```
4. Ensure the backend server is running before starting the frontend.

## Future Updates
<to be added>
