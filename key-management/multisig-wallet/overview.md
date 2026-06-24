# マルチシグウォレットの概要

#### 1. **マルチシグウォレットとは？**

マルチシグウォレット（マルチシグネチャウォレット）とは、送金などのウォレット操作の承認に複数の署名（秘密鍵）を必要とするセキュリティ機能を備えたウォレットです。

ウォレット操作をする際に、マルチシグウォレットに予め登録しているアドレス（秘密鍵）を使って署名を行います。

ウォレット操作する際に必要な署名の数は、任意の数を設定することができます。マルチシグウォレットは、「n個のアドレス（秘密鍵）のうちm個の署名が必要」というような設定を行い、この設定情報を「n of m」と表現します。下図のマルチシグウォレットは、3つのアドレス（秘密鍵）のうち、2つの署名が必要な設定となっています。このような場合、2 of 3と表現します。

<div align="left"><figure><img src="../../.gitbook/assets/image (27).png" alt="" width="375"><figcaption></figcaption></figure></div>

#### 2. **N Suiteのマルチシグウォレット**

N Suiteのマルチシグウォレットは、一般的なマルチシグウォレットを更に拡張した設計になっています。

下図のように、マルチシグウォレットの署名用のアドレスのグループが3つ設定されています。アドレスのグループは、Signer Groupと呼び、各グループに署名用のアドレス（秘密鍵）を複数登録することができます。3つのSigner Groupのうち、2つのSigner Groupの署名が必要な設定となっています。

<div align="left"><figure><img src="../../.gitbook/assets/image (28).png" alt="" width="375"><figcaption></figcaption></figure></div>



それぞれのSigner Groupの役割は下記の通りです。

<table><thead><tr><th width="241.20001220703125" align="center">Signer  Group</th><th>　　　　　　　　　　　　　　　　　概要</th></tr></thead><tbody><tr><td align="center">User Signer Group</td><td>通常、マルチシグウォレットを使用する際に署名に使うアドレス（秘密鍵）を登録しておくグループ。</td></tr><tr><td align="center">Backup Signer Group</td><td>有事の際に、マルチシグウォレットを使用する際に署名に使うアドレス（秘密鍵）を登録しておくバックアップ用のグループ。</td></tr><tr><td align="center">N Suite Signer Group</td><td>N Suiteがお客様の代わりに管理するグループ。</td></tr></tbody></table>

N Suiteのワークフロー機能でマルチシグウォレットを使用する場合、User Signer GroupとN Suite Signer Groupに登録されているアドレス（秘密鍵）で署名を行います。

<div align="left"><figure><img src="../../.gitbook/assets/image (29).png" alt="" width="375"><figcaption></figcaption></figure></div>



なお、同じSigner Groupのアドレス（秘密鍵）2つで署名しても、マルチシグウォレットは使用できません。署名に使うアドレス（秘密鍵）は別々のSigner Groupに登録されている必要があります。

<div align="left"><figure><img src="../../.gitbook/assets/image (30).png" alt="" width="375"><figcaption></figcaption></figure></div>



#### 3. **N Suiteのマルチシグウォレットの運用**

* **Backup Signer Groupを使用するケース**

上述の通り、通常のご利用時にはUser Signer GroupとN Suite Signer Groupのアドレス（秘密鍵）を使用するため、Backup Signer Groupのアドレス（秘密鍵）は使用しません。

Backup Signer Groupのアドレス（秘密鍵）は有事の際にのみ使用します。

{% hint style="info" %}
具体的には、下記のケースが挙げられます。

&#x20;・User Signer Groupに登録した秘密鍵を全て紛失し、User Signer Groupが使えなくなった場合

&#x20;・User Signer Groupに登録した秘密鍵が盗まれて、攻撃者にUser Signer Groupのコントロールを奪われた場合
{% endhint %}

このようなケースで下記の対処を行うために、Backup Signer Groupを使用します。

* #### **User Signer GroupとBackup Signer Groupの入れ替え**

ワークフロー機能でBackup Signer Groupのアドレス（秘密鍵）で署名できるように、N Suiteの設定変更を行い、User Signer GroupとBackup Signer Groupを入れ替えます。

<div align="left"><figure><img src="../../.gitbook/assets/image (31).png" alt="" width="375"><figcaption></figcaption></figure></div>



* #### **User Signer Groupの削除と新規作成**

使用できなくなったUser Signer Groupをマルチシグウォレットから削除した後、新しいSigner Groupを作成し、マルチシグウォレットに登録します。

User Signer Groupの削除及び登録を行うためには、通常のマルチシグウォレットの使用時と同様に、署名が2つ必要になっています。そのため、Backup Signer GroupとN Suite Signer Groupのアドレス（秘密鍵）で署名を行い、User Signer Groupの削除と登録を行います。

