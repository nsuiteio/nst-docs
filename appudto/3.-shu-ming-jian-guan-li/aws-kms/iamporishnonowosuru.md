# IAMポリシーの作成：秘密鍵の署名権限を作成する手順

{% hint style="warning" %}
IAMポリシーとは？

AWS KMSでは、鍵の作成、使用、管理を行う際に、アクセス制御を行うためにIAMポリシーを使用します。IAMポリシーは、誰がどの操作を行えるかを定義し、特定のKMSキーやリソースへのアクセスを制限・許可するためのルールセットです。本記事では、IAMポリシーを作成し、秘密鍵の署名権限を定めます。
{% endhint %}

* 組織によって署名権限の付与のパターンが異なります。全社共通で同じ秘密鍵を使用するパターン（下記図）では下記Step4を参照してください。（Step5は割愛）

<figure><img src="../../../.gitbook/assets/image (17).png" alt="" width="563"><figcaption></figcaption></figure>

* プロジェクトや部署毎に異なる秘密鍵を使用するパターン（下記図）ではStep5を参照してください。（Step4は割愛）

<figure><img src="../../../.gitbook/assets/image (18).png" alt="" width="563"><figcaption></figcaption></figure>

## IAM ポリシーの作成

1. AWS マネジメントコンソールのIAMの画面で、「Policies」を選択し、「Create Policy」をクリック

![](<../../../.gitbook/assets/Screen Shot 2021-12-02 at 22.27.15.png>)

2. 「Create Policy」で、Serviceに「KMS」を指定

![](<../../../.gitbook/assets/Screen Shot 2021-12-02 at 22.28.02.png>)

3. 「Create Policy」で、Actionsを下記の画像のとおり設定

* 「List」と「Read」は全てにチェックを入れ、「Write」は「Sign」にチェックを入れる。

<figure><img src="../../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

4. AWS KMSに作成した全ての秘密鍵の使用権限を付与する場合

* 「Create Policy」で、Resourcesを下記のとおり「All resources」に設定

![](<../../../.gitbook/assets/Screen Shot 2021-12-02 at 22.30.25.png>)

#### 5. AWS KMSに作成した特定の秘密鍵の使用権限を付与する場合

* (下記の手順で付与したい秘密鍵のARN情報を事前にコピーしておきます。）
* KMS > Customer managed keys にアクセスし秘密鍵の一覧を表示させる。
* Alias / Key id のいずれかをクリックし詳細画面を開く。

<figure><img src="../../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

* ARN 情報を四角のコピペ用のアイコンをクリックし、クリップボードにコピー

<figure><img src="../../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

* 再度Policyの編集画面に戻り、Policy「Specific」を選択し、「Add ARN」をクリック

![](<../../../.gitbook/assets/Screen Shot 2021-12-02 at 22.30.20.png>)

* Add ARN(s）で、Specify ARN for Keyの欄にクリップボードの情報をペーストする。

<figure><img src="../../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

* 使用権限を付与したい秘密鍵のRegion / Account / Key idの項目が自動的に反映されたことを確認

#### 6. 「Next Tags」をクリック

![](<../../../.gitbook/assets/Screen Shot 2021-12-02 at 22.30.25 (1).png>)

7. 「Next Review」をクリック

![](<../../../.gitbook/assets/Screen Shot 2021-12-02 at 22.32.08.png>)

#### 8. 任意のpolicy名を入力し、「Create policy」をクリック

![](<../../../.gitbook/assets/Screen Shot 2021-12-02 at 22.32.24.png>)

