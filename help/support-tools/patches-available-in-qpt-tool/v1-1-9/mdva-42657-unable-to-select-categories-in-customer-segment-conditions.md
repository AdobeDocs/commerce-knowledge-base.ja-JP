---
title: 「MDVA-42657：顧客セグメント条件でカテゴリを選択できない」
description: MDVA-42657 パッチは、管理者ユーザーが顧客セグメント条件でカテゴリを選択できない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.9 がインストールされている場合に利用できます。 パッチ ID は MDVA-42657。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: 9c810dcd-b39b-4456-a362-5452ada4dc53
feature: Categories, Console, Customer Service
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# MDVA-42657：顧客セグメント条件でカテゴリを選択できない

MDVA-42657 パッチは、管理者ユーザーが顧客セグメント条件でカテゴリを選択できない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.9 がインストールされている場合に使用できます。 パッチ ID は MDVA-42657。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.1 ～ 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

管理者ユーザーが顧客セグメント条件でカテゴリを選択できません。

<u> 再現手順 </u>:

1. **顧客**/**セグメント** に移動します。
1. 新しいセグメントを作成します。
1. 新しく作成されたセグメントに移動し、左側のナビゲーションで **条件** をクリックします。
1. 緑色のプラス記号をクリックします。
1. 「製品」の下の「製品履歴」を選択します。
1. 「表示済み」を「注文済み」に変更します。
1. 「すべて」を「すべて」に変更します。
1. ネストされた緑のプラス記号をクリックし、「カテゴリ」を選択します。
1. 「**...**」記号をクリックし、選択アイコン（チェックマークの左側）をクリックします。
1. ブラウザーの開発コンソールを開きます。
1. 任意または複数のカテゴリのチェックボックスをオンにし、コンソールに Javascript エラーがスローされることに注意してください。
1. 「**保存** ボタンをクリックします。
1. 条件に戻り、選択したカテゴリが保存されているかどうかを確認します。

<u> 期待される結果 </u>:

セグメント条件を表示または編集すると、選択したカテゴリが保存され、選択されます。

<u> 実際の結果 </u>:

選択したカテゴリが見つからず、正しく保存されませんでした。 コンソールで次のエラーが発生します。

```
category-checkbox-tree.js:249 Uncaught TypeError: Cannot set properties of undefined (setting 'value')
    at Ext.tree.TreePanel.Enhanced.<anonymous> (category-checkbox-tree.js:249)
    at Ext.util.Event.fire (ext-tree.js:29)
```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) を参照してください。
