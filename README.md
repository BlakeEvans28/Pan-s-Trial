# Project 2

## Pan's Trial

Pan's Trial is a two-player digital strategy game built for ECE 348. Two challengers enter a shifting labyrinth and compete to become Pan's next champion. Players draft their starting cards, traverse a 6x6 toroidal labyrinth, collect useful cards, fight when they land on the same tile, and use the Appeasing Pan phase to reshape the board or change damage totals.

## Submission Contents

- `Pans_Trial.exe` - single-file Windows executable for playing the game.
- `main.py` - Python entry point for running from source.
- `engine/` - core game rules and state management.
- `ui/` - Pygame interface, rendering, and input handling.
- `tests/` - pytest rule tests.
- `balance_testing.py` - headless simulation harness used for balance testing.
- `Balancing_Testing_01.xlsx` - 100-game balance testing spreadsheet.
- `latex_apr_5.txt` - LaTeX mini balance report draft.

## How to Play the Executable

1. Download or clone the repository.
2. Open the `Pans_Trial` folder.
3. Double-click `Pans_Trial.exe`.
4. Use the on-screen controls to start the draft and play the game.

If Windows shows a security warning, choose the option to run the app anyway. This can happen for student-built executables that are not code-signed.

## Controls

- `Arrow Keys` or `WASD`: move through the labyrinth.
- `Mouse`: click cards, requests, Ballista targets, Plane Shift rows/columns, Restructure colors, and Appeasing Pan placement holes.
- `Pick Up`: spend a movement turn to collect the card under the current player, except walls.

## Rules Summary

The game starts with an initial draft. Players alternate choosing high-rank cards, and the remaining player cards are used as the player identities. The Omens then assign the four color families to the current labyrinth roles: Walls, Traps, Ballista, and Weapons.

During Traversing the Labyrinth, players alternate movement turns. The board wraps toroidally, so leaving one edge enters from the opposite edge. Walls block movement. Traps become damage for the player who triggers them. Ballista tiles let the player choose a reachable tile in a straight line until a wall blocks the path. Weapon-color cards are kept in the normal hand and may be used only during head-to-head combat.

During Appeasing Pan, both players play one normal hand card if possible. The reversed Omen color order determines trump strength, and same-color cards are decided by card rank. The winner chooses a request first, then the loser chooses unless Ignore Us ends the phase. Requests include Restructure, Steal Life, Ignore Us, and Plane Shift. At the end of the phase, the loser places the two played cards into labyrinth holes when possible; if there are not enough holes, the remaining played cards return to the loser's hand.

The game ends immediately when a player reaches 25 or more damage. The other player becomes Pan's champion.

## Run From Source

This project was developed with Python 3.13 on Windows.

```powershell
python -m venv .venv
.\.venv\Scripts\activate
python -m pip install pygame-ce pygame_gui pandas pytest
python main.py
```

## Run Tests

```powershell
.\.venv\Scripts\python.exe -m pytest tests\test_rules.py -q
```

## Build the Executable

The submitted executable was built with PyInstaller and the included slim spec file. The spec removes unused large pygame_gui CJK font bundles so the single executable stays below the 25 MB upload limit.

```powershell
.\.venv\Scripts\python.exe -m pip install pyinstaller
.\.venv\Scripts\python.exe -m PyInstaller --noconfirm --clean --distpath . --workpath build\pyinstaller_slim Pans_Trial_slim.spec
```

## Notes for GitHub

Do not commit the virtual environment, cache folders, or PyInstaller build folder. The executable is included because the assignment asks for a single playable file.
