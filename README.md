# Assembly: Endgame

A Wordle-style word guessing game built with **React** and **TypeScript**. Guess the hidden word one letter at a time before your stack of programming languages is exhausted — and Assembly takes over the world.

## How to Play

- A random word is chosen from the word list.
- Guess letters using the on-screen keyboard.
- Correct letters are revealed on the word board.
- Every wrong guess eliminates the next language from your stack — HTML, CSS, JavaScript, React, TypeScript, Node.js, Python, and more — each shown as a brand-colored chip.
- Each wrong guess also triggers a randomized farewell message: *"Farewell, HTML"*, *"R.I.P., CSS"*, *"Node.js bites the dust"*…
- Fill in the word before the stack runs out to win. Lose, and Assembly wins.

## Features

- Wordle-style letter guessing with correct / incorrect feedback on the keyboard
- Language elimination stack with brand-colored chips
- Randomized farewell messages on each wrong guess
- Confetti celebration on a win
- Fully typed components and props (TypeScript)
- Accessible: ARIA live region announces guesses and remaining attempts to screen readers
- "New Game" button after each round
- Vite dev server with HMR, ESLint configured

## Tech Stack

| | |
|---|---|
| UI | React 19 |
| Language | TypeScript |
| Build tool | Vite 8 |
| Linting | ESLint 10 + typescript-eslint |
| Utilities | `clsx`, `react-confetti` |

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) and npm

### Installation

```bash
git clone https://github.com/gauripatil/assembly-game-react-typescript.git
cd assembly-game-react-typescript
npm install
```

### Development

```bash
npm run dev
```

Then open the local URL printed in the terminal (usually `http://localhost:5173`).

### Production build

```bash
npm run build      # type-check with tsc and bundle with vite
npm run preview    # serve the production build locally
```

### Lint

```bash
npm run lint
```

## Project Structure

```
src/
  App.tsx                 # Game state, win/loss logic, layout
  words.ts                # Word list used to pick the secret word
  languages.ts            # Language stack (name + brand colors)
  utils.ts                # getRandomWord, getFarewellText
  components/
    Header.tsx            # Title and game description
    GameStatus.tsx        # Win/lose banner and farewell messages
    LanguageChips.tsx     # Stack of languages, struck out on wrong guesses
    WordLetters.tsx       # Hidden / revealed letters of the secret word
    Keyboard.tsx          # On-screen alphabet keyboard
    AriaLiveStatus.tsx    # Screen-reader status announcements
    NewGameButton.tsx     # Reset button shown after a round ends
    ConfettiContainer.tsx # Confetti overlay on a win
```

## How the Game Logic Works

All game state lives in `App.tsx`:

- `guessedLetters` — every letter the player has picked so far
- `wrongGuessCount` — guessed letters that are **not** in the secret word
- You **win** when every letter of the word has been guessed
- You **lose** when `wrongGuessCount` reaches the number of allowed wrong guesses (`languages.length - 1`)

`utils.ts` picks a random word and generates the farewell messages; `languages.ts` holds the elimination stack and each language's brand colors.

## License

Add a license here before publishing publicly.
