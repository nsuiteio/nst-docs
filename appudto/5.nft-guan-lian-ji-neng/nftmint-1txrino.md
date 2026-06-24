# NFT一括Mint - 1Tx辺りの上限設定

December 1st, 2022

## 概要

OpenSea等のNFTマーケットプレイスは、1TxごとのMint数に上限を設けている場合があります。この際、大量に同時にMintしようとすると不正行為と誤検知されてしまい、Mintができないといった障壁がありました。1Txごとの上限設定をすることにより、この障壁を気にせずに一括Mintを行う事が可能になります。

### 操作手順

[NFT Mint 専用フォームの基本的な使い方](nft-mint-fmu-mint.md)は変わりません。上限設定の画面をアクセスするには、申請フォーム内の「発行リスト」の横にある「詳細設定」をクリックします。

<figure><img src="../../.gitbook/assets/image (88).png" alt=""><figcaption><p>NFT Mint せんようフォーム</p></figcaption></figure>



デフォルトは「自動」が選択されてますので、必要に応じて「指定」をクリックし数値をテキストボックスに入力します。例：OpenSeaの場合は 7 か 8(2022年12月現在) が上限値として最適とされています。

<figure><img src="../../.gitbook/assets/image (89).png" alt=""><figcaption></figcaption></figure>



