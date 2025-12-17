# Minishell (42) — A Minimal Bash-like Shell in C

Minishell is a simplified Unix shell written in **C** as part of the **42 curriculum**. It provides an interactive prompt, parses user input, executes commands (including pipelines), and implements core shell behaviors such as redirections, environment variable expansion, and signal handling.

---

## Features

### Execution
- Runs executables via:
  - Absolute paths (e.g., `/bin/ls`)
  - Relative paths (e.g., `./program`)
  - `$PATH` lookup (e.g., `ls`)
- Command arguments and exit status propagation

### Pipes & Redirections
- Pipes: `cmd1 | cmd2 | cmd3`
- Redirections:
  - Input: `< file`
  - Output: `> file`
  - Append: `>> file`

### Environment & Expansion
- Environment variable expansion (e.g., `$HOME`, `$USER`)
- Exit code expansion: `$?`

### Builtins (typical for Minishell)
- `echo` (including `-n`)
- `cd`
- `pwd`
- `export`
- `unset`
- `env`
- `exit`

### Signals
- Interactive signal behavior aligned with a real shell:
  - `Ctrl-C` (SIGINT)
  - `Ctrl-\` (SIGQUIT)
  - `Ctrl-D` (EOF)

> Exact behavior may vary slightly depending on implementation details.

---

## Project Structure

The repository is organized into modules for maintainability:

- `parse/` — tokenization/parsing and syntax handling
- `execute/` — process creation, pipes, redirections, command execution 
- `builtin/` — builtin command implementations
- `utils/` — helper utilities 
- `free/` — memory cleanup helpers
- `signals.c` — signal handling logic
- `minishell.c` / `init.c` — entry point and initialization 

---

## Requirements

- `cc` (or `clang`)
- `make`
- Unix-like OS (Linux/macOS)
- `readline` library (commonly required for history and line editing)

If `readline` is missing on Linux (Debian/Ubuntu):
```bash
sudo apt-get update && sudo apt-get install -y libreadline-dev

On macOS (Homebrew):

brew install readline

Build

From the repository root:

make


Common targets (if available in the Makefile):

make clean
make fclean
make re

Run
./minishell


You should see a prompt. Try:

echo hello
pwd
export TEST=42
echo $TEST
ls -la | grep minishell
cat < input.txt | wc -l > out.txt
echo $?


Exit with:

exit


or press Ctrl-D.

What You Learn From This Project

Process management: fork, execve, waitpid

File descriptor control: dup2, pipes, redirections

Parsing and tokenizing user input reliably

Environment handling and state management

Signal behavior in interactive programs

Writing robust C code with careful memory management

Limitations / Notes

Minishell projects typically focus on the mandatory shell subset; advanced bash features are usually not part of the baseline requirements (e.g., &&, ||, subshells, wildcard/globbing) unless explicitly implemented.

Credits

Developed as a 42 curriculum project.

Author: Ilknur Hançer
Repo: https://github.com/ilknurhnc/minishell
