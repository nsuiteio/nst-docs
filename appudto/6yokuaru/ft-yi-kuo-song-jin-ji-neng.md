# FT一括送金機能

December 1st, 2022

## 概要

複数アドレスへの送金が一つの申請で実行可能になりました。これまで[NFT Mint専用フォームで一括Mint機能](../5.nft-guan-lian-ji-neng/nft-mint-fmu-mint.md)を実装してきましたが、同じ操作感でFTの一括送金・一括配布が可能となります。

{% hint style="warning" %}
本機能はマルチシグウォレットは非対応となります。

Ledgerに関しても利用可能ですが、送付する宛先の数だけ署名操作が必要になります。
{% endhint %}

### 操作手順

1. ワークフロー > 新規申請ボタン > 送金 > まとめて送金 を選択

<figure><img src="../../.gitbook/assets/image (84).png" alt=""><figcaption></figcaption></figure>



2\. 通常の申請同様に必要事項を記入した後、送金先・金額の一覧をアップロードするためのテンプレートファイルをダウンロード

<figure><img src="../../.gitbook/assets/image (85).png" alt=""><figcaption></figcaption></figure>



3\. A列に送金先のアドレス、B列に金額を入力しファイルを保存

<figure><img src="../../.gitbook/assets/image (86).png" alt=""><figcaption><p>記入例</p></figcaption></figure>



4\. ファイルをアップロードすると、プレビュー画面に送金先アドレス / 送金額が表示されます。申請前にご確認ください。

<figure><img src="../../.gitbook/assets/image (87).png" alt=""><figcaption></figcaption></figure>



5\. 申請をした後、承認⇒署名まで進めるとTxが全てまとめて実行されます。

<figure><img src="../../.gitbook/assets/image (83).png" alt=""><figcaption></figcaption></figure>

