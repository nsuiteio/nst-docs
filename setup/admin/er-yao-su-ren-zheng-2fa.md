# 二要素認証(2FA)

## 二要素認証とは？

通常のパスワード認証に加えて、ワンタイムパスワードによる認証を設定することで、セキュリティを強化できる機能です。N Suiteにおいては、N Boardへのログインの際にGoogle Authenticatorを使用することをユーザーに強制する方式を採用しております。

Google Authenticator のインストールはこちら:  [ iOS ](https://apps.apple.com/app/google-authenticator/id388497605) / [ Android](https://play.google.com/store/apps/details?id=com.google.android.apps.authenticator2)



## 自分のアカウントのみ2FAを有効にする

右上のアイコン①から自分のユーザー設定②を表示させ、左側のタブで「セキュリティ」③を選択します。次にGoogle Authenticatorの有効ボタン④をクリックし、有効化を完了させます。

<div align="left"><figure><img src="../../.gitbook/assets/image (90).png" alt="" width="375"><figcaption></figcaption></figure></div>

認証アプリの設定画面に遷移しますので、QRコードをiOS / AndroidデバイスのGoogle Authenticatorでスキャン →「ワンタイムコードの入力」に表示されたコードを入力後 →「続ける」をクリックし、初期設定を完了させます。次回以降のログインの際にワンタイムパスワードの入力を要求させるようになります。

<div align="left"><figure><img src="../../.gitbook/assets/image (91).png" alt="" width="146"><figcaption><p>認証アプリの設定画面</p></figcaption></figure></div>

## 組織のユーザー全員に2FAの有効化を強制する

オーナーもしくは管理者権限でN Boardにログインし、組織の設定①→②を開きます。「セキュリティ」の下に「すべてのユーザーに二要素認証を強制する」というチェックボックス③がありますので、こちらを有効にすることによってユーザーが二要素認証の有効化をしないとログインできない状態に切り替わります。

<div align="left"><figure><img src="../../.gitbook/assets/image (92).png" alt="" width="273"><figcaption></figcaption></figure></div>

## 2FAの初期設定画面（管理者から強制された場合）

管理者から2FAの有効化を強制された場合、ユーザー側はN Boardにアクセスしようとすると下記の画面が表示され、2FAの初期設定を済ませないとログインできなくなります。「二要素認証を有効化」を押すと上記の「自分のアカウントのみ2FAを有効にする」の欄で記載したユーザー設定画面に遷移しますので、同じ手順で自分の2FA有効化→初期設定を完了させます。

<div align="left"><figure><img src="../../.gitbook/assets/image (93).png" alt="" width="301"><figcaption></figcaption></figure></div>
