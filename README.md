# Asteroid Game

Hello, I recently created this arcade stule asteroids game in python using pygame. The following project was made with the help of lessons on boot.dev where I have been learning backend programming. Below are the instructions on how to run and test the project on your own machine. Enjoy and expect me to add my own customization to this game at some point.

## Requirements

- **Python 3.13 or newer**
- **[uv](https://docs.astral.sh/uv/)**, the Python package and project manager this project uses. It installs pygame for you and can also install the right Python version.
- **Git**, to download the project

## Setup

### 1. Install uv

macOS / Linux:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Windows (PowerShell):

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

After installing, open a new terminal and check that it worked:

```bash
uv --version
```

### 2. Download the project

```bash
git clone https://github.com/luxNiru/asteroid-game.git
cd asteroid-game
```

### 3. Run the game

```bash
uv run main.py
```

The first time you run this, uv creates a virtual environment, downloads Python 3.13 if you don't already have it, and installs pygame 2.6.1 (the version pinned in `uv.lock`). After that the game opens in a 1280×720 window.

## Controls

| Key     | Action         |
| ------- | -------------- |
| `W`     | Move forward   |
| `S`     | Move backward  |
| `A`     | Rotate left    |
| `D`     | Rotate right   |
| `Space` | Shoot          |

The game ends when an asteroid hits your ship. Close the window to quit at any time.

## Running without uv

If you'd rather use plain `pip`:

```bash
python3 -m venv .venv
source .venv/bin/activate      # Windows: .venv\Scripts\activate
pip install pygame==2.6.1
python main.py
```

Make sure `python3 --version` reports 3.13 or newer first.

## Log files

Every run writes two files to the project folder:

- `game_state.jsonl`: a snapshot of the game state about once per second, for the first 16 seconds
- `game_events.jsonl`: events such as `asteroid_shot` and `player_hit`

They are overwritten on each run, and you can delete them safely.

## Project structure

| File               | Purpose                                                   |
| ------------------ | --------------------------------------------------------- |
| `main.py`          | Entry point: sets up pygame and runs the game loop        |
| `player.py`        | The player's ship: movement, rotation and shooting        |
| `asteroid.py`      | Asteroids and how they split when shot                    |
| `asteroidfield.py` | Spawns new asteroids from the edges of the screen         |
| `shot.py`          | Bullets fired by the player                               |
| `circleshape.py`   | Base class for every object, including collision checks   |
| `constants.py`     | Settings such as screen size, speeds and spawn rate       |
| `logger.py`        | Writes the `.jsonl` log files                             |

To change how the game feels (ship speed, fire rate, asteroid spawn rate and so on), edit the values in `constants.py`.

## Troubleshooting

- **`uv: command not found`**: open a new terminal after installing uv, or follow the PATH instructions the installer printed.
- **`ModuleNotFoundError: No module named 'pygame'`**: you ran `python main.py` directly without installing dependencies. Use `uv run main.py`, or follow the pip steps above.
- **No window appears**: pygame needs a graphical desktop, so it won't open a window over SSH or in a headless environment.
