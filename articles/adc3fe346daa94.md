---
title: "おすすめgitignore"
emoji: "🎉"
type: "tech"
topics: []
published: false
---

# Miscellaneous
*.class
*.log
*.pyc
*.swp
.DS_Store
.atom/
.buildlog/
.history
.svn/
migrate_working_dir/

# IntelliJ related
*.iml
*.ipr
*.iws
.idea/

# The .vscode folder contains launch configuration and tasks you configure in
# VS Code which you may wish to be included in version control, so this line
# is commented out by default.
#.vscode/

# Flutter/Dart/Pub related
**/doc/api/
**/ios/Flutter/.last_build_id
.dart_tool/
.flutter-plugins
.flutter-plugins-dependencies
.packages
.pub-cache/
.pub/
/build/

# Symbolication related
app.*.symbols

# Obfuscation related
app.*.map.json

# Android Studio will place build artifacts here
/android/app/debug
/android/app/profile
/android/app/release

# FVM Version Cache
.fvm/

# Generated file
*.g.dart
*.gen.dart
*.freezed.dart
*.lock
/generated/intl

# Ignore Firebase configuration files
ios/Runner/GoogleService-Info.plist
ios/flavors/*/GoogleService-Info.plist
android/app/google-services.json
android/app/src/*/google-services.json

# Dart-Defines.xcconfig
ios/Flutter/Dart-Defines.xcconfig