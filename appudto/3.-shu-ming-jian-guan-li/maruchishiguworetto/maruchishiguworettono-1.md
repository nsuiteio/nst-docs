# マルチシグウォレット：初期設定の手順

{% hint style="info" %}
　N Suiteでマルチシグウォレットが利用可能になるまでのフローを記載しています。
{% endhint %}

#### 1. マルチシグウォレットを登録する[チームを作成する](/broken/pages/WVIjDxukqMCpibbly0Cw)

#### 2. マルチシグウォレットの署名に使うアドレス(User Signer Group用 + Backup Signer Group用)を作成する

&#x20; [AWS KMSの秘密鍵](/broken/pages/ktWEcshTm4zD7HC2xUDl)または[ハードウェアウォレット](/broken/pages/kN9OyzG4cHkrm207HdbC)が必要になります。

#### 3.  ↑で作成したアドレスを[チームへ追加](/broken/pages/F1a6yQSaW4c7SU6FH5IE)する

※マルチシグウォレットを登録するチームと同一のチームへアドレスを登録していることを確認ください

#### 4. マルチシグ[初期設定シートをダウンロード](https://drive.google.com/file/d/1FBnVgTpbsij50ZIXvvD_I4vsXeAQauG-/view?usp=sharing)し必要事項を記入する

&#x20; User Signer Groupに登録するアドレス、Backup Signer Groupに登録するアドレスは無制限に指定できますので、その場合はそれぞれ行数を増やしてご提出ください。

{% hint style="warning" %}
Backup Signer Groupに含めるアドレスはセキュリティ強度の観点から、[ハードウェアウォレット](https://www.ledger.com/)か、別のAWS KMSアカウントで管理しているアドレスを登録する事を推奨します。
{% endhint %}

#### 5. 記入が終わったら保存し、シートをN Suite運営チームに送信

&#x20; 基本的に[contact@nsuite.io](mailto:contact@nsuite.io)宛てにEメールの添付ファイルにてお願いいたします

#### 6. N Suiteチームより設定完了の報告 + マルチシグウォレットのアドレスをご連絡

&#x20; 通常1～2営業日でアドレスをお渡しできます。

#### 7. 利用開始🎉
