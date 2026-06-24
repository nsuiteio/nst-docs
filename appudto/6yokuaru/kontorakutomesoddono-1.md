# コントラクトメソッドの一括実行

May 10th, 2023

## 概要

トークンの一括ミントなど、同じコントラクトメソッドを複数同時に実行したい場合、一回の申請でまとめて行えるようになりました。

{% hint style="info" %}
使用する秘密鍵管理オプションによって対応可否がございます。下記参照：
{% endhint %}

<table><thead><tr><th>秘密鍵管理オプション</th><th width="147.33333333333331">対応</th><th>備考</th></tr></thead><tbody><tr><td>クラウド型 (AWS)</td><td>○</td><td></td></tr><tr><td>ハードウェア (Ledger)</td><td>△</td><td>FTを送付する宛先の数だけLedgerで署名操作が必要なため、件数が多い場合は非推奨。</td></tr><tr><td>マルチシグ</td><td>✗</td><td></td></tr></tbody></table>

{% hint style="info" %}
同時に実行できるトランザクション数は200件迄となります。
{% endhint %}

### 操作手順

1. ワークフロー ＞ 新規申請 ＞コントラクトメソッド ＞ 一括実行を選択

<figure><img src="../../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure>

2. チームを選択後、タイトルやメモ等の申請内容を必要に応じて記入します。次に、ネットワーク、実行アドレス、コントラクト、メソッドを選択します。

<figure><img src="../../.gitbook/assets/image (79).png" alt=""><figcaption></figcaption></figure>

3. 一番下のテンプレートファイルをダウンロードをクリックし、アップロード用のCSVをダウンロードします。
4. （サンプルはtransferメソッド）引数をCSVへ入力し、保存します。

<figure><img src="../../.gitbook/assets/image (80).png" alt=""><figcaption></figcaption></figure>

5. ファイルを選択後、アップロードが完了したことを確認します。

<figure><img src="../../.gitbook/assets/image (81).png" alt=""><figcaption></figcaption></figure>

※一件一件の虫眼鏡 (+) マークをクリックすると、申請・実行前に詳細を確認することができます。

<figure><img src="../../.gitbook/assets/image (82).png" alt=""><figcaption></figcaption></figure>

6.  申請をした後、承認⇒署名まで進めるとTxが全てまとめて実行されます。

    <figure><img src="../../.gitbook/assets/image (83).png" alt=""><figcaption></figcaption></figure>
