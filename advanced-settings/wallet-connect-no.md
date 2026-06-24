---
description: ※OpenSea を例に解説（NFTマーケットプレイス以外の dApps にも対応）
---

# Wallet Connect の接続方法

{% hint style="info" %}
<sub>Wallet Connectは、スマートフォンのウォレットアプリを使って、さまざまなdApps（分散型アプリケーション）に安全に接続するためのプロトコルです。</sub>\ <sub>※NFTマーケットプレイス 以外の dApps にも対応します。</sub>
{% endhint %}

### ■ OpenSeaを例にしたWallet Connectの接続手順

**1：接続準備**

* OpenSea のサイトを開く（ブラウザ、またはスマートフォン）
* 右上の 「 ウォレット接続 」 を押下　≫　「 Wallet Connect 」 を選択

<div align="left"><figure><img src="../.gitbook/assets/スクリーンショット 2025-06-19 163400.png" alt=""><figcaption></figcaption></figure></div>

<div align="left"><figure><img src="../.gitbook/assets/スクリーンショット 2025-06-19 161619.png" alt="" width="176"><figcaption></figcaption></figure></div>

**2：QRコードの読み取り**

* 画面に QRコード が表示される

<div align="left"><figure><img src="../.gitbook/assets/スクリーンショット 2025-06-19 161824.png" alt="" width="176"><figcaption></figcaption></figure></div>

* スマートフォンの N Boardアプリ を起動
* アプリ内右上「 QAコード読み取り 」マークを押下

<div align="left"><figure><img src="../.gitbook/assets/スクリーンショット 2025-06-19 152012.png" alt="" width="375"><figcaption></figcaption></figure></div>

・QRコード をカメラで読み取る

**3：接続設定**

* アプリ内で接続する ウォレットアドレス を選択

<div align="left"><figure><img src="../.gitbook/assets/スクリーンショット 2025-06-20 104051.png" alt="" width="177"><figcaption></figcaption></figure></div>

* ネットワークを選択（例：Ethereum ）

<div align="left"><figure><img src="../.gitbook/assets/スクリーンショット 2025-06-20 104637.png" alt="" width="244"><figcaption></figcaption></figure></div>

* 「 接続 」 を押下し、OpenSea 側との接続が完了

<div align="left"><figure><img src="../.gitbook/assets/スクリーンショット 2025-06-20 105037.png" alt="" width="190"><figcaption></figcaption></figure></div>

### **■マルチシグウォレットの注意点**

* マルチシグウォレットでも Wallet Connect を使って dApps に接続することは可能です。
* QRコード を読み取り、マルチシグアドレス を選択して接続します。

　 <sub>※OpenSea のような 「EPI-191準拠」 のメッセージ署名を要求する dApps では、署名処理が必要となり、</sub>

　　 <sub>現状 N Suite のマルチシグウォレットは 「EIP-191署名」 に対応していないため、 エラー が生じます。</sub>

\
&#xNAN;**■まとめ**

* Wallet Connect を使えば、スマートフォンの N Wallet から安全かつ柔軟に dApps へ接続することが可能です。
* 本マニュアルでは OpenSea を例に接続手順を紹介しましたが、NFTマーケットプレイス 以外の dApps にも同様の手順で対応できます。
* EOA（Externally Owned Account）やMPC（Multi-Party Computation）ウォレットは、EIP‑191準拠 のメッセージ署名に対応しているため、署名が必要な dApps でも問題なく利用できます。
