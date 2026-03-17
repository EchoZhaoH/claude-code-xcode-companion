---
name: xcode-companion
description: Xcode project build, get compilation errors, auto-fix
allowed-tools: Bash, Glob, Grep, Read, Edit
---

## When to use

Use when user wants to:
- Build Xcode project and get errors
- Check compilation errors
- Fix errors automatically

## Commands

### /build
Build Xcode project and get compilation errors.

**Steps:**
1. Find project: `ls *.xcworkspace *.xcodeproj`
2. List schemes: `xcodebuild -list -project <project>`
3. Build: `xcodebuild -project <project> -scheme <scheme> -destination 'platform=iOS Simulator' build -json`

### /errors
Get compilation errors.

**Steps:**
1. From xcresult: `xcrun xcresulttool format json --path <xcresult>`
2. Or from build: `xcodebuild ... build -json`

### /fix
Auto-fix compilation errors.

**Steps:**
1. Get errors first
2. Analyze and fix:

| Error | Fix |
|-------|-----|
| Cannot find 'X' | Add import/declaration |
| Missing return | Add return |
| Type mismatch | Fix type conversion |

3. Verify: rebuild

## Notes

- Always confirm before modifying code
- Use `-json` flag for structured output
