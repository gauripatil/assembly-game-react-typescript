# Assembly: Endgame

A Wordle-style word guessing game in **React** + **TypeScript**. Guess the word before your stack of programming languages runs out — and Assembly takes over.

![React](https://img.shields.io/badge/React-19-61DAFB?logo=react&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-6.0-3178C6?logo=typescript&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-8.2-646CFF?logo=vite&logoColor=white)
![ESLint](https://img.shields.io/badge/ESLint-10.8-4B32C3?logo=eslint&logoColor=white)


**Live demo:** https://assembly-game-react-typescript.vercel.app/


<!--
  Demo GIF: record ~5s of gameplay (a win with confetti), save as public/demo.gif,
  then uncomment:
  ![Gameplay demo](public/demo.gif)
-->

---

## Tech Stack

| Layer | Choice |
|---|---|
| UI | React 19 |
| Language | TypeScript |
| Build tool | Vite 8 |
| Linting | ESLint 10 + typescript-eslint |
| Utilities | `clsx`, `react-confetti` |

## Keywords

`react` · `typescript` · `vite` · `wordle` · `word-game` · `game` · `react-hooks` · `word-guessing` · `education` · `scrimba` · `accessibility` · `aria-live` · `confetti`

## Quick Start

```bash
git clone https://github.com/gauripatil/assembly-game-react-typescript.git
cd assembly-game-react-typescript
npm install
npm run dev
```

Open the local URL (default `http://localhost:5173`).

## Features

- Wordle-style letter guessing with on-screen keyboard feedback
- Wrong guesses eliminate a stack of programming languages — each a brand-colored chip
- Randomized farewell messages (*"Farewell, HTML"*, *"Node.js bites the dust"*)
- Confetti on win
- Typed components and props throughout (TypeScript)
- ARIA live region announces guesses and remaining attempts

## Scripts

| Command | What it does |
|---|---|
| `npm run dev` | Start dev server with HMR |
| `npm run build` | Type-check (`tsc`) and bundle for production |
| `npm run preview` | Serve the production build locally |
| `npm run lint` | Run ESLint |

## What I Built

Base project: Scrimba's [Assembly: Endgame](https://scrimba.com/learn/learnreact) — a React course project by Bob Ziroll. This repo is the **TypeScript implementation**: I completed the course's typing challenges and carried that typing through the whole app.

- **Typed props on every component** — explicit props objects (`GameStatusProps`, `KeyboardProps`, `LanguageChipsProps`, `WordLettersProps`, `AriaLiveStatusProps`) instead of untyped params or `React.FC` signatures
- **Return type annotations** — every component and helper declares what it returns
- **Utility types** — `Omit<Language, 'name'>` in `LanguageChips`, so the inline style object can't drift from the `Language` contract
- **Typed helper layer** — `utils.ts` functions (`getRandomWord`, `getFarewellText`) annotated with parameter and return types
- **Repo hygiene** — production build (`tsc -b && vite build`), ESLint 10 + typescript-eslint config, and a project-specific README

### What I Learned

- Deriving game state from a single `guessedLetters` array instead of storing multiple boolean flags
- The difference between **state**, **derived state**, and **static values** in React
- Why typed props objects beat `React.FC` for component contracts
- Keeping pure logic (`utils.ts`) separate from rendering so it stays testable

## How It Works

Game state lives in `App.tsx`:

- **Win** — every letter of the word has been guessed
- **Lose** — wrong guesses reach `languages.length - 1`

`utils.ts` picks the random word and generates farewell messages; `languages.ts` holds the elimination stack and brand colors.

## Project Structure

```
src/
  App.tsx              # Game state, win/loss logic, layout
  words.ts             # Word list
  languages.ts         # Language stack + brand colors
  utils.ts             # getRandomWord, getFarewellText
  components/          # Header, GameStatus, LanguageChips,
                       # WordLetters, Keyboard, AriaLiveStatus,
                       # NewGameButton, ConfettiContainer
```

## Attribution

Base project: [Assembly: Endgame](https://scrimba.com/learn/learnreact) by Bob Ziroll, from [Scrimba](https://scrimba.com)'s React course. This repo is a TypeScript implementation of that course project — see [What I Built](#what-i-built) for what was added on top.

## License

Add a license before publishing publicly.
