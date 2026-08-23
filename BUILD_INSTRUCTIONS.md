# Bot Hosting - 本物ネイティブAPKのビルド＆実機インストール手順書

本プロジェクトは **100% 完全なネイティブ Android / Flutter アプリケーション** のソースコード一式です。
Androidのセキュリティ仕様上、実機にインストール可能な署名済みAPKファイルは Android SDK（Java / Gradle）によるコンパイルが必要です。

以下の3つの方法のいずれかで、本物のAPKを取得できます。

---

## 🚀 方法 1: GitHub Actions で無料クラウド自動ビルド（最も簡単・PCスペック不要）

PCにAndroid StudioやJavaをインストールせずに、GitHubの無料サーバーでAPKを自動ビルドできます。

1. [GitHub](https://github.com/) で新規リポジトリを作成します。
2. このZIPを展開した中身をすべてリポジトリにアップロード（Push）します。
3. リポジトリの **「Actions」** タブを開くと、同梱されている `.github/workflows/build_native_apk.yml` が自動起動します。
4. 約2〜3分でビルドが完了し、**Artifacts（成果物）から本物の `app-release.apk` を直接ダウンロード**できます！
5. ダウンロードしたAPKをAndroid端末でタップしてインストールしてください。

---

## 💻 方法 2: Android Studio でワンクリックビルド＆実機デバッグ

1. [Android Studio](https://developer.android.com/studio) を起動します。
2. **「Open」** を選択し、この解凍フォルダを選択して開きます。
3. Gradleの依存同期が完了したら、上部メニューの **「Build」 > 「Build Bundle(s) / APK(s)」 > 「Build APK(s)」** をクリックします。
4. 数十秒で本物の `app-debug.apk` が `app/build/outputs/apk/debug/` に生成されます。
5. Android端末をUSB接続またはWi-Fiデバッグ接続して **「Run (▶)」** を押すと、実機に直接アプリが転送・起動します。

---

## ⚡ 方法 3: コマンドライン（CLI）で1行ビルド

### Flutterの場合:
```bash
flutter pub get
flutter build apk --release
# 生成先: build/app/outputs/flutter-apk/app-release.apk
```

### Android (Gradle) の場合:
```bash
./gradlew assembleRelease
# 生成先: app/build/outputs/apk/release/app-release.apk
```

Android実機への直接インストール:
```bash
adb install -r app/build/outputs/apk/release/app-release.apk
```
