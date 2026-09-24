# Notes

## Goal
A stopwatch web app, with the option to move to phones later.

## Stack
- **Vite + React + TypeScript**: fast setup and widely used.
- **Vitest** for unit tests.
- Keep the timing logic in a plain TypeScript module with no React or DOM code, so it can move to a phone app as-is.

## Path to phones
1. **PWA** (Progressive Web App: a website installable on a phone's home screen). Add a manifest and service worker so it installs and works offline. This needs very little extra work.
2. **React Native / Expo**, only if a native app is needed later. It can reuse the timing module.

## Timing approach
Don't count ticks. Store `startedAt` (from `performance.now()`) and `accumulated` (the total from earlier runs before pausing).
- elapsed = accumulated + (running ? now - startedAt : 0)
- The display updates on `requestAnimationFrame`, but the elapsed time always comes from timestamps, so it never drifts.

## v1 scope
- [ ] Start / pause / resume
- [ ] Reset
- [ ] Display `mm:ss.cc` (hours added when needed)
- [ ] Laps: record a split and list lap and total times

## Later
- Keyboard shortcuts (Space = start/pause, L = lap, R = reset)
- Save state in localStorage so a refresh doesn't lose the time
- PWA install and offline support
- Dark mode
- Countdown timer

## Build order
1. Scaffold the Vite + React + TS project, then make the first commit on `develop`
2. Timing module plus unit tests
3. Minimal UI: time display and start/pause/reset buttons
4. Laps
5. Styling and keyboard shortcuts
6. Saving state and PWA
