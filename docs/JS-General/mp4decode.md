# MP4動画のデコードについて
## 用途
- この機能は、街頭サイネージや電車内サイネージ広告などをMP4から読み込み、再生することを主な用途としています。
- この機能は、JCodecというライブラリを使用しています（Mod内部に同梱しています）。
## 使用法
1. 以下の方法でパッケージをインポートします。
```js
importPackage(Packages.nest.addon.mtrante.patch.ntelib);
```
2. 以下の方法でmp4データを取得します。
    - フレームデータの取得サンプル
```js
let inputStream = ResourceUtil.openFile("(namespaces)", "(path)");
let file = ResourceUtil.copyToTempFile(inputStream);
let decoded = Mp4Decoder.decode(file);
let frames = decoded.frames();
let pictureIndex0 = frames.get(index).picture(); // ピクチャ(Picture)
let imageIndex0 = Mp4Decoder.toBufferedImage(pictureIndex0); // 画像データ(BufferedImage)
// indexは任意の数値
// (namespaces), (path)はmp4ファイルの名前空間，パス
```
    - 音声データの取得サンプル
```js
let inputStream = ResourceUtil.openFile("(namespaces)", "(path)");
let file = ResourceUtil.copyToTempFile(inputStream);
let decoded = Mp4Decoder.decode(file);
let pcmSamples = decoded.pcmSamples(); // PCMサンプル配列(short[])
let sampleRate = decoded.sampleRate(); // サンプルレート(int)
// (namespaces), (path)はmp4ファイルの名前空間，パス
```