---
name: xcode-companion
description: Xcode project build assistant - build projects, get compilation errors, auto-fix, provide Xcode context. Use when user wants to build, compile, fix Xcode projects, or needs Xcode context.
disable-model-invocation: false
allowed-tools: Bash, Glob, Grep, Read, Edit, Write
---

# Xcode Companion

Build, analyze, and fix Xcode projects.

## Usage

### /build [scheme] [destination]
Build Xcode project and get compilation errors.

**Steps:**
1. Find project: `ls *.xcworkspace *.xcodeproj`
2. List schemes: `xcodebuild -list -project <project>` (if no scheme provided)
3. Build with JSON output for parsing:
   ```bash
   xcodebuild -project <project> -scheme <scheme> -destination 'platform=iOS Simulator,name=iPhone 16' build -json 2>&1 | tee build.json
   ```

**Parameters:**
- `scheme`: Target scheme (optional, will prompt if not found)
- `destination`: Build destination (default: 'platform=iOS Simulator,name=iPhone 16')

### /errors [xcresult-path]
Get compilation errors from build result.

**Steps:**
1. From xcresult: `xcrun xcresulttool format json --path <xcresult>`
2. Parse JSON output for error details

### /fix [file-or-directory]
Auto-fix compilation errors.

**Steps:**
1. Get errors first using `/errors`
2. Analyze each error type and apply fixes:

| Error Pattern | Fix |
|--------------|-----|
| Cannot find 'X' in scope | Add import or declare missing symbol |
| Missing return in function | Add return statement |
| Type mismatch | Fix type conversion |
| Variable used before being assigned | Initialize variable |
| No such module 'X' | Add missing framework/Swift package |
| Cannot convert value 'X' to type 'Y' | Fix type casting |
| Property 'X' not found on object | Check property name or type |
| Ambiguous use of 'X' | Specify explicit type |
| Declaration requires explicit initializer | Add default value |
| Value of type 'X' has no member 'Y' | Check correct API |

3. Verify by rebuilding: `/build`

### /clean
Clean Xcode build folder.

**Steps:**
1. Find project
2. Run: `xcodebuild -project <project> -scheme <scheme> clean`

### /simulators
List available iOS simulators.

**Steps:**
```bash
xcrun simctl list devices available | grep -E "iPhone|iPad"
```

## Common Error Fixes

### Import Issues
```swift
// Error: Cannot find 'SwiftUI' in scope
// Fix: Add import SwiftUI
```

### Type Mismatch
```swift
// Error: Cannot convert value of type 'String' to expected argument type 'Int'
// Fix: Convert types appropriately using Int(string) or String(describing:)
```

### Nil Handling
```swift
// Error: Value of optional type 'String?' must be unwrapped
// Fix: Use guard let, if let, or ?? operator
```

### Missing Return
```swift
// Error: Missing return in global function expected to return 'String'
// Fix: Add return statement
```

## Best Practices

1. Always confirm before modifying code
2. Use `-json` flag for structured error output
3. Build with `-destination 'generic/platform=iOS'` for device builds
4. Use `xcodebuild -showBuildSettings` to see all settings
5. Check `.xcodeproj/project.pbxproj` for project configuration

## Natural Language Commands

You can also respond to natural language requests:

| User Request | Action |
|--------------|--------|
| "Build my iOS project" | Run /build |
| "What errors do we have?" | Run /errors |
| "Fix the build errors" | Run /fix |
| "Clean the build" | Run /clean |
| "List available devices" | Run /simulators |
| "Why is this crashing?" | Run /build then /errors then analyze |
| "Make this a reusable component" | Read selection, refactor code |

## Use Cases

### Build and Fix Workflow
1. User: "Build my project"
2. Run `/build` → Get errors
3. Run `/fix` → Auto-fix common errors
4. Run `/build` again → Verify fix

### Error Analysis Workflow
1. User: "Why is this code failing?"
2. Run `/build` to get errors
3. Run `/errors` to parse error details
4. Analyze and explain the root cause

### Context-Aware Assistance
When user asks about Xcode-related tasks, proactively provide context:
- Current file path
- Selection (if any)
- Recent build errors
- Project structure
