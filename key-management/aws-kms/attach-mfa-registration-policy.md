---
description: 署名する人が N Wallet の QR コードで MFA デバイスを登録できるように、アクセスキーを渡すときに期限付きの MFA 登録用ポリシーを付ける手順です。
---

# アクセスキーを渡すときに、MFA 登録用のポリシーを期限付きで付ける

{% hint style="warning" %}
本手順の対象者：\
IAMユーザーとアクセスキーを発行するAWSの管理者（インフラ担当）
{% endhint %}

署名する人は、N Wallet の画面に表示される QR コードを自分のスマホの認証アプリで読み取って、MFA デバイスを登録できます（インフラ担当と署名する人が、画面共有で QR コードを読み取る必要はありません）。

そのためには、その IAM ユーザーに MFA デバイスを登録する権限が必要です。**この権限は、アクセスキーを発行して渡すときに、そのユーザーにだけ、期限付きで付けてください**。期限の長さは運用に合わせて決めます（例: 1時間）。

{% hint style="info" %}
**期限を付ける理由**

MFA デバイスをまだ登録していないユーザーに、この権限を期限なしで付けたとします。本人が登録を忘れている間にアクセスキーが盗まれると、盗んだ人が先に自分の MFA デバイスを1台目として登録し、MFA 付きで署名できてしまいます。

MFA デバイスを登録済みのユーザーには、AWS がアクセスキーだけでの追加の MFA デバイスの有効化を認めません（"An IAM user must authenticate with an existing MFA device to enable or disable an additional MFA device."）。そのため、危険があるのは登録が済むまでの間だけです。その間を期限で閉じます。
{% endhint %}

{% hint style="info" %}
**グループには付けないでください**

期限は `aws:CurrentTime` の日時で書くしかなく（日時の条件演算子にはポリシー変数を使えません）、ユーザーごとに期限が違うためです。
{% endhint %}

期限は短いほど安全です。**本人がすぐに N Wallet で登録できるタイミングで付けてください**（アクセスキーを渡すときに、本人と時間を合わせます）。

## 付けるポリシー

`__DEADLINE__` の2か所を期限の日時に置き換えます。日時は **UTC** で書きます（日本時間から9時間引きます）。

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

例: 日本時間 2026-10-27 15:00 に付けて、1時間後を期限にする場合は、`__DEADLINE__` を `2026-10-27T07:00:00Z` にします。

以下、AWS コンソールの表示名は日本語表示のものです（括弧内は英語表示）。

## 0. 対象の IAM ユーザーを確かめる

N Wallet のアクセスキーが、どの IAM ユーザーのものかを確かめます。

* N Wallet の「N Cloud Key 管理」に、アクセスキー ID の先頭と末尾（例: `AKIAEX...XAMPLE`）が表示されます。**IAM** →「ユーザー」でユーザーを開き、「セキュリティ認証情報」(Security credentials) タブの「アクセスキー」と見比べてください。
* AWS CLI が使える場合は、`aws iam get-access-key-last-used --access-key-id <アクセスキーID>` の結果の `UserName` がそのユーザーです。

## 1. AWS コンソールで付ける

1. IAM のポリシーを編集できる権限で AWS コンソールにサインインし、上部の検索窓から **IAM** を開く
2. 「ユーザー」(Users) → 手順0のユーザー名をクリック
3. 「**許可**」(Permissions) タブ →「**許可を追加**」(Add permissions) →「**インラインポリシーを作成**」(Create inline policy) をクリック
4. ポリシーエディタの右上で「**JSON**」に切り替え、最初から入っている内容をすべて消して、上の JSON を貼り付ける
5. `__DEADLINE__` の2か所を期限の日時（UTC）に書き換える
6. エラーや警告が無いことを確かめて「次へ」(Next) をクリック
7. ポリシー名に `NWalletMfaRegistration` を入力し、「**ポリシーの作成**」(Create policy) をクリック
8. ユーザーの「許可」タブの一覧に、そのポリシーが「インライン」として表示されていれば完了です

## 2. AWS CLI で付ける（期限を自動で入れる）

上の JSON を `nwallet-mfa-registration.json` という名前で保存しておき、アクセスキーを渡すときに次のコマンドを実行します。

