# FMRuby Coreについて

## 概要

FMRuby Coreは、ESP32-S3-N16R8向けに設計された組み込みOSで、ハードウェアアクセラレーテッドグラフィックス機能を備えた軽量なマルチVMランタイム環境を提供します。

## システムアーキテクチャ

### マルチVMランタイム

FMRuby Coreは複数の実行環境をサポートします：

- **mruby (PicoRuby)**: PicoRuby実装によるRubyスクリプティング
- **Lua 5.4**: Luaスクリプトエンジン
- **ネイティブC**: 直接的なC関数実行

各VMは独立したメモリ管理で動作し、アプリケーションの安定性とセキュリティを確保します。

### ハードウェアプラットフォーム

**対象ハードウェア**: ESP32-S3-N16R8
- 16MB Flash
- 8MB PSRAM
- デュアルコアプロセッサ
- ハードウェアグラフィックスアクセラレーション対応

**対応ペリフェラル**:
- USBホスト（キーボード/マウス）
- SDカード
- SPI（別のESP32-WROVERへのNTSC映像出力用）

### グラフィックスシステム

- **キャンバスベースレンダリング**: 効率的なグラフィックス抽象化
- **LovyanGFX互換API**: 業界標準のグラフィックスインターフェース
- **NTSC映像出力**: アナログビデオ出力機能
- **ハードウェア抽象化層**: プラットフォーム非依存のグラフィックスAPI

### オーディオシステム

- APUエミュレーションによる音声処理
- サウンド合成と再生機能

### タスク管理

- **FreeRTOSベース**: 業界標準のRTOS基盤
- **マルチタスク**: 並行アプリケーション実行
- **メモリ分離**: アプリケーション毎のメモリ保護
- **メッセージングシステム**: プロセス間通信（IPC）

## プロジェクト構造

```
components/          ESP-IDFコンポーネント
  ├── lua/          Lua 5.4 VMと拡張機能
  ├── picoruby-esp32/ mruby VM（サブモジュール）
  ├── fmrb_*/       FMRubyコアライブラリ
  │   ├── fmrb_hal/     ハードウェア抽象化層
  │   ├── fmrb_gfx/     グラフィックスシステム
  │   ├── fmrb_mem/     メモリ管理
  │   ├── fmrb_msg/     メッセージングシステム
  │   ├── fmrb_audio/   オーディオシステム
  │   └── ...
  └── ...
main/               FMRuby OSカーネルとアプリケーション層
  ├── kernel/       コアOSカーネル
  ├── app/          アプリケーションランタイム
  └── drivers/      ハードウェアドライバ
flash/              フラッシュファイルシステムの内容
  ├── apps/         アプリケーション
  └── configs/      設定ファイル
host/               PCシミュレーション環境（SDL2）
lib/                カスタムmrbgemsとパッチ
doc/                ドキュメント
```

## ビルド要件

### ESP32ビルド

- **Docker**: ESP-IDF v5.5.1コンテナ
- **Ruby**: ビルドスクリプト用（Rakefile）

### Linuxシミュレーションビルド

**Ubuntu/Debian**:
```bash
sudo apt-get install libsdl2-dev libmsgpack-dev pkg-config clang-format clang-tidy llvm
```

**macOS**:
```bash
brew install sdl2 msgpack pkg-config llvm
```

**Ruby Gems**:
```bash
gem install serialport
```

## 開発ワークフロー

### ビルドコマンド

```bash
# Linuxシミュレーション
rake build:linux

# ESP32ハードウェア
rake build:esp32

# クリーンビルド
rake clean

# すべてのコマンドを表示
rake -T
```

### ドキュメント生成

```bash
# C/C++ APIドキュメント（Doxygen）
rake doc:c

# Ruby APIドキュメント（YARD）
rake doc:ruby

# すべてのドキュメントを生成
rake doc:all

# ドキュメントをクリーン
rake doc:clean
```

## 主要技術

- **ESP-IDF v5.5.1**: Espressif IoT開発フレームワーク
- **FreeRTOS**: リアルタイムオペレーティングシステム
- **PicoRuby**: 軽量なmruby実装
- **Lua 5.4**: スクリプト言語
- **LovyanGFX**: グラフィックスライブラリ
- **SDL2**: Linux/macOS用シミュレーション環境
- **MkDocs**: ドキュメントサイトジェネレーター
- **Material for MkDocs**: ドキュメントテーマ
- **Doxygen**: C/C++ APIドキュメント
- **YARD**: Ruby APIドキュメント

## デュアルプラットフォーム開発

FMRuby Coreは2つのプラットフォームでの開発をサポートします：

1. **ESP32ターゲット**: すべてのペリフェラルサポートを含む完全なハードウェア実装
2. **Linuxシミュレーション**: 高速な開発とテストのためのSDL2ベースのシミュレーション

このアプローチにより以下が可能になります：
- 開発中の高速なイテレーション（Linux）
- 頻繁な書き込みなしでのハードウェア検証（Linux）
- 必要に応じた完全なハードウェアテスト（ESP32）

## 詳細情報

詳細な開発ガイドライン、アーキテクチャの決定事項、コーディング規約については、fmruby-coreリポジトリのCLAUDE.mdファイルを参照してください。

## ライセンス

詳細はfmruby-coreリポジトリのLICENSEファイルをご覧ください。
