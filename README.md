# miniGrep — a tiny grep-like tool in Rust

A small command-line search utility written in Rust, inspired by the "minigrep" example from "The Rust Programming Language" book. It searches for a query string inside a file and prints matching lines.

## Features

- Search for a literal query in a file (case-sensitive by default).
- Optional case-insensitive search.
- Small, fast, and easy to build with Cargo.

## Quick example

This repository includes `src/poem.txt`. Example (zsh):

```zsh
# build in debug (or use --release for an optimized binary)
cargo build

# run the program: query then filename
cargo run -- "life" src/poem.txt

# case-insensitive search using environment variable
CASE_INSENSITIVE=1 cargo run -- "rust" src/poem.txt
```

You can also run the compiled binary directly:

```zsh
./target/debug/minigrep "query" src/poem.txt
```

## Usage

The program expects two positional arguments:

1. query — the string to search for
2. filename — the file to search

Examples:

```zsh
cargo run -- "duct" src/poem.txt
```

For case-insensitive search, set the `CASE_INSENSITIVE` environment variable to any value (e.g. `1`):

```zsh
CASE_INSENSITIVE=1 cargo run -- "rust" src/poem.txt
```

## How it works (short)

The core search logic lives in `src/lib.rs` and provides two functions:

- `search(query, contents)` — case-sensitive search returning matched lines.
- `search_case_insensitive(query, contents)` — case-insensitive search.

The CLI in `src/main.rs` parses arguments, reads the file contents, picks the search mode (based on the `CASE_INSENSITIVE` env var), and prints matched lines.

## Tests

Run the unit tests bundled with the library with:

```zsh
cargo test
```

There are tests for both case-sensitive and case-insensitive search functions.

## Contributing

Small project: feel free to open issues or pull requests. If you add features, include tests and update the README.

Checklist for PRs:

- [ ] Code compiles (run `cargo build`)
- [ ] Tests pass (`cargo test`)
- [ ] Add/modify tests for new behavior
