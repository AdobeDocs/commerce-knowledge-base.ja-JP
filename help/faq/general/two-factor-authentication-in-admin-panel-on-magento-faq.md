---
title: Adobe Commerceの管理パネルでの 2 要素認証に関するよくある質問
description: 1. **管理パネルの二要素認証とは 変更点？** 2 要素認証（2FA）は、ID を検証するための追加のセキュリティレイヤーであり、パスワードを知っている人がいる場合でも、管理者アカウントにのみアクセスできるようにします。 Adobeは、2.3.0 のCommerce管理パネルで 2FA のサポートを追加して、管理者アカウントを不正アクセスから保護しました。 2.4.0 では、2FA は管理パネルでデフォルトで有効になっており、UI または web API を使用して管理にログインする前に設定する必要があります。 Adobeでは、2FA モジュールを無効にすることを強くお勧めします。
exl-id: 77b57c11-fcde-4bc6-814e-45fa990cc491
feature: Admin Workspace, Best Practices
source-git-commit: f11c8944b83e294b61d9547aefc9203af344041d
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 0%

---

# Adobe Commerceの管理パネルでの 2 要素認証に関するよくある質問

1. **管理パネルの二要素認証とは 変更点** 2 要素認証（2FA）は、ID を検証するための追加のセキュリティレイヤーです。パスワードを知っている人がいる場合でも、管理者アカウントにのみアクセスできるようにするためのものです。 Adobeは、2.3.0 のCommerce管理パネルで 2FA のサポートを追加して、管理者アカウントを不正アクセスから保護しました。 2.4.0 では、2FA は管理パネルでデフォルトで有効になっており、UI または web API を使用して管理にログインする前に設定する必要があります。 Adobeでは、2FA モジュールを無効にすることを強くお勧めします。
1. **2.4.0 で 2FA がデフォルトで有効になっていたのはなぜですか。** 2FA を通じて追加の認証レイヤーを提供することは、管理ポータルのセキュリティを高めるために追加の認証レイヤーを提供するデフォルトのセキュア設定です。これにより、攻撃をスキミングするための攻撃サーフェスが減少し、セキュリティインシデントの潜在的なリスクが減少します。
1. **この 2FA 設定を 2.4.0 で無効にできますか？** このセキュリティのベストプラクティスと、二要素認証による追加の保護レイヤーを無効にしないことを強くお勧めします。
1. **2FA はどのバージョンでサポートされていますか。** 2FA のサポートは 2.3.0 で追加されましたが、2.4.0 ではデフォルトで有効になっています。
1. **2.3 で 2FA を有効にするにはどうすればよいですか？** Adobe Commerce 2.3 で 2FA を有効にする手順については、次を参照してください。 [2FA のインストール](https://devdocs.magento.com/guides/v2.3/security/two-factor-authentication.html#install-2fa) 開発者向けドキュメントを参照してください。
1. **IP やネットワークに関係なく、管理者向けの 2FA は必要ですか？** 2.4.0 では、2FA はデフォルトで有効になっており、IP やネットワークに関係なく必須です。 これは、セキュリティのベストプラクティスであり、すべてのお客様に従うことをお勧めします。 2FA の詳細については、こちらを参照してください。 [二要素認証](https://devdocs.magento.com/guides/v2.4/security/two-factor-authentication.html) 開発者向けドキュメントを参照してください。
1. **スマートフォンを所有していない場合、2FA を有効にするにはどうすればよいですか？** 管理パネルの 2FA は、次のオーセンティケーターをサポートしています：Google オーセンティケーター、Authy、U2F キーと Duo セキュリティ。 スマートフォンを所有していない管理者ユーザーは、U2F キーを使用するか、Google Authenticator などの認証者向けのブラウザー拡張機能を使用できます。
1. **Adobe Commerceで少数のユーザーに対して 2FA をアクティブ化することはできますか。それとも、ログイン時に 2FA を使用する必要がありますか。** Adobe Commerceでは、すべての管理者ユーザーに、管理者アカウントにログインする際に 2FA を有効にすることをお勧めします。 Adobe Commerce 2.4 以降で実行されている web ストアの場合、デフォルトでは、すべてのユーザーに対して 2FA が有効になっています。
1. **管理パネルで 2FA を設定する際の想定される動作は何ですか。設定中に受信したメールからのリンクを使用して、既にログインしてリクエストした 2FA 設定とは別のブラウザーを使用できますか？** ユーザーは、ログインしているかどうかに関係なく、任意のブラウザーでメールリンクを開くことができます。 セキュリティ上の理由から、このプロセス中に開くことのできるセッションは 1 つのみであり、ブラウザーを切り替えた場合は再認証が必要になります。 2FA の利点は、ユーザーに 2 つの異なる方法を使用して ID を検証させることです。 この設定シナリオでは、ユーザーのメールへのアクセスは 1 つの方法に過ぎず、別の方法を指定する必要があります。 プロセスのその時点では、2 番目のオプションとしてパスワードのみが存在します。 したがって、ユーザーがメールリンク自体を使用してログインすることはできません。ブラウザーを切り替えた場合や、まだログインしていない場合は、続行する前にパスワードの入力が求められます。
1. **2FA 設定では、個々のユーザーが自分の個人用 2FA を設定できるように、ACL 設定を変更し、管理者以外のユーザーに 2FA 管理設定を変更するためのアクセス権を付与する必要がありますか？** 2 つの「2 要素認証」があります [ACL](https://devdocs.magento.com/guides/v2.4/ext-best-practices/tutorials/create-access-control-list-rule.html) インターフェイスのリソース。 1 つは、グローバル設定（**ストア** > 設定 > **設定** > **セキュリティ** > **2FA**）以外の数字は、ユーザーが自分の個人用 2FA を使用できるようにします（**システム** > **権限** > **2FA**）に設定します。 グローバル設定は、管理者タイプのユーザーがシステムを設定するためのもので、管理者以外のユーザーは、2 番目のタイプの ACL でログインして独自の 2FA 設定を行う必要があります。 グローバル設定を許可する ACL は、設定に対する権限を持つ管理者がグローバル設定を指定することを許可するので、個々のユーザーが設定を変更する必要はありません。 ユーザーは、ログインして「アクセスが拒否されました」画面が表示されたら、https://にアクセスできます``<magento store>``/&lt;admin _path=&quot;&quot;>/tfa/tfa/requestconfig/：個人設定にアクセスします。 これは2.4.1/2.3.6/2.4.0-p1（セキュリティパッケージ 1.1.0）の既知の問題で、2.4.2/2.3.7/2.4.1-p1（セキュリティパッケージ 1.1.1）で解決されます。
