## DevSecOps Pipeline Implementation for Tic Tac Toe Game

# Tic Tac Toe Game

## Overview

This is a classic Tic Tac Toe game implemented using React.  It provides a clean and intuitive user interface to play the game, track scores, and view game history.

## Features

* **Interactive Game Board:** A 3x3 grid where players can make their moves.
* **Two-Player Gameplay:** Supports two players (X and O) taking turns.
* **Score Tracking:** Keeps track of wins for each player (X and O) and the number of draws.
* **Game History:** Records and displays the history of completed games, showing the final board state and the winner (or draw) of each game.
* **Game Status:** Displays the current game status, indicating whose turn it is or the outcome of the game (win or draw).
* **Reset Functionality:**
    * "New Game" button to reset the current game.
    * "Reset All" button to reset the scores, game history, and the current game.
* **Winning Line Highlight:** Highlights the winning line on the board when a player wins.

## Tech Stack

* **React:** The game is built using React, a popular JavaScript library for building user interfaces.
* **JavaScript:** The game logic and component interactivity are implemented using JavaScript.
* **HTML:** The structure of the application.
* **CSS:** Styling for the application.
* **Lucide React: Icons** The application uses icons from the Lucide React library.

## Project Structure

├── public/│   └── index.html        # Main HTML file├── src/│   ├── components/│   │   ├── Board.tsx       # Game board component│   │   ├── GameHistory.tsx # Game history display component│   │   ├── ScoreBoard.tsx  # Scoreboard component│   │   └── Square.tsx # Represents one square of the board│   ├── utils/│   │   └── gameLogic.ts  # Functions for calculating the winner and checking for a draw│   ├── App.tsx           # Main application component│   ├── index.css         # Global styles│   └── index.js          # Entry point of the React application├── package.json          # Project dependencies and scripts└── README.md             # Project documentation (this file)
## Logic of the Game

The game logic is implemented in `src/utils/gameLogic.ts` and within the main `App.tsx` component. Here's a breakdown:

1. X goes first, followed by O
2. The first player to get 3 of their marks in a row (horizontally, vertically, or diagonally) wins
3. If all 9 squares are filled and no player has 3 marks in a row, the game is a draw
4. Winning combinations are highlighted
5. Game statistics are tracked and displayed

## Instructions for Building and Deployment

### Prerequisites

* **Node.js:** Ensure you have Node.js installed (version 14 or later).
* **npm or Yarn:** You'll need npm (Node Package Manager) or Yarn to manage project dependencies.
* **Git:** Recommended for version control.

### Installation

1.  **Clone the repository:**
    ```bash
    git clone <repository_url>
    cd <repository_name>
    ```

2.  **Install dependencies:**
    Using npm:
    ```bash
    npm install
    ```
    Or, using Yarn:
    ```bash
    yarn install
    ```

### Building for Production

1.  **Build the project:**
    Using npm:
    ```bash
    npm run build
    ```
    Or, using Yarn:
    ```bash
    yarn build
    ```
    This will create an optimized production build of the application in the `build` directory.

### Deployment

The deployment process will depend on your chosen hosting platform. Here are some common options:

#### 1.  **Netlify/Vercel:**

* These platforms offer easy deployment for React applications.
* Simply connect your repository to the platform and it will automatically build and deploy your application.
* The `build` directory should be specified as the output directory.

#### 2.  **GitHub Pages:**

* You can deploy your app to GitHub Pages.
    * Add the following to your `package.json`
        ```json
        "homepage": "http://{your_github_username}.github.io/{your_repo_name}"
        ```
    * Run these commands:
        ```bash
        npm run build
        npm run deploy
        ```
    * You might need to install `gh-pages`:
        ```bash
        npm install gh-pages -D
        ```
    * Add the deploy script in `package.json`:
        ```json
        "scripts": {
        "predeploy": "npm run build",
        "deploy": "gh-pages -d build"
        }
        ```

#### 3.  **Other Hosting Providers:**

* For other hosting providers (e.g., AWS, Heroku, etc.), follow their specific deployment instructions for React applications.  You'll typically need to:
    * Create a production build.
    * Configure a server to serve the static files from the `build` directory.

### Running in Development Mode

For local development:

1.  **Start the development server:**
    Using npm:
    ```bash
    npm start
    ```
    Or, using Yarn:
    ```bash
    yarn start
    ```

    This will start a development server, and you can view the application in your browser (usually at `http://localhost:3000`).


