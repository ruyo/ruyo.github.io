---
title: "ライト環境に合わせる"

#gallery:
#  - url: /VRM4U/assets/images/010_top.png
#    image_path: /VRM4U/assets/images/010_top.png

#gallery2:
#  - url: /VRM4U/assets/images/010_release.png
#    image_path: /VRM4U/assets/images/010_release.png

# {% include gallery id="gallery" caption="This is a sample gallery with **Markdown support**." %}

# {% include gallery id="gallery2" %}

# [![](./assets/images/small/010_release.png)](../assets/images/010_release.png)

# [![](/assets/images/010_release.png)](/assets/images/010_release.png)

# [![](/VRM4U/assets/images/010_release.png)](https://ruyo.github.io/VRM4U/assets/images/010_release.png)

---

----
このドキュメントは書きかけです。

----
## 概要

UE4のライト環境は多種多様であり、キャラクタが極端に「明るく/暗く」「薄く/濃く」描画されることがあります。それらの補正方法を紹介します。

----
## 先に結論

MaterialSystemより、`PreLightScale`　と　`PostLightScale` を組合せて補正します。

VRM4UのLitマテリアルは、主光源が3.14 luxの時に原色に近い色が出ます。
この明るさから離れるほど色の再現度が低くなります。

補正はマテリアル側で行います。ライト側は変更しません。
以下のように補正します。


|主光源の明るさ|補正方法|典型的なシーン||
|:-|:-|:-|-|
|1～3.14 lux|Preを上げてPostを下げる|DayLightテンプレート|
|3.14 lux|補正必要なし|標準テンプレート|
|3.14～10,000 lux 以上|Preを下げてPostを上げる|太陽光を再現したIBL環境や、光源デフォルト値を利用したもの|


----
## 補正の詳しい話

### Litマテリアルの補正
VRM4UではFilmicTonemapperを逆変換しています。逆変換処理には、ライト強度とExposureを利用します。PreとPostが、それぞれの補正に対応しています。

### SSSマテリアルの補正
ライトに対する補正は不要ですが、モデルの材質・見た目に合わせる調整は必要です。

`PostLightScale`に初期値として0.5を利用しています。これは原色テクスチャをAlbedoとして違和感なく利用するための補正値で、この値は適宜調整する必要があります。
