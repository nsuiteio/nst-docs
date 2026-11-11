# IAMユーザーの作成：秘密鍵の署名権限ユーザーを作成する手順

{% hint style="warning" %}
IAMユーザーとは？
\
IAMユーザーとは、AWS KMSで作成した秘密鍵にアクセスするために作成される個別のエンティティです。IAMユーザーには、特定のユーザーに関連する認証情報（Access Key ID とSecret Access Key）が割り当てられ、AWS KMSで作成した秘密鍵にアクセスすることが可能です。
{% endhint %}

{% hint style="info" %}
署名実行権限を持つユーザーがAWS KMSで作成した秘密鍵をN Walletで使うには、まず該当するユーザーのIAMユーザーを作成し、次に前回作成したIAMポリシーに紐付け、最後に認証情報としてのAccess Key IDとAecret Access Keyを発行する必要があります。本記事では、その方法を説明します。
{% endhint %}

## 1. IAM ユーザーを作成する

* 「Add users」をクリック

![](<../../.gitbook/assets/Screen Shot 2021-12-10 at 18.45.03.png>)

* 「User name」に任意の名前を入力し、「Next」をクリック

<figure><img src="../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

## 2. IAM ユーザーをIAM ポリシーに紐づける

* 「Attach existing policies directly」を選択し、「IAM ポリシーの作成」で作成したIAM ポリシーにチェックを入れ、「Next」をクリック

<figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

* 「Create user」をクリック (Tagは任意)

<figure><img src="../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

## 3. IAMユーザーに対する認証情報を発行する

* IAMユーザーの一覧に画面が遷移するので、作成したIAM ユーザーを開く

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

* Security credentials をクリック

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

* 下にスクロールし、Access keys内のCreate access keyをクリック

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

* Application running outside AWSを選択し「Next」をクリック

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

* Create access keyをクリック

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

* Access key createdと表示されれば成功です。次章のN Walletの初期設定で使用しますので、Access key / Secret access keyをセキュアな環境に控えて下さい。

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

{% hint style="danger" %}
※ この画面を閉じると `Secret access key` は二度と確認できなくなるため、忘れずに情報を控えてください
{% endhint %}

## 4. MFA 登録用のポリシーを期限付きで付ける

N Wallet を使う人にアクセスキーを渡すときに行います。

1. 作成した IAM ユーザーを開き、「Permissions」→「Add permissions」→「Create inline policy」をクリック
2. 「JSON」に切り替え、中身をすべて消して次を貼り付ける
3. `__DEADLINE__` の2か所を期限の日時（**UTC**。日本時間から9時間引く）に書き換える。1時間後の日時は、CloudShell で `date -u -d '+1 hour' +%Y-%m-%dT%H:%M:%SZ` を実行すると表示されます
4. ポリシー名に `NWalletMfaRegistration` を入力し、「Create policy」をクリック

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowCreateMfaDeviceUntilDeadline",
      "Effect": "Allow",
      "Action": "iam:CreateVirtualMFADevice",
      "Resource": "arn:aws:iam::*:mfa/*",
      "Condition": { "DateLessThan": { "aws:CurrentTime": "__DEADLINE__" } }
    },
    {
      "Sid": "AllowEnableOwnMfaUntilDeadline",
      "Effect": "Allow",
      "Action": ["iam:EnableMFADevice", "iam:ListMFADevices"],
      "Resource": "arn:aws:iam::*:user/${aws:username}",
      "Condition": { "DateLessThan": { "aws:CurrentTime": "__DEADLINE__" } }
    }
  ]
}
```

例: 日本時間 2026-10-27 15:00 から1時間なら `2026-10-27T07:00:00Z`

{% hint style="info" %}
N Wallet を使う人が、N Wallet の QR コードで自分の MFA デバイスを登録できるようになります（画面共有で QR コードを読み取る必要がありません）。
{% endhint %}

{% hint style="warning" %}
**期限は必ず付けてください。** 登録前にアクセスキーが盗まれると、盗んだ人が先に自分の MFA デバイスを登録できてしまいます。期限は短いほど安全です（例: 1時間）。本人がすぐ登録できるタイミングで付けてください。
{% endhint %}

{% hint style="info" %}
グループには付けないでください（ユーザーごとに期限が違うため）。登録が済んだら、このポリシーは外して構いません。
{% endhint %}

**CLI で付ける場合**（上の JSON を `nwallet-mfa-registration.json` として保存しておく。期限は1時間後）

```bash
DEADLINE=$(date -u -v+1H +%Y-%m-%dT%H:%M:%SZ)   # Linux: date -u -d '+1 hour' +%Y-%m-%dT%H:%M:%SZ
sed "s/__DEADLINE__/$DEADLINE/g" nwallet-mfa-registration.json > /tmp/nwallet-mfa-registration.json
aws iam put-user-policy --user-name <ユーザー名> \
  --policy-name NWalletMfaRegistration \
  --policy-document file:///tmp/nwallet-mfa-registration.json
```

{% hint style="info" %}
**N Wallet を使う人から「MFA デバイスを登録する権限がありません。」と連絡があったとき**

* 期限切れ: 期限を延ばして付け直す（同じ名前で上書きされます）
* パス付きの IAM ユーザー（`user/部署/名前`）: 2つ目の `Resource` を、そのユーザーの ARN に書き換える
* すでに MFA デバイスがある: 2台目以降は N Wallet から登録できません。「Security credentials」→「Assign MFA device」で登録し、ARN を N Wallet を使う人に伝える
* SCP やアクセス許可の境界: 組織の管理者に確認する
{% endhint %}

{% hint style="danger" %}
新しいユーザーなのに、期限内でも上のエラーになる場合は、誰かが先に MFA デバイスを登録した（アクセスキーが盗まれた）おそれがあります。身に覚えのない MFA デバイスがあれば、アクセスキーを無効化して作り直してください。
{% endhint %}

## 5. N Wallet を使う人にアクセスキーを渡す

N Wallet を使う人に、期限内に [N Walletの初期設定](register-aws-kms-address-in-n-wallet.md)を行ってもらいます。

{% hint style="info" %}
複数人で使う場合は、一人ずつ IAM ユーザーを作るのがおすすめです（[複数人で N Wallet を使う場合](multiple-signers.md)）。
{% endhint %}
