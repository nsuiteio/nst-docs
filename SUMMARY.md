# Table of contents

## はじめに

* [N Suiteドキュメント](README.md)
  * [初回ログイン手順](getting-started/roguin.md)
  * [動作環境](getting-started/dong-zuo-huan-jing.md)
  * [対応ネットワーク](getting-started/nettowku.md)

## 導入・初期設定

* [導入・初期設定](setup/README.md)
  * [管理者向け設定](setup/admin/README.md)
    * [組織/チーム/ロール](setup/admin/organization-team-roles/README.md)
      * [組織](setup/admin/organization/README.md)
        * [組織へのメンバー追加](setup/admin/organization/henomenb.md)
        * [チームの作成](setup/admin/organization/chmuno.md)
      * [チーム](setup/admin/team/README.md)
        * [チームへのメンバー追加](setup/admin/team/chmuhenomenb.md)
        * [チームへの保有アドレス登録](setup/admin/team/chmuhenoadoresu.md)
        * [チーム内メンバーの編集・削除](setup/admin/team/chmumenbno.md)
      * [ロール](setup/admin/roles/README.md)
        * [組織ロールの説明](setup/admin/roles/rruno.md)
        * [チームロールの説明](setup/admin/roles/chmurruno.md)
    * [ワークフロー](setup/admin/workflow/README.md)
      * [ワークフローのプロセス設定](setup/admin/workflow/wkufurnopurosesu.md)
      * [プロセスに 「適用条件」 を設定する](setup/admin/workflow/purosesuni-wosuru.md)
    * [二要素認証(2FA)](setup/admin/er-yao-su-ren-zheng-2fa.md)

## 署名・鍵管理

* [署名・鍵管理](key-management/README.md)
  * [MPC](key-management/mpc/README.md)
    * [MPCの概要](key-management/mpc/mpcno.md)
    * [MPCの有効化](key-management/mpc/mpcno-1.md)
    * [MPC署名権の付与](key-management/mpc/mpcno-2.md)
    * [MPCのアドレス作成](key-management/mpc/mpcnoadoresu.md)
  * [マルチシグウォレット](key-management/multisig-wallet/README.md)
    * [マルチシグウォレットの概要](key-management/multisig-wallet/maruchishiguworettono.md)
    * [マルチシグウォレット：初期設定の手順](key-management/multisig-wallet/maruchishiguworettono-1.md)
    * [既存のマルチシグウォレットへアドレスを追加登録](key-management/multisig-wallet/nomaruchishiguworettoheadoresuwo.md)
    * [既存のマルチシグウォレットからアドレスを削除](key-management/multisig-wallet/nomaruchishiguworettokaraadoresuwo.md)
  * [AWS KMS](key-management/aws-kms/README.md)
    * [初回ログイン手順](key-management/aws-kms/roguin.md)
    * [AWS KMSの秘密鍵作成手順 （macOS向け）](key-management/aws-kms/aws-kmsno-macoske.md)
    * [AWS KMSの秘密鍵作成手順（Windows向け）](key-management/aws-kms/aws-kmsnowindowske.md)
    * [IAMポリシーの作成：秘密鍵の署名権限を作成する手順](key-management/aws-kms/iamporishnonowosuru.md)
    * [IAMユーザーの作成：秘密鍵の署名権限ユーザーを作成する手順](key-management/aws-kms/iamyznonoyzwosuru.md)
    * [N Walletのインストール](key-management/aws-kms/n-walletnoinsutru.md)
    * [N Walletの初期設定（AWS KMSのアドレス登録）](key-management/aws-kms/n-walletnoaws-kmsnoadoresu.md)
    * [アドレスのN Walletへの追加方法](key-management/aws-kms/adoresunon-walletheno.md)
    * [アドレスとN Cloud Keyへの名前登録](key-management/aws-kms/adoresuton-cloud-keyheno.md)
    * [N Walletの手動アップデート](key-management/aws-kms/n-walletnoappudto.md)
  * [Ledger](key-management/ledger/README.md)
    * [N Walletのインストール](key-management/ledger/n-walletnoinsutru.md)
    * [N Walletの初期設定（Ledgerのアドレス登録）](key-management/ledger/n-walletnoledgernoadoresu.md)
    * [アドレスのN Walletへの追加方法](key-management/ledger/adoresunon-walletheno.md)
    * [アドレスとN Cloud Keyへの名前登録](key-management/ledger/adoresuton-cloud-keyheno.md)
    * [N Walletの手動アップデート](key-management/ledger/n-walletnoappudto.md)

## N Boardの基本操作

* [N Boardの使い方](n-board/README.md)
  * [申請のコピー](n-board/nokop.md)
  * [任意のトークン追加](n-board/notkun.md)
  * [外部サービスからの申請作成](n-board/sbisukarano.md)
  * [カスタムネットワークの追加](n-board/kasutamunettowkuno.md)

## NFT関連機能

* [NFT関連機能](nft/README.md)
  * [NFTの送付の方法](nft/nftnono.md)
  * [NFT Mint 専用フォーム](nft/nft-mint-fmu.md)
  * [NFT Mint 専用フォーム - 大量同時Mint](nft/nft-mint-fmu-mint.md)
  * [NFT一括Mint - 1Tx辺りの上限設定](nft/nftmint-1txrino.md)

## 応用機能・各種設定

* [応用機能・各種設定](advanced-settings/README.md)
  * [ネットワーク設定](advanced-settings/network/README.md)
    * [ネットワーク追加: Klaytn](advanced-settings/network/nettowku-klaytn.md)
    * [ネットワーク追加: Optimism](advanced-settings/network/nettowku-optimism.md)
    * [ネットワーク追加: Arbitrum](advanced-settings/network/nettowku-arbitrum.md)
    * [ネットワーク追加: Avalanche / Testnet系](advanced-settings/network/nettowku-avalanche-testnet.md)
    * [ネットワーク追加: BSC / Binance Smart Chain](advanced-settings/network/nettowku-bsc-binance-smart-chain.md)
  * [プリセットコントラクトの一覧](advanced-settings/purisettokontorakutono.md)
  * [コントラクトメソッドの実行手順](advanced-settings/kontorakutomesoddono.md)
  * [コントラクトメソッドの一括実行](advanced-settings/kontorakutomesoddono-1.md)
  * [Wallet Connect の接続方法](advanced-settings/wallet-connect-no.md)
  * [FT一括送金機能](advanced-settings/ft-yi-kuo-song-jin-ji-neng.md)
  * [Gas代の編集](advanced-settings/gasno.md)
  * [請求書送付先メールアドレスの変更手順](advanced-settings/mruadoresuno.md)

## スマートフォンでの利用

* [スマートフォンでの使い方](mobile/README.md)
  * [スマートフォンアプリについて](mobile/sumtofonapurinitsuite.md)
  * [スマホUI: 申請一覧と申請詳細](mobile/sumahoui-to.md)
