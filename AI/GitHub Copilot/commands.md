# GitHub Copilot Commands

This document outlines useful commands and shortcuts for interacting with GitHub Copilot in your editor.

## Inline Suggestions

These are the primary way you interact with Copilot. As you type, Copilot will provide suggestions that you can accept or ignore.

| Action                      | Windows/Linux         | macOS                 |
| --------------------------- | --------------------- | --------------------- |
| Accept Suggestion           | `Tab`                 | `Tab`                 |
| Dismiss Suggestion          | `Esc`                 | `Esc`                 |
| Show Next Suggestion        | `Alt + ]`             | `Option + ]`          |
| Show Previous Suggestion    | `Alt + [`             | `Option + [`          |
| Trigger Suggestion          | `Ctrl + Enter`        | `Cmd + Enter`         |

## Copilot Chat

Copilot Chat allows you to ask coding-related questions and get help directly in your IDE.

| Action                      | Description                                     |
| --------------------------- | ----------------------------------------------- |
| `/explain`                  | Explain how the selected code works.            |
| `/tests`                    | Generate unit tests for the selected code.      |
| `/fix`                      | Propose a fix for problems in the selected code.|
| `/help`                     | Get help on how to use Copilot Chat.            |

## Editor-Specific Commands

Your experience with GitHub Copilot can be enhanced by using commands specific to your code editor.

### Visual Studio Code

| Command ID                          | Description                                       |
| ----------------------------------- | ------------------------------------------------- |
| `github.copilot.generate`           | Trigger Copilot to generate code suggestions.     |
| `github.copilot.accept`             | Accept the current Copilot suggestion.            |
| `github.copilot.next`               | Cycle to the next suggestion.                     |
| `github.copilot.prev`               | Cycle to the previous suggestion.                 |
| `github.copilot.toggleCopilot`      | Enable or disable Copilot for the current editor. |

You can access these commands through the command palette (`Ctrl+Shift+P` or `Cmd+Shift+P`).
