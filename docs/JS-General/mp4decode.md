# 動画のデコードについて
!!! warning "クラス名の変更について"
    **v1.2.7**以降、Mp4Decoderというクラス名をMediaDecoderに変更しています。

    Mp4以外のデコードにも備えたクラス名としました。

    なお、従来のMp4Decoderを使用した場合、MediaDecoderを経由しており機能しますが、非推奨であり今後Mp4Decoderは削除する予定です。
## 用途
- この機能は、街頭サイネージや電車内サイネージ広告などの動画を読み込み、再生することを主な用途としています。
- この機能は、JavaCVというライブラリを使用しています。起動時にダウンロードします。
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
let decoded = MediaDecoder.decode(file);
let frames = decoded.frames();
let pictureIndex0 = frames.get(index).picture(); // ピクチャ(Picture)
let imageIndex0 = MediaDecoder.toBufferedImage(pictureIndex0); // 画像データ(BufferedImage)
// indexは任意の数値
// (namespaces), (path)はmp4ファイルの名前空間，パス
```
    - 音声データの取得サンプル
```js
let inputStream = ResourceUtil.openFile("(namespaces)", "(path)");
let file = ResourceUtil.copyToTempFile(inputStream);
let decoded = MediaDecoder.decode(file);
let pcmSamples = decoded.pcmSamples(); // PCMサンプル配列(short[])
let sampleRate = decoded.sampleRate(); // サンプルレート(int)
// (namespaces), (path)はmp4ファイルの名前空間，パス
```