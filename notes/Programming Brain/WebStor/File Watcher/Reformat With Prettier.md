# Reformat With Prettier

Formatting code consistently is a challenge, but modern developer tools make it possible to maintain consistency across your team’s codebase automatically.

## For HTML File

Go to `File > Settings > Tools > File Watchers` to set up the reformat with pretter.

- **File Type**: `HTML` file type.
- **Scope**: Leave as `Current Files`.
- **Program**: Add the path to the Prettier executable (`Prettier`).
- **Arguments**: Use `--write $FilePathRelativeToProjectRoot$` or `--write $ContentRoot$`.
- Uncheck Auto-save to edited files.

## For JavaScript File

Go to `File > Settings > Tools > File Watchers` for setup reformat with pretter.

- **File Type**: `JavaScript, TypeScript`, or other relevant file types.
- **Scope**: Leave as `Current Files`.
- **Program**: Add the path to the Prettier executable (`Prettier`).
- **Arguments**: Use `--write $FilePathRelativeToProjectRoot$` or `--write $ContentRoot$`.
- Uncheck Auto-save to edited files.