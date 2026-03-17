# Xcode Companion

> The missing IDE context layer for Claude Code on Xcode

Xcode project smart assistant - build, get errors, auto-fix, and provide Xcode context to Claude.

## Install

### Option 1: Claude Code Plugin (Recommended)

Submit to Claude Code marketplace or install locally:

```bash
# Local installation
ln -s /path/to/xcode-companion ~/.claude/skills/xcode-companion
```

### Option 2: Copy to Project

```bash
cp -r xcode-companion .claude/skills/
```

## Features

- **Build** - Compile Xcode projects with xcodebuild
- **Errors** - Parse and display compilation errors
- **Fix** - Auto-fix common Swift compilation errors
- **Clean** - Clean build folder
- **Simulators** - List available iOS simulators

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

## Architecture

```
Claude Code → Xcode Companion Skill → xcodebuild
```

## License

MIT
