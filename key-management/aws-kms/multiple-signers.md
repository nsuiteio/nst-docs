---
description: 複数人が、MFA を設定した AWS KMS の鍵を N Wallet で使う場合の構成と手順です。
---

# 複数人で N Wallet を使う場合

{% hint style="warning" %}
本手順の対象者：\
IAMユーザーとアクセスキーを発行するAWSの管理者（インフラ担当）
{% endhint %}

## おすすめ: 一人ずつ IAM ユーザーを作る

N Wallet を使う人ごとに、[IAMユーザーの作成](create-iam-user-for-signing.md)の手順1〜5を行います。KMS の鍵は同じものを使えます。

{% hint style="info" %}
各自が N Wallet の QR コードで、自分で MFA デバイスを登録できます。一人が辞めたり端末をなくしたりしても、その人のアクセスキーだけを止められ、誰が署名したかも IAM ユーザー名で分かります。
{% endhint %}

## 同じ IAM ユーザー（同じアクセスキー）を共有する場合

最初の1人は、一人ずつ作る場合と同じ手順です。**後から加わる人**の MFA デバイスは、次の手順で登録します。

{% hint style="info" %}
1つの IAM ユーザーで2台目以降の MFA デバイスは、N Wallet の QR コードでは登録できません（AWS の仕様）。そのため、インフラ担当が AWS コンソールで登録します。MFA デバイスは1ユーザーにつき8台までです。
{% endhint %}

### インフラ担当が AWS コンソールで行う

1. IAM →「Users」→ 共有している IAM ユーザー →「Security credentials」タブ →「Assign MFA device」をクリック
2. 「Device name」に名前（例: `suzuki-phone`）を入力し、「Authenticator app」を選んで「Next」をクリック
3. 「Show QR code」で QR コードを表示し、後から加わる人に自分のスマホの認証アプリで読み取ってもらう
4. 後から加わる人の認証アプリに表示される連続した2つのコードを「MFA code 1」「MFA code 2」に入力し、「Add MFA」をクリック
5. 「Security credentials」の MFA デバイスの一覧に表示された、追加したデバイスの ARN（「Identifier」）を、後から加わる人に伝える

{% hint style="danger" %}
QR コードは MFA の秘密情報です。対面で読み取ってもらうのが安全です。画面共有で読み取る場合は、録画しないでください。
{% endhint %}

### 後から加わる人が N Wallet で行う

1. 共有のアクセスキーで [N Walletの初期設定](register-aws-kms-address-in-n-wallet.md)を行い、MFA は「ほかの PC・ブラウザで使っている（ARN を入力）」を選ぶ
2. 伝えられた ARN を入力して「登録」をクリック
3. 「鍵を選択」画面で「アドレスを取得」をクリックし、自分の認証アプリのコードを入力する

<figure><img src="../../.gitbook/assets/n-wallet-kms-register-form-mfa-arn.png" alt="初期設定の登録フォーム。MFA はほかの PC・ブラウザで使っている（ARN を入力）が選ばれている" width="357"><figcaption><p>手順1: 「ほかの PC・ブラウザで使っている（ARN を入力）」を選ぶ</p></figcaption></figure>

{% hint style="info" %}
すでに N Wallet にそのアクセスキーを登録している場合は、「N Cloud Key 管理」→ 鍵のメニュー →「MFA 設定」→「ARN を入力」で設定します（[MFA 設定](n-wallet-mfa-settings.md)）。
{% endhint %}

{% hint style="info" %}
誰の MFA デバイスで署名したかは、CloudTrail で確認できます。
{% endhint %}