<div align="left"><figure><img src="../../.gitbook/assets/image (32).png" alt="" width="375"><figcaption></figcaption></figure></div>



* #### **Backup Signer Groupを使用する場合の連絡先**

{% hint style="info" %}
Backup Signer Groupを使って下記の操作を行うためには、N Suiteの問い合わせ窓口にご連絡をいただく必要がございます。
\
・User Signer GroupとBackup Signer Groupの入れ替え
\
・User Signer Groupの削除と新規作成


\
これらの操作が必要な場合、下記のメールアドレスまでご連絡ください。

[contact@nsuite.io](overview.md#id-2-n-suitenomaruchishiguworetto)
{% endhint %}

#### 4. **マルチシグウォレットに登録するアドレス**

* #### **基本的な考え方**

User Signer GroupとBackup Signer Groupに登録するアドレス（秘密鍵）は、最小でそれぞれ1ずつから運用できます。

<div align="left"><figure><img src="../../.gitbook/assets/image (33).png" alt="" width="375"><figcaption></figcaption></figure></div>

一方で、User Signer GroupとBackup Signer Groupにそれぞれ複数のアドレス（秘密鍵）を登録しておくと、万が一、登録したアドレス（秘密鍵）が紛失した場合にも、UserSigner Group及びBackup Signer Groupを継続して使うことができるため、それぞれのSigner Groupに2つ以上のアドレス（秘密鍵）を登録することを推奨いたします。

万が一、User Signer GroupまたはBackup Signer Groupに登録したアドレス（秘密鍵）を紛失した場合、同じSigner Groupに登録している別のアドレス（秘密鍵）を使って、紛失したアドレス（秘密鍵）の削除と新しいアドレス（秘密鍵）の追加登録ができます。

<div align="left"><figure><img src="../../.gitbook/assets/image (34).png" alt="" width="375"><figcaption></figcaption></figure></div>



また、User Signer GroupとBackup Signer Groupに登録するアドレス（秘密鍵）は、それぞれ別の方が管理することを推奨いたします。
\
N Suiteでは、User Signer GroupとBackup Signer Groupのアドレス（秘密鍵）を使ってウォレット操作を行うインタフェースは提供しておりませんが、理論上はUser Signer GroupとBackup Signer Groupのアドレス（秘密鍵）を使ってウォレット操作が可能です。同じ人がそれぞれのSigner Groupのアドレス（秘密鍵）を保有していると、単独でウォレット操作をできてしまうため、マルチシグウォレットのメリットを活かせません。

また、複数人で結託して不正なウォレット操作をするような内部犯行の対策として、User Signer GroupとBackup Signer Groupに登録するアドレス（秘密鍵）は、別の部署の人が管理することを推奨します。別々の部署の人であれば利害関係が一致しづらく、結託が成立する可能性を下げられるからです。
\
なお、Backup Signer Groupに登録するアドレス（秘密鍵）は、ハードウェアウォレット（Ledger）で管理し、ハードウェアウォレット（Ledger）は金庫などの安全な場所に保管することを推奨いたします。
\
ハードウェアウォレット（Ledger）であればオフラインで管理できるため、サイバー攻撃のリスクを大幅に防げます。



* #### **推奨設定のまとめ**

以上をまとめると、推奨設定は下記の通りとなります。

{% hint style="info" %}
・User Signer GroupとBackup Signer Groupには2つ以上のアドレス（秘密鍵）を登録する。
\
・Backup Signer Groupにはハードウェアウォレット（Ledger）で管理し、ハードウェアウォレット（Ledger）は金庫などの安全な場所に保管する。
\
・User Signer GroupとBackup Signer Groupのアドレス（秘密鍵）は別の人（可能であれば別の部署）が管理する。
{% endhint %}

<figure><img src="../../.gitbook/assets/image (35).png" alt="" width="563"><figcaption></figcaption></figure>

## 対応ネットワーク一覧

|      ネットワーク      |  対応状況 |
| :--------------: | :---: |
|     Ethereum     | **〇** |
|      Polygon     | **〇** |
|       Oasys      | **〇** |
|     TCG Verse    | **〇** |
|    HOME Verse    | **〇** |
|      Soneium     | **〇** |
|       Astar      | **〇** |
|      Shiden      | **〇** |
|        BSC       | **〇** |
|       KAIA       | **〇** |
|     Avalanche    | **×** |
|   Arbitrum One   | **×** |
|     Optimism     | **×** |
| Japan Open Chain | **〇** |
|      Solana      | **×** |
|    zkSync Era    | **×** |

