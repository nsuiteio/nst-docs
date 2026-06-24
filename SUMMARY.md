# Table of contents

## はじめに

* [N Suiteドキュメント](README.md)
  * [初回ログイン手順](appudto/1hajimeni/roguin.md)
  * [動作環境](appudto/1hajimeni/dong-zuo-huan-jing.md)
  * [対応ネットワーク](appudto/1hajimeni/nettowku.md)

## 導入・初期設定

* [導入・初期設定](appudto/2matome/README.md)
  * [管理者向け設定](appudto/2matome/ke/README.md)
    * [組織/チーム/ロール](appudto/2matome/ke/chmurru/README.md)
      * [組織](appudto/2matome/ke/chmurru/zu-zhi/README.md)
        * [組織へのメンバー追加](appudto/2matome/ke/chmurru/zu-zhi/henomenb.md)
        * [チームの作成](appudto/2matome/ke/chmurru/zu-zhi/chmuno.md)
      * [チーム](appudto/2matome/ke/chmurru/chmu/README.md)
        * [チームへのメンバー追加](appudto/2matome/ke/chmurru/chmu/chmuhenomenb.md)
        * [チームへの保有アドレス登録](appudto/2matome/ke/chmurru/chmu/chmuhenoadoresu.md)
        * [チーム内メンバーの編集・削除](appudto/2matome/ke/chmurru/chmu/chmumenbno.md)
      * [ロール](appudto/2matome/ke/chmurru/rru/README.md)
        * [組織ロールの説明](appudto/2matome/ke/chmurru/rru/rruno.md)
        * [チームロールの説明](appudto/2matome/ke/chmurru/rru/chmurruno.md)
    * [ワークフロー](appudto/2matome/ke/wkufur/README.md)
      * [ワークフローのプロセス設定](appudto/2matome/ke/wkufur/wkufurnopurosesu.md)
      * [プロセスに 「適用条件」 を設定する](appudto/2matome/ke/wkufur/purosesuni-wosuru.md)
    * [二要素認証(2FA)](appudto/2matome/ke/er-yao-su-ren-zheng-2fa.md)

## 署名・鍵管理

* [署名・鍵管理](appudto/3.-shu-ming-jian-guan-li/README.md)
  * [MPC](appudto/3.-shu-ming-jian-guan-li/mpc/README.md)
    * [MPCの概要](appudto/3.-shu-ming-jian-guan-li/mpc/mpcno.md)
    * [MPCの有効化](appudto/3.-shu-ming-jian-guan-li/mpc/mpcno-1.md)
    * [MPC署名権の付与](appudto/3.-shu-ming-jian-guan-li/mpc/mpcno-2.md)
    * [MPCのアドレス作成](appudto/3.-shu-ming-jian-guan-li/mpc/mpcnoadoresu.md)
  * [マルチシグウォレット](appudto/3.-shu-ming-jian-guan-li/maruchishiguworetto/README.md)
    * [マルチシグウォレットの概要](appudto/3.-shu-ming-jian-guan-li/maruchishiguworetto/maruchishiguworettono.md)
    * [マルチシグウォレット：初期設定の手順](appudto/3.-shu-ming-jian-guan-li/maruchishiguworetto/maruchishiguworettono-1.md)
    * [既存のマルチシグウォレットへアドレスを追加登録](appudto/3.-shu-ming-jian-guan-li/maruchishiguworetto/nomaruchishiguworettoheadoresuwo.md)
    * [既存のマルチシグウォレットからアドレスを削除](appudto/3.-shu-ming-jian-guan-li/maruchishiguworetto/nomaruchishiguworettokaraadoresuwo.md)
  * [AWS KMS](appudto/3.-shu-ming-jian-guan-li/aws-kms/README.md)
    * [初回ログイン手順](appudto/3.-shu-ming-jian-guan-li/aws-kms/roguin.md)
    * [AWS KMSの秘密鍵作成手順 （macOS向け）](appudto/3.-shu-ming-jian-guan-li/aws-kms/aws-kmsno-macoske.md)
    * [AWS KMSの秘密鍵作成手順（Windows向け）](appudto/3.-shu-ming-jian-guan-li/aws-kms/aws-kmsnowindowske.md)
    * [IAMポリシーの作成：秘密鍵の署名権限を作成する手順](appudto/3.-shu-ming-jian-guan-li/aws-kms/iamporishnonowosuru.md)
    * [IAMユーザーの作成：秘密鍵の署名権限ユーザーを作成する手順](appudto/3.-shu-ming-jian-guan-li/aws-kms/iamyznonoyzwosuru.md)
    * [N Walletのインストール](appudto/3.-shu-ming-jian-guan-li/aws-kms/n-walletnoinsutru.md)
    * [N Walletの初期設定（AWS KMSのアドレス登録）](appudto/3.-shu-ming-jian-guan-li/aws-kms/n-walletnoaws-kmsnoadoresu.md)
    * [アドレスのN Walletへの追加方法](appudto/3.-shu-ming-jian-guan-li/aws-kms/adoresunon-walletheno.md)
    * [アドレスとN Cloud Keyへの名前登録](appudto/3.-shu-ming-jian-guan-li/aws-kms/adoresuton-cloud-keyheno.md)
    * [N Walletの手動アップデート](appudto/3.-shu-ming-jian-guan-li/aws-kms/n-walletnoappudto.md)
  * [Ledger](appudto/3.-shu-ming-jian-guan-li/ledger/README.md)
    * [N Walletのインストール](appudto/3.-shu-ming-jian-guan-li/ledger/n-walletnoinsutru.md)
    * [N Walletの初期設定（Ledgerのアドレス登録）](appudto/3.-shu-ming-jian-guan-li/ledger/n-walletnoledgernoadoresu.md)
    * [アドレスのN Walletへの追加方法](appudto/3.-shu-ming-jian-guan-li/ledger/adoresunon-walletheno.md)
    * [アドレスとN Cloud Keyへの名前登録](appudto/3.-shu-ming-jian-guan-li/ledger/adoresuton-cloud-keyheno.md)
    * [N Walletの手動アップデート](appudto/3.-shu-ming-jian-guan-li/ledger/n-walletnoappudto.md)

