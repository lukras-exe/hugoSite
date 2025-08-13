---
title: "TimedMinesweeper-Java"
summary: "This is a modified version of Minesweeper with a timer, built in Java."
date: 2024-12-28T00:00:00Z
draft: false
---

## Overview
A fully interactive **Minesweeper game** built in Java using the Swing framework. The game features a customizable gride (default set to 8x8), a customizable coutdown timer (default set at 30 seconds), and a GUI.

## Features
- **Interactive Game Board**: 8x8 grid of tiles for a classic Minesweeper experience.
- **Randomized Mines**: Mines are placed randomly on the board at the start of each game.
- **Timer Functionality**: A 30-second countdown timer, adding urgency to the gameplay.
- **Tile actions**
    - **Left-click**: Reveals a tile
    - **Right-click**: flag/unflag a suspected mine
- **Win/Loss Conditions:**
    - **Win**: Reveals all tiles without mines
    - **Loss**: Click on a mine or run out of time
- **Dynamic Messaging**: Displays remaining time, mine count, and win/loss messages in real time.

View on github: [Github](https://github.com/lukras-exe/TimedMinesweeper-Java)