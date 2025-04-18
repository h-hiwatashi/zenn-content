---
title: "個人的 Flutter 環境構築"
emoji: "🐣"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [Flutter, Dart]
published: true
published_at: 2025-04-19 09:00
---

# この記事について

PC を新調し Flutter の環境構築を改めて行なったので、そのときの備忘録をまとめました。

# この記事の対象読者

- 環境構築から FVM で Flutter のバージョンを管理したい方。
- 既存プロジェクトの Java のバージョンが古い状態で環境構築したい方。

# 環境構築

## iOS

1. Xcode を install

   App Store からダウンロード

## Flutter

FVM でバージョン管理を行いたいため、 Flutter SDK を直接インストールはしません！

1. fvm install

   ```.zshrc
   brew tap leoafarias/fvmbrew
   install fvm
   ```

1. fvm の PATH を通す

   ```.zshrc
   export PATH="$PATH:$HOME/.pub-cache/bin"
   ```

## VS Code

1. VS Code
   設定 dart.flutterSdkPath に ".fvm/flutter_sdk" を設定

   ```settings.json
    {
    "dart.flutterSdkPath": ".fvm/flutter_sdk"
    }
   ```

1. プロジェクトルートで `fvm install` を実行

## Android

1. Android Studio install

   公式 Doc: https://developer.android.com/studio?hl=ja

1. Android Studio のプラグインに Flutter をインストール
1. Android Studio の Flutter SDK path に以下を設定
   ```
   /{プロジェクトのパス}/.fvm/flutter_sdk
   ```

## インストールが終わったら

1. プロジェクトルートにて `fvm flutter doctor`を実行する。
1. 不足しているライブラリやツールが表示されるため、出力されたメッセージに従って各種設定・インストールを行う

何もインストールしていない PC では大抵以下が要求されます。

### Android のライセンス

1. 以下を実行

   `flutter doctor --android-licenses`

### CocoaPods

1. CocoaPods のインストール
1. Ruby のバージョンを更新

### もし Java のバージョンをダウングレードする必要があった場合

既存プロジェクトの Android Studio のバージョンが古い場合、Java のバージョンを下げる必要があります。

1. 以下コマンドで Java のバージョンが正しい確認。
   fvm flutter analyze --suggestions

1. 以下を参考に java 17.0.7-zulu をインストールする。
   https://qiita.com/nacho4d/items/a9f0e1a0ec5e22e6f16d
1. `echo $JAVA_HOME`で Java のパスを確認。
1. 以下コマンドで Flutter の Java のパスを更新する。
   ```
   fvm flutter config --jdk-dir="Java のパス"
   ```
1. 以下コマンドで Java のエラーが表示されないことを確認。

   `fvm flutter analyze --suggestions`

# 参考

- FVM ( Flutter のバージョン管理ライブラリ)

  https://zenn.dev/altiveinc/articles/flutter-version-management#vs-code

- 環境構築

  https://dev.classmethod.jp/articles/flutter-environment-mac/

- Java の互換性

  https://qiita.com/t_hiro2626/items/e367aa44b631e2a372bb