```bash
# 期限 = 今から1時間後（UTC）の例。期間は運用に合わせて変えてください。
# macOS の date の書き方です。Linux では date -u -d '+1 hour' +%Y-%m-%dT%H:%M:%SZ
DEADLINE=$(date -u -v+1H +%Y-%m-%dT%H:%M:%SZ)
sed "s/__DEADLINE__/$DEADLINE/g" nwallet-mfa-registration.json > /tmp/nwallet-mfa-registration.json
aws iam put-user-policy --user-name <ユーザー名> \
  --policy-name NWalletMfaRegistration \
  --policy-document file:///tmp/nwallet-mfa-registration.json
echo "期限: $DEADLINE"
```

同じポリシー名で実行し直すと上書きされます。期限を延ばすときも、同じコマンドを実行してください。

## 3. 効いているか確かめる

1. **IAM** →「ユーザー」→ 対象のユーザー →「許可」タブに、付けたポリシーが表示されていることを確認する
2. 確実に確かめる場合は、**IAM ポリシーシミュレーター**（[https://policysim.aws.amazon.com/](https://policysim.aws.amazon.com/)）を使う
   * 左でそのユーザーを選ぶ
   * サービスで「IAM」を選び、`CreateVirtualMFADevice` と `EnableMFADevice` にチェックを入れる
   * リソースを入力する（空のままだとリソースが `*` 扱いになり、ポリシーの `Resource` に一致せず「暗黙的な拒否」になります）
     * `CreateVirtualMFADevice`: `arn:aws:iam::<アカウントID>:mfa/<任意の名前>`（例: `mfa/nwallet-test`）
     * `EnableMFADevice`: `arn:aws:iam::<アカウントID>:user/<ユーザー名>`
   * 「シミュレーションを実行」をクリックする
   * 期限内なら、両方が「許可」(allowed) になります（期限を過ぎていれば「暗黙的な拒否」になります）
3. 署名する人が N Wallet で QR コードを作成し、QR コードが表示されれば成功です（[N Walletの初期設定](register-aws-kms-address-in-n-wallet.md)、または[MFA 設定](n-wallet-mfa-settings.md)）。権限が足りない場合は、N Wallet に「MFA デバイスを登録する権限がありません。」と表示されます。

## うまくいかないとき

* **期限切れ**: N Wallet に「MFA デバイスを登録する権限がありません。」と表示されます。期限を延ばして付け直してください（手順1でポリシーの日時を書き換えるか、手順2のコマンドを実行し直します）。
* **パス付きの IAM ユーザー**（ARN が `arn:aws:iam::123456789012:user/部署/名前` の形）には、`${aws:username}` が一致しません。2つ目の `Resource` を、そのユーザーの ARN そのもの（ユーザーの画面の上部に表示されています）に書き換えてください。
* **ポリシーシミュレーターでは「許可」なのに N Wallet で拒否される**場合は、AWS Organizations の SCP や「アクセス許可の境界」(Permissions boundary) が IAM の操作を止めている可能性があります。組織の管理者に確認してください。
* **2台目以降**（そのユーザーに MFA デバイスがすでにある）は、このポリシーがあっても N Wallet からは登録できません。IAM コンソールのユーザーの「セキュリティ認証情報」→「MFA デバイスの割り当て」で登録し、署名する人に MFA デバイスの ARN を伝えてください（N Wallet では「ARN を入力」で設定します）。

## 登録が済んだら

* 本人の MFA デバイスの登録が済んだら、`NWalletMfaRegistration` を外して構いません（期限を過ぎれば効かなくなるので、付いたままでも問題はありません）。
* MFA デバイスの登録が済んだら、[KMS の署名に MFA を必須にする](require-mfa-for-kms-signing.md)に進んでください。

{% hint style="danger" %}
**新しいユーザーで、期限内なのに QR コードでの登録が「MFA デバイスを登録する権限がありません。」で拒否された場合**は、すでに誰かが MFA デバイスを登録した（アクセスキーが盗まれた）可能性があります。IAM コンソールでそのユーザーの MFA デバイスを確かめ、身に覚えが無ければアクセスキーを無効化して作り直してください。
{% endhint %}
