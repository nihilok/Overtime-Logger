# Overtime Logger

A simple Python script to log overtime hours to a SQLite database.

## Installation

To make the script available globally, add it to your PATH:

```bash
# Option 1: Create a symlink in a directory that's already in your PATH
sudo ln -s "$HOME/Code/overtime-logger/overtime-log" /usr/local/bin/overtime-log

# Option 2: Add this directory to your PATH (add to ~/.zshrc or ~/.bashrc)
export PATH="$PATH:"$HOME/Code/overtime-logger"
```

_Adjust paths according to where the repo was cloned to_

## Usage

Log hours for today:
```bash
overtime-log 3.5
```

Log hours for a specific date:
```bash
overtime-log 2.5 --date 2025-11-14
```

## Features

- **Automatic database creation**: Database is stored in `~/.local/share/overtime-logger/overtime.db`
- **Conflict handling**: If hours already exist for a date, you can:
  - **Overwrite**: Replace the existing value
  - **Add**: Add to the existing value
  - **Cancel**: Keep the existing value unchanged
- **Date flexibility**: Defaults to today, but you can specify any date in YYYY-MM-DD format

## Database Location

The SQLite database is stored at:
```
~/.local/share/overtime-logger/overtime.db
```

## Examples

```bash
# Log 3.5 hours for today
$ overtime-log 3.5
✓ Logged 3.5 hours for 2025-11-15

# Try to log more hours for the same day
$ overtime-log 2.0
Hours already logged for 2025-11-15: 3.5
You want to log: 2.0 hours

Options:
  [o] Overwrite - Replace existing hours with new value
  [a] Add - Add new hours to existing value
  [c] Cancel - Do nothing

Your choice (o/a/c): a
✓ Updated 2025-11-15: 5.5 hours (added 2.0)
```

## Querying the Database

You can query the database directly using sqlite3:

```bash
sqlite3 ~/.local/share/overtime-logger/overtime.db "SELECT * FROM overtime_log ORDER BY date DESC LIMIT 10;"
```
