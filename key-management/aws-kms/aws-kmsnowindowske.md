# AWS KMSの秘密鍵作成手順（Windows向け）

{% hint style="warning" %}
こちらの手順ではWindowsの[コマンドプロンプト](https://www.modis.co.jp/candidate/insight/column_28)を使用します。予め使用方法について、ご確認ください。
{% endhint %}

## 1. AWS CLIのインストール

① AWSCLIV2.msi ファイルをダウンロード

[https://awscli.amazonaws.com/AWSCLIV2.msi](https://awscli.amazonaws.com/AWSCLIV2.msi)

② ダウンロードしたファイルをダブルクリックして、インストーラを起動

③ 画面の指示に従って、AWS CLIをインストール

## 2. AWS CLI操作用のAWSユーザー作成

① AWS マネジメントコンソールのIAMの画面で、「Users」を選択し、「Add users」をクリック

![](<../../.gitbook/assets/Screen Shot 2022-06-02 at 21.47.37 (1).png>)

② 「User name」に任意の名前を入力し、「Next」をクリック

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

③ 「Attach policies directly」を選択し、`AWSKeyManagementServicePowerUser`という名前ポリシーにチェックを入れ、「Next」をクリック

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption><p>"power"で検索すると該当ポリシーが見つけやすいです</p></figcaption></figure>

④「Create user」をクリック

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

⑤ IAMユーザーの一覧に画面が遷移するので、作成したIAM ユーザーを開く。

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

⑥ Security credentials をクリック

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

⑦ 下にスクロールし、Access keys内のCreate access keyをクリック

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

⑧ Application running outside AWSを選択し「Next」をクリック

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

⑨「Create access key」をクリック

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

⑩Access key createdと表示されれば成功です。次のステップで使用しますので、Access key / Secret access keyをセキュアな環境に控えて下さい。

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
この画面を閉じると、`Secret Access Key`　は二度と確認できなくなります。画面を閉じる前に、必ず情報を控えてください。
{% endhint %}

## 3. AWS CLIの設定

① AWS CLIの認証用の設定ファイル作成

[コマンドプロンプト](https://www.modis.co.jp/candidate/insight/column_28)で下記のコマンドを実行。（実行するとAWS CLIの認証用の設定ファイルが作成されます。）

```bash
aws configure
```

{% hint style="warning" %}
コマンド実行時に設定する値は以下の通りです。

`・AWS Access Key ID：`手順「**2. AWS CLI操作用のAWSユーザー作成**」にて控えたもの

`・AWS Secret Access Key：`手順「**2. AWS CLI操作用のAWSユーザー作成**」にて控えたもの

・Default region name：任意のregionで問題ないが、特に指定がない場合は「ap-northeast-1」を設定※

・Default output format：未入力で問題なし
{% endhint %}

{% hint style="warning" %}
※**AWS KMS管理コンソールとregion設定が一致していることをご確認ください**！

管理コンソール右上のプルダウンメニューで確認できます。

![](<../../.gitbook/assets/image (16).png>)
{% endhint %}

② 「システムのプロパティ」を開き、環境変数をクリック

![](<../../.gitbook/assets/スクリーンショット 2021-12-10 215042.png>)

③ AWS CLIの認証用ファイルの適用

下記の環境変数を設定。（設定すると、上記①で作成した認証用ファイルがAWS CLIに反映されます。）新規(W)...をクリックし、下記値を手動で入力します：

* 変数 = AWS\_REGION / 値(例) = ap-northeast-1
* 変数 = AWS\_PROFILE / 値 = default

![](<../../.gitbook/assets/スクリーンショット 2021-12-10 215116.png>)

## 4. nsuite-kmscliのダウンロード

① nsuite-kmscliのGithubリポジトリにアクセス

[https://github.com/doublejumptokyo/nsuite-kmscli](https://github.com/doublejumptokyo/nsuite-kmscli)

② 最新のリリースバージョンをクリック

<figure><img src="../../.gitbook/assets/スクリーンショット 2024-03-19 18.11.02 (1).png" alt=""><figcaption></figcaption></figure>

③ 「nsuite-kmscli-Windows.tar.gz」をクリックし、実行ファイルをダウンロード

<figure><img src="../../.gitbook/assets/スクリーンショット 2024-03-19 18.09.55 2.png" alt=""><figcaption></figcaption></figure>

④ nsuite-kmscliの実行ファイルを任意のディレクトリに格納

ダウンロードした、「nsuite-kmscli-Windows.tar.gz」を解凍し、ファイル「nsuite-kmscli.exe」を任意のディレクトリに格納

## 5. 秘密鍵の作成

① 秘密鍵の作成コマンド実行

コマンドプロンプトで、「nsuite-kmscli.exe」を格納したディレクトリに移動し、下記のコマンドを実行（コマンドが正常に実行されるとAWS KMSに秘密鍵が作成されます。）

```bash
nsuite-kmscli.exe new
```

② 作成した秘密鍵の確認

下記のコマンドを実行すると、AWS KMSに作成した秘密鍵に対応するアドレスが一覧で表示され、秘密鍵が作成されたことを確認できます。（秘密鍵自体は表示されません。）

```bash
nsuite-kmscli.exe list
```