## N Boardの基本操作

* [N Boardの使い方](appudto/4n-boardnoi/README.md)
  * [申請のコピー](appudto/4n-boardnoi/nokop.md)
  * [任意のトークン追加](appudto/4n-boardnoi/notkun.md)
  * [外部サービスからの申請作成](appudto/4n-boardnoi/sbisukarano.md)
  * [カスタムネットワークの追加](appudto/4n-boardnoi/kasutamunettowkuno.md)

## NFT関連機能

* [NFT関連機能](appudto/5.nft-guan-lian-ji-neng/README.md)
  * [NFTの送付の方法](appudto/5.nft-guan-lian-ji-neng/nftnono.md)
  * [NFT Mint 専用フォーム](appudto/5.nft-guan-lian-ji-neng/nft-mint-fmu.md)
  * [NFT Mint 専用フォーム - 大量同時Mint](appudto/5.nft-guan-lian-ji-neng/nft-mint-fmu-mint.md)
  * [NFT一括Mint - 1Tx辺りの上限設定](appudto/5.nft-guan-lian-ji-neng/nftmint-1txrino.md)

## 応用機能・各種設定

* [応用機能・各種設定](appudto/6yokuaru/README.md)
  * [ネットワーク設定](appudto/6yokuaru/nettowku/README.md)
    * [ネットワーク追加: Klaytn](appudto/6yokuaru/nettowku/nettowku-klaytn.md)
    * [ネットワーク追加: Optimism](appudto/6yokuaru/nettowku/nettowku-optimism.md)
    * [ネットワーク追加: Arbitrum](appudto/6yokuaru/nettowku/nettowku-arbitrum.md)
    * [ネットワーク追加: Avalanche / Testnet系](appudto/6yokuaru/nettowku/nettowku-avalanche-testnet.md)
    * [ネットワーク追加: BSC / Binance Smart Chain](appudto/6yokuaru/nettowku/nettowku-bsc-binance-smart-chain.md)
  * [プリセットコントラクトの一覧](appudto/6yokuaru/purisettokontorakutono.md)
  * [コントラクトメソッドの実行手順](appudto/6yokuaru/kontorakutomesoddono.md)
  * [コントラクトメソッドの一括実行](appudto/6yokuaru/kontorakutomesoddono-1.md)
  * [Wallet Connect の接続方法](appudto/6yokuaru/wallet-connect-no.md)
  * [FT一括送金機能](appudto/6yokuaru/ft-yi-kuo-song-jin-ji-neng.md)
  * [Gas代の編集](appudto/6yokuaru/gasno.md)
  * [請求書送付先メールアドレスの変更手順](appudto/6yokuaru/mruadoresuno.md)

## スマートフォンでの利用

* [スマートフォンでの使い方](appudto/7sumtofondenoi/README.md)
  * [スマートフォンアプリについて](appudto/7sumtofondenoi/sumtofonapurinitsuite.md)
  * [スマホUI: 申請一覧と申請詳細](appudto/7sumtofondenoi/sumahoui-to.md)
