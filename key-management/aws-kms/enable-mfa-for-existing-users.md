---
description: MFA なしで AWS KMS の N Wallet を使っている組織が、MFA を使うように切り替える手順です。
---

# すでに N Wallet を使っている場合の MFA の設定

{% hint style="warning" %}
本手順の対象者：\
MFA なしで AWS KMS の N Wallet を使っている組織の、インフラ担当と N Wallet で署名する人
{% endhint %}

次の順番で行ってください。各手順の詳しい操作は、リンク先のページにあります。

## 手順

1. **署名する人**: N Wallet を最新版に更新する（[N Walletの手動アップデート](update-n-wallet.md)）
2. **インフラ担当**: 各 IAM ユーザーに、期限付きの MFA 登録用ポリシーを付ける（[IAMユーザーの作成](create-iam-user-for-signing.md)の手順4）
3. **署名する人**: 期限内に、「N Cloud Key 管理」→ 鍵のメニュー →「MFA 設定」で MFA を設定する（[MFA 設定](n-wallet-mfa-settings.md)）
4. **インフラ担当**: IAM コンソールで、各 IAM ユーザーの「Security credentials」に MFA デバイスが登録されたことを確認する
5. **インフラ担当**: KMS の許可に MFA の条件を付け、MFA なしで署名できる経路が無いか確認する（[IAMポリシーの作成](create-iam-policy-for-signing.md)の手順9・10）
6. **署名する人**: ブラウザを開き直し、認証アプリのコードを入力して署名できることを確認する（[MFA を設定した N Cloud Key で署名する](sign-with-mfa.md)）

{% hint style="danger" %}
署名する人全員が MFA を設定する前に手順5を行うと、MFA を設定していない人は署名できなくなります。
{% endhint %}

{% hint style="info" %}
IAM コンソールで MFA デバイスを登録し、「ARN を入力」で設定してもらった場合は、設定し終えたことを本人に確認してから手順5を行ってください。
{% endhint %}

## 次の場合は、手順2・3の代わりに

* **同じ IAM ユーザー（同じアクセスキー）を複数人で使っている**: [複数人で N Wallet を使う場合](multiple-signers.md)の「同じ IAM ユーザーを共有する場合」
* **同じ N Cloud Key を複数の PC・ブラウザで使っている**: 1台目で MFA を設定した後、ほかの PC・ブラウザでは「MFA 設定」の「ARN を入力」で同じ ARN を設定する（[MFA 設定](n-wallet-mfa-settings.md)の「ARN を入力する」）

## 完了の確認

署名する人全員の「N Cloud Key 管理」で、すべての N Cloud Key に「MFA 設定済み」が表示され、「MFA なしで署名できます」が表示されていなければ完了です。

{% hint style="info" %}
「MFA 設定済み」なのに「MFA なしで署名できます」が残る場合は、手順5が済んでいないか、MFA なしで署名できる経路が残っています（[MFA 設定と「MFA なしで署名できます」の警告](n-wallet-mfa-settings.md)）。
{% endhint %}
