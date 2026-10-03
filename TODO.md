# TODO

## 🟠 High value — Physical keyboard support

**Status:** Planned, not started

Wordle-style games should be playable from the keyboard. Today the game is mouse-only — `Keyboard.tsx` renders `<button>` elements, and there is no `keydown` listener anywhere in `src/`.

### Plan

Add a `keydown` listener on `document` in `src/App.tsx` (not `Keyboard.tsx` — that component is presentational; `App.tsx` owns `addGuessedLetter` and `isGameOver`).

```ts
useEffect(() => {
  function handleKeyDown(e: KeyboardEvent) {
    if (e.repeat) return                          // ignore key hold
    if (e.ctrlKey || e.metaKey || e.altKey) return // don't steal browser shortcuts
    if (!/^[a-z]$/.test(e.key)) return             // letters only
    if (isGameOver) return                         // no guessing after win/lose
    addGuessedLetter(e.key.toLowerCase())
  }
  document.addEventListener("keydown", handleKeyDown)
  return () => document.removeEventListener("keydown", handleKeyDown)
}, [isGameOver, addGuessedLetter])
```

- Duplicate guesses are already a no-op — `addGuessedLetter` guards with `prevLetters.includes(letter)` in `App.tsx`.
- Dependency array is required: the handler closes over `isGameOver`, so it must re-bind when the round ends.
- Files touched: **`src/App.tsx` only** (~15 lines). No new deps, no changes to `Keyboard.tsx`.

### Optional add-on

Press `Enter` / `Space` to start a new game when `isGameOver` is true, so the whole loop stays on the keyboard.

### Verify

1. Type letters → board + keyboard colors match clicking
2. Hold a key → only one guess registers
3. Play to win → further keys ignored, confetti fires
4. Play to lose → missed letters reveal
5. (If add-on) Enter after a round → new word, guesses cleared
6. `npm run lint` and `npm run build` pass

---

## Other remaining polish

- [ ] Strip redundant type annotations (exercise-style `: string` on inferred values); drop verbose `JSX.Element` return types
- [ ] Add an MIT `LICENSE` file and remove the placeholder license note from `README.md`
- [ ] Add a demo GIF / screenshot to `README.md`
- [ ] Add unit tests for `utils.ts` and the win/loss logic in `App.tsx`
- [ ] Deploy a live demo (Vercel / Netlify / GitHub Pages)

## Done

- [x] Rewrite `README.md` (replaced default Vite template boilerplate)
- [x] Remove all `CHALLENGE` comments and the dead `React.FC` block
