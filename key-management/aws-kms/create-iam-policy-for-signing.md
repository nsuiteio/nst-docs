# IAMポリシーの作成：秘密鍵の署名権限を作成する手順

{% hint style="warning" %}
IAMポリシーとは？

AWS KMSでは、鍵の作成、使用、管理を行う際に、アクセス制御を行うためにIAMポリシーを使用します。IAMポリシーは、誰がどの操作を行えるかを定義し、特定のKMSキーやリソースへのアクセスを制限・許可するためのルールセットです。本記事では、IAMポリシーを作成し、秘密鍵の署名権限を定めます。
{% endhint %}

* 組織によって署名権限の付与のパターンが異なります。全社共通で同じ秘密鍵を使用するパターン（下記図）では下記Step4を参照してください。（Step5は割愛）

<figure><img src="../../.gitbook/assets/image (17).png" alt="" width="563"><figcaption></figcaption></figure>

* プロジェクトや部署毎に異なる秘密鍵を使用するパターン（下記図）ではStep5を参照してください。（Step4は割愛）

<figure><img src="../../.gitbook/assets/image (18).png" alt="" width="563"><figcaption></figcaption></figure>

## IAM ポリシーの作成

1. AWS マネジメントコンソールのIAMの画面で、「Policies」を選択し、「Create Policy」をクリック

![](<../../.gitbook/assets/Screen Shot 2021-12-02 at 22.27.15.png>)

2. 「Create Policy」で、Serviceに「KMS」を指定

![](<../../.gitbook/assets/Screen Shot 2021-12-02 at 22.28.02.png>)

3. 「Create Policy」で、Actionsを下記の画像のとおり設定

* 「List」と「Read」は全てにチェックを入れ、「Write」は「Sign」にチェックを入れる。

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

4. AWS KMSに作成した全ての秘密鍵の使用権限を付与する場合

* 「Create Policy」で、Resourcesを下記のとおり「All resources」に設定

![](<../../.gitbook/assets/Screen Shot 2021-12-02 at 22.30.25.png>)

#### 5. AWS KMSに作成した特定の秘密鍵の使用権限を付与する場合

* (下記の手順で付与したい秘密鍵のARN情報を事前にコピーしておきます。）
* KMS > Customer managed keys にアクセスし秘密鍵の一覧を表示させる。
* Alias / Key id のいずれかをクリックし詳細画面を開く。

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

* ARN 情報を四角のコピペ用のアイコンをクリックし、クリップボードにコピー

<figure><img src="../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

* 再度Policyの編集画面に戻り、Policy「Specific」を選択し、「Add ARN」をクリック

![](<../../.gitbook/assets/Screen Shot 2021-12-02 at 22.30.20.png>)

* Add ARN(s）で、Specify ARN for Keyの欄にクリップボードの情報をペーストする。

<figure><img src="../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

* 使用権限を付与したい秘密鍵のRegion / Account / Key idの項目が自動的に反映されたことを確認

#### 6. 「Next Tags」をクリック

![](<../../.gitbook/assets/Screen Shot 2021-12-02 at 22.30.25 (1).png>)

7. 「Next Review」をクリック

![](<../../.gitbook/assets/Screen Shot 2021-12-02 at 22.32.08.png>)

#### 8. 任意のpolicy名を入力し、「Create policy」をクリック

![](<../../.gitbook/assets/Screen Shot 2021-12-02 at 22.32.24.png>)

#### 9. 作成したポリシーに MFA の条件を付ける

{% hint style="danger" %}
すでに MFA なしで N Wallet を使っている場合は、先に[すでに N Wallet を使っている場合の MFA の設定](enable-mfa-for-existing-users.md)を確認してください。この手順を行うと、MFA を設定していない人は署名できなくなります。
{% endhint %}

1. 「Policies」で作成したポリシーを開き、「Edit」→「JSON」を選択
2. `"Effect": "Allow"` のステートメントに次を追加し、保存

```json
"Condition": {
  "Bool": { "aws:MultiFactorAuthPresent": "true" },
  "NumericLessThanEquals": { "aws:MultiFactorAuthAge": "3600" }
}
```

{% hint style="info" %}
アクセスキーが漏れても、MFA（認証アプリのコード）が無ければ署名できなくなります。
{% endhint %}

{% hint style="warning" %}
`aws:MultiFactorAuthAge` は **3600 以上**にしてください。N Wallet は1時間有効な認証情報で署名するため、短いと途中で署名が拒否されます。
{% endhint %}

{% hint style="info" %}
MFA を強制する Deny ポリシーを使う場合は、次を `NotAction` で除外してください。除外しないと N Wallet が MFA の認証や、QR コードでの MFA デバイスの登録を行えません。

* `sts:GetSessionToken`
* `iam:CreateVirtualMFADevice`
* `iam:EnableMFADevice`
* `iam:ListMFADevices`
{% endhint %}

#### 10. MFA なしで署名できる経路が無いか確認する

次のどれかで署名を許可していると、MFA なしでも署名できてしまいます。

* そのユーザーに付いている、ほかのポリシー
* そのユーザーが所属するグループのポリシー
* KMS の鍵ポリシー（ユーザーを直接許可していないか）

{% hint style="info" %}
N Wallet は MFA が効いているかを確かめるため、MFA なしの署名を試します（実際には署名しません）。MFA が効いていると CloudTrail に `kms:Sign` の `AccessDenied` が記録されるので、監視している場合は担当者に伝えてください。
{% endhint %}

## すでに MFA なしで N Wallet を使っている場合

[すでに N Wallet を使っている場合の MFA の設定](enable-mfa-for-existing-users.md)の順番で、手順9・10を行ってください。
