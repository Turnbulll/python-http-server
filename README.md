# simple-python-http-server

A lightweight static file server written in Python. Serves files and directories from the current working directory over HTTP with no external dependencies.

## Features

- Serves static files directly from disk
- Automatically serves `index.html` when a directory is requested
- Falls back to a directory listing if no `index.html` is present
- Returns a clean HTML error page for missing files or unexpected errors
- Zero dependencies — uses Python's built-in `http.server` module

## Usage

```bash
python server.py
```

The server starts on port `8080`. Navigate to `http://localhost:8080` in your browser.

Files are served relative to the directory you run the script from.

## How It Works

Incoming GET requests are matched against a chain of cases in order:

| Case | Condition | Action |
|------|-----------|--------|
| `case_no_file` | Path does not exist | Returns 404 error page |
| `case_existing_file` | Path is a file | Serves the file |
| `case_directory_index_file` | Path is a directory with `index.html` | Serves `index.html` |
| `case_directory_no_index_file` | Path is a directory without `index.html` | Serves a directory listing |
| `case_always_fail` | Fallback | Returns an error page |

Each case has a `test()` method to check if it applies and an `act()` method to handle the request. The first matching case wins.

## Configuration

The port is set near the bottom of `server.py`:

```python
serverAddress = ("", 8080)
```

Change `8080` to any available port you prefer.

## Requirements

- Python 3.x
- No third-party packages needed

## Project Structure

```
py-server/
└── server.py
```

## License

MIT
