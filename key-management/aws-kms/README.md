---
description: AWS KMS
---

# AWS KMS

AWS KMS で管理する秘密鍵を、N Wallet から使って署名できます。N Wallet には、署名の権限を持つ IAM ユーザーのアクセスキーを登録します。

## MFA（多要素認証）

N Wallet に登録するアクセスキー（N Cloud Key）ごとに、任意で MFA を設定できます。MFA を設定した N Cloud Key では、署名の前にスマホの認証アプリに表示される6桁のコードを入力します。

さらに、インフラ担当が KMS の許可に MFA の条件を付けると、**アクセスキーが単体で漏れても、それだけでは署名できなくなります**。N Wallet の登録画面でも、MFA を使うことを標準にしています。

* 使える認証方式は、認証アプリ（Google Authenticator、Microsoft Authenticator、1Password など）の時刻ベースのコード（TOTP）だけです。物理キーやパスキーは使えません（AWS の仕様で、MFA で保護した API の利用は U2F セキュリティキーに対応していないため）。
* 正しいコードを入力すると、その後およそ1時間はコードなしで署名できます。
* MFA を設定しない N Cloud Key の動きは、これまでと変わりません。
* MFA に対応しているのは N Wallet（Chrome 拡張）だけです。N Suite モバイルアプリは未対応のため、モバイルアプリで使う IAM ユーザーには、KMS の許可に MFA の条件を付けないでください。

{% hint style="warning" %}
この MFA は、N Board へのログインに使う[二要素認証(2FA)](../../setup/admin/two-factor-authentication.md)とは別のものです。N Board の 2FA を有効にしていても、アクセスキーでの署名は保護されません。
{% endhint %}

## 読む人ごとのページ

### インフラ担当（AWS の管理者）

1. [初回ログイン手順](first-login.md)
2. AWS KMS の秘密鍵の作成（[macOS](create-aws-kms-private-key-macos.md) / [Windows](create-aws-kms-private-key-windows.md)）
3. [IAMポリシーの作成](create-iam-policy-for-signing.md)（MFA の条件を含む）
4. [IAMユーザーの作成](create-iam-user-for-signing.md)（MFA 登録用のポリシーを含む）
5. [複数人で N Wallet を使う場合](multiple-signers.md)

### N Wallet を使う人

1. [N Walletのインストール](install-n-wallet.md)
2. [N Walletの初期設定（AWS KMSのアドレス登録）](register-aws-kms-address-in-n-wallet.md)
3. [アドレスのN Walletへの追加方法](add-address-to-n-wallet.md)
4. [MFA を設定した N Cloud Key で署名する](sign-with-mfa.md)
5. [MFA 設定と「MFA なしで署名できます」の警告](n-wallet-mfa-settings.md)
6. [別の PC・ブラウザで使う](use-on-another-pc.md)

{% hint style="info" %}
**これまで MFA なしで使っていて、MFA に切り替える場合**\
[MFA なしで使っている場合の MFA への切り替え](enable-mfa-for-existing-users.md)の順番で行ってください。
{% endhint %}
