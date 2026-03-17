# xcode-companion

Xcode project smart assistant - build, get errors, auto-fix for Claude Code.

## Install

```bash
ln -s /path/to/xcode-companion ~/.claude/skills/xcode-companion
```

Or copy to project:

```bash
cp -r xcode-companion .claude/skills/
```

## Usage

Just tell Claude:
- `/build` - Build Xcode project
- `/errors` - Get compilation errors
- `/fix` - Auto-fix errors
- `/clean` - Clean build folder
- `/simulators` - List available simulators

Or describe naturally:
- "Build my iOS project"
- "What compilation errors do we have?"
- "Fix the build errors"
- "Clean the build"

## Commands

| Command | Description |
|---------|-------------|
| `/build [scheme] [destination]` | Build Xcode project |
| `/errors [xcresult]` | Get compilation errors |
| `/fix [file]` | Auto-fix errors |
| `/clean` | Clean build folder |
| `/simulators` | List available simulators |

## Tools

- **Bash**: Execute xcodebuild commands
- **Read**: Read source files
- **Edit**: Modify code
- **Grep**: Search code
- **Write**: Create new files
