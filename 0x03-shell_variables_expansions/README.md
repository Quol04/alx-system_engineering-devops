# Shell variables & expansions exercises

This repository contains short shell script exercises focused on shell variables, environment variables, PATH manipulation, simple arithmetic, and text generation. Each script lives under `0x03-shell_variables_expansions/` and is intentionally small and self-contained. The exercises are suitable for POSIX-compliant shells (sh, dash, bash). Examples and testing notes below assume a bash-compatible shell.

## Contents

- `0x03-shell_variables_expansions/`
  - `0-alias` — create an alias named `ls` that runs `rm *` (exercise in alias creation)
  - `1-hello_you` — print `hello <user>` where `<user>` is the current Linux username
  - `2-path` — add `/action` to the end of the `PATH` environment variable
  - `3-paths` — count the number of directories in the current `PATH`
  - `4-listenv` — list environment variables
  - `5-listall` — list local variables, environment variables, and functions
  - `6-create_local_variable` — create a new local (shell) variable
  - `7-create_global_variable` — create a new global (exported) environment variable
  - `8-true_knowledge` — print the result of `128 + $TRUEKNOWLEDGE`
  - `9-divide_and_rule` — print the result of `$POWER / $DIVIDE`
  - `10-love_exponent_breath` — compute `$BREATH ** $LOVE` (BREATH to the power LOVE)
  - `11-binary_to_decimal` — convert binary (stored in `$BINARY`) to base 10
  - `12-combinations` — print all two-letter combinations (aa..zz) except `oo`
  - `13-print_float` — print the value of `$NUM` with two decimal places

Note: filenames above are inferred from the original folder listing and README contents. If a different filename exists for a task, use the file that implements the described behavior.

## How to use

1. Open a POSIX shell (bash is recommended). On Windows, use WSL or Git Bash for correct behavior.
2. Make scripts executable if needed: `chmod +x 0x03-shell_variables_expansions/*`
3. Run a script directly, for example: `./0x03-shell_variables_expansions/1-hello_you`

Some scripts rely on environment variables. You can export them inline or before running. Examples below show usage and quick tests.

## Examples and quick tests

- 1-hello_you

  - Purpose: print `hello <user>` where `<user>` is your current username.
  - Test: `./0x03-shell_variables_expansions/1-hello_you`

- 2-path (add `/action` to PATH)

  - Purpose: append `/action` so it is the last lookup dir in `PATH`.
  - Test: `./0x03-shell_variables_expansions/2-path` then `echo $PATH` and verify `/action` is at the end.

- 3-paths (count PATH directories)

  - Purpose: print the number of colon-separated directories in `PATH`.
  - Test: `./0x03-shell_variables_expansions/3-paths`

- 4-listenv

  - Purpose: list environment variables (usually prints NAME=VALUE pairs).
  - Test: `./0x03-shell_variables_expansions/4-listenv`

- 5-listall

  - Purpose: list local variables, exported environment variables, and shell functions.
  - Test: `./0x03-shell_variables_expansions/5-listall`

- 6-create_local_variable

  - Purpose: demonstrate creating a shell-local variable (not exported).
  - Test: Run the script and then in the same shell try `echo $LOCAL_VAR` (if the script is executed in a subshell you won't see it — prefer `source` to observe the change):
    - `source 0x03-shell_variables_expansions/6-create_local_variable` then `echo $MY_LOCAL`

- 7-create_global_variable

  - Purpose: export a variable so subshells see it.
  - Test: `source 0x03-shell_variables_expansions/7-create_global_variable` then `echo $MY_GLOBAL`

- 8-true_knowledge

  - Purpose: print `128 + $TRUEKNOWLEDGE` followed by a newline.
  - Test: `TRUEKNOWLEDGE=10 ./0x03-shell_variables_expansions/8-true_knowledge` should print `138`.

- 9-divide_and_rule

  - Purpose: compute `POWER / DIVIDE` using environment variables and print the result followed by a newline.
  - Test: `POWER=10 DIVIDE=2 ./0x03-shell_variables_expansions/9-divide_and_rule` prints `5`.

- 10-love_exponent_breath

  - Purpose: compute `BREATH` to the power `LOVE` and print the result.
  - Test: `BREATH=2 LOVE=3 ./0x03-shell_variables_expansions/10-love_exponent_breath` prints `8`.

- 11-binary_to_decimal

  - Purpose: convert a binary string from `$BINARY` to base 10 and print it.
  - Test: `BINARY=1010 ./0x03-shell_variables_expansions/11-binary_to_decimal` prints `10`.

- 12-combinations

  - Purpose: print all two-letter lowercase combinations in alphabetical order, except `oo`.
  - Test: `./0x03-shell_variables_expansions/12-combinations | grep -xv oo | head -n 5` (first lines should be `aa`, `ab`, `ac`, ...).

- 13-print_float

  - Purpose: print the value of `$NUM` with exactly two decimal places.
  - Test: `NUM=3.14159 ./0x03-shell_variables_expansions/13-print_float` prints `3.14`.

## Implementation notes and portability

- These scripts are exercises; keep them short and aim for POSIX shell compatibility. When using bash-specific features (like arithmetic exponentiation `**`), ensure the environment uses bash.
- For scripts that should set variables in the current shell (local/global variable tasks), prefer `source` (dot) invocation: `source <script>`.
- Avoid destructive aliases (e.g., an alias that maps `ls` to `rm *`) in a shared environment. If you test `0-alias`, do so in an isolated shell session.

## Testing checklist

1. Make scripts executable: `chmod +x 0x03-shell_variables_expansions/*`
2. Run each script and compare output to examples above.
3. For environment-variable-based scripts, test by exporting variables inline as shown in the examples.
