# AWS KMSの秘密鍵作成手順 （macOS向け）

## 1. AWS CLIのインストール

① macOS pkg ファイルをダウンロード

[https://awscli.amazonaws.com/AWSCLIV2.pkg](https://awscli.amazonaws.com/AWSCLIV2.pkg)

② ダウンロードしたファイルをダブルクリックして、インストーラを起動

③ 画面の指示に従って、AWS CLIをインストール

## 2. AWS CLI操作用のAWSユーザー作成

{% hint style="info" %}
本手順は、AWS マネジメントコンソールで操作します。
{% endhint %}

① AWS マネジメントコンソールのIAMの画面で、「Users」を選択し、「Add users」をクリック

![](<../../.gitbook/assets/Screen Shot 2022-06-02 at 21.47.37.png>)

② 「User name」に任意の名前を入力し、「Select AWS credential type」の「Access key - Programmatic access」にチェックを入れ、「Next: Permissions」をクリック

![](<../../.gitbook/assets/Screen Shot 2022-06-02 at 21.48.24.png>)

③ 「Attach existing policies directly」を選択し、`AWSKeyManagementServicePowerUser`という名前ポリシーにチェックを入れ、「Next: Tags」をクリック

![](<../../.gitbook/assets/Screen Shot 2022-06-02 at 21.48.58.png>)

④ 「Next: Review」をクリック

![](<../../.gitbook/assets/Screen Shot 2022-06-02 at 21.49.28.png>)

⑤「Create user」をクリック

![](<../../.gitbook/assets/Screen Shot 2022-06-02 at 21.49.44.png>)

⑥ 作成したIAM ユーザーの`Access Key ID` と `Secret access key` が表示されるため、メモを控える

{% hint style="warning" %}
この画面を閉じると `Secret access key` は二度と確認できなくなるため、忘れずに情報を控えてください
{% endhint %}

![](<../../.gitbook/assets/Screen Shot 2022-06-02 at 21.49.50.png>)



## 3. AWS CLIの設定

① AWS CLIの認証用の設定ファイル作成

ターミナルで下記のコマンドを実行。（実行するとAWS CLIの認証用の設定ファイルが作成されます。）

```bash
aws configure
```

{% hint style="warning" %}
コマンド実行時に設定する値は下記の通りです。

`・AWS Access Key ID：`手順「**2. AWS CLI操作用のAWSユーザー作成**」にて控えたもの

`・AWS Secret Access Key：`手順「**2. AWS CLI操作用のAWSユーザー作成**」にて控えたもの

・Default region name：任意のregionで問題ないが、特に指定がない場合は「ap-northeast-1」を設定※

・Default output format：未入力で問題なし
{% endhint %}

{% hint style="warning" %}
※**AWS KMS管理コンソールとregion設定が一致している事をご確認ください**！

管理コンソール右上のプルダウンメニューで確認できます。

![](<../../.gitbook/assets/image (6).png>)
{% endhint %}

② AWS CLIの認証用ファイルの適用

ターミナルで下記コマンドを実行。（実行すると、上記①で作成した認証用ファイルがAWS CLIに反映されます。）

```bash
export AWS_REGION=YOUR_REGION
export AWS_PROFILE=YOUR_PROFILE
```

ex.) YOUR\_REGION: ap-northeast-1

ex.) YOUR\_PROFILE: default



## 4. nsuite-kmscliのダウンロードと設定

① nsuite-kmscliのGithubリポジトリにアクセス

[https://github.com/doublejumptokyo/nsuite-kmscli](https://github.com/doublejumptokyo/nsuite-kmscli)

② 最新のリリースバージョンをクリック

<figure><img src="../../.gitbook/assets/スクリーンショット 2024-03-19 18.11.02.png" alt=""><figcaption></figcaption></figure>

③ 「nsuite-kmscli-macOS.tar.gz」をクリックし、実行ファイルをダウンロード

<figure><img src="../../.gitbook/assets/スクリーンショット 2024-03-19 18.09.55.png" alt=""><figcaption></figcaption></figure>

③ ダウンロードしたnsuite-kmscliの実行ファイルを任意のディレクトリに格納

ダウンロードした、「nsuite-kmscli-macOS.tar.gz」を解凍し、ファイル「nsuite-kmscli」を任意のディレクトリに格納

④ ファイルへの権限付与\
ターミナルで、「nsuite-kmscli」を格納したディレクトリに移動し、下記のコマンドを実行

```
chmod 777 nsuite-kmscli
```

## 5. 秘密鍵の作成

```
既にN Suiteを使っていて、秘密鍵を追加作成されたいカスタマーは、こちらのステップから始めてください。
```

①ターミナルを開く。

* Finderから「アプリケーション > ユーティリティ > ターミナル」を開きます。または、Spotlight検索で「ターミナル」と入力し、ターミナルを選択します。

②「nsuite-kmscli」が格納されているディレクトリに移動

* ターミナルが開いたら、以下のコマンドを入力して「nsuite-kmscli」が格納さているフォルダに移動します。
* 例）「ダウンロード」フォルダに格納されている場合：

```
cd ~/Downloads
```

* このコマンドで、ユーザーのホームフォルダの中にある「Downloads」フォルダに移動します。

③「nsuite-kmscli」を確認

* `ls`コマンドを使ってフォルダ内のファイルを確認します。
* 「nsuite-kmscli」というファイルがリストに表示されれば、そのフォルダに正しく移動できています。

④秘密鍵の作成

* 下記のコマンドを実行（コマンドが正常に実行されるとAWS KMSに秘密鍵が作成されます。）

```
./nsuite-kmscli new
```

⑤ファイルの認証

* コマンドを実行して、下記のポップアップが表示された場合は「キャンセル」をクリックして「ファイルの認証手順」を行った後、コマンドを再実行してください。

![](<../../.gitbook/assets/Screen Shot 2022-03-11 at 16.43.08.png>)\
**ファイルの認証手順**

1. Finderで右クリックし、表示されるメニューから「開く」をクリック

![](<../../.gitbook/assets/Screen Shot 2022-03-11 at 16.44.07.png>)

&#x20;2\. 表示されるポップアップで「開く」をクリック

![](<../../.gitbook/assets/Screen Shot 2022-03-11 at 16.44.15.png>)\
\
⑥ 作成した秘密鍵の確認

* 下記のコマンドを実行すると、AWS KMSに作成した秘密鍵に対応するアドレスが一覧で表示され、秘密鍵が作成されたことを確認できます。（秘密鍵自体は表示されません。）

```bash
./nsuite-kmscli list
```

