# IAMユーザーの作成：秘密鍵の署名権限ユーザーを作成する手順

{% hint style="warning" %}
IAMユーザーとは？\
IAMユーザーとは、AWS KMSで作成した秘密鍵にアクセスするために作成される個別のエンティティです。IAMユーザーには、特定のユーザーに関連する認証情報（Access Key ID とSecret Access Key）が割り当てられ、AWS KMSで作成した秘密鍵にアクセスすることが可能です。
{% endhint %}

{% hint style="info" %}
署名実行権限を持つユーザーがAWS KMSで作成した秘密鍵をN Walletで使うには、まず該当するユーザーのIAMユーザーを作成し、次に前回作成したIAMポリシーに紐付け、最後に認証情報としてのAccess Key IDとAecret Access Keyを発行する必要があります。本記事では、その方法を説明します。
{% endhint %}

## 1. IAM ユーザーを作成する

* 「Add users」をクリック

![](<../../../.gitbook/assets/Screen Shot 2021-12-10 at 18.45.03.png>)

* 「User name」に任意の名前を入力し、「Next」をクリック

<figure><img src="../../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

## 2. IAM ユーザーをIAM ポリシーに紐づける

* 「Attach existing policies directly」を選択し、「IAM ポリシーの作成」で作成したIAM ポリシーにチェックを入れ、「Next」をクリック

<figure><img src="../../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

* 「Create user」をクリック (Tagは任意)

<figure><img src="../../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

## 3. IAMユーザーに対する認証情報を発行する

* IAMユーザーの一覧に画面が遷移するので、作成したIAM ユーザーを開く

<figure><img src="../../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

* Security credentials をクリック

<figure><img src="../../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

* 下にスクロールし、Access keys内のCreate access keyをクリック

<figure><img src="../../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

* Application running outside AWSを選択し「Next」をクリック

<figure><img src="../../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

* Create access keyをクリック

<figure><img src="../../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

* Access key createdと表示されれば成功です。次章のN Walletの初期設定で使用しますので、Access key / Secret access keyをセキュアな環境に控えて下さい。

<figure><img src="../../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

{% hint style="danger" %}
※ この画面を閉じると `Secret access key` は二度と確認できなくなるため、忘れずに情報を控えてください
{% endhint %}
