---
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%
---

# KB形式ガイド

## Markdownでのオーサー

通常、[Adobe Experience League Markdown構文スタイルガイド ](https://experienceleague.adobe.com/docs/authoring-guide-exl/using/markdown/syntax-style-guide.html?lang=en)を使用しますが、いくつかの違いや例外があります。 また、特定のケースでは、特定のHTML タグが必要になります。

次に、当社のリポジトリで最もよく使用されるMarkdown形式の例を示します。

## 基本書式設定

テキストを太字で書式設定するには、次の2つのアスタリスク記号で囲みます。

`This will be **bold** text`

テキストを斜体として書式設定するには、1つのアスタリスクを使用します。

`This text will be *italics*`

下線付きのテキストを書式設定するには、`<ins>` タグを使用します。

`<ins>This text will be underlined</ins>`

改行を追加するには、`<br>` HTML タグを使用します。


## ヘッダー

H2からH5までのヘッダーには、次の書式設定を使用します。 記事タイトルはH1と見なされるため、H1は使用されません。

`## Header 2 `

`### Header 3 `

`#### Header 4`

`##### Header 5`

## インラインおよびブロックのコード

1つのバックティックを使用して、ハイライトするコード要素を囲みます。

これは、テキストの段落内の\&#39;インラインコード\&#39;です。

### コードブロック

コードブロックを挿入するには、コードブロックを3つのバックティックで囲み、3つのバックティックを開いた後に言語を指定します。

\&#39;\&#39;\&#39; sql

SELECT TABLE_NAME AS `Table`,
ROUND （（DATA_LENGTH + INDEX_LENGTH） / 1024 / 1024） AS `Size (MB)`
FROM information_schema.TABLES
WHERE TABLE_SCHEMA = &quot;%project_id%&quot;
ORDER BY （DATA_LENGTH + INDEX_LENGTH） DESC;

\&#39;\&#39;\&#39;

これは次のようにレンダリングされます。

```sql
SELECT TABLE_NAME AS `Table`,
  ROUND((DATA_LENGTH + INDEX_LENGTH) / 1024 / 1024) AS `Size (MB)`
FROM information_schema.TABLES
WHERE TABLE_SCHEMA = "%project_id%"
ORDER BY (DATA_LENGTH + INDEX_LENGTH) DESC;
```

リンティングルールに従って、コードブロックの言語を常に指定する必要があります。

サポートされている言語の一覧については、https://github.com/github/linguist/blob/master/lib/linguist/languages.ymlを参照してください。

マークダウンの特定の言語でハイライト表示が機能しない場合（つまり、言語がサポートされていない場合）、https://support.magento.com/hc/en-us/に公開するときに少なくともハイライト表示するには、次のHTMLを使用します。

```html
<pre><code class="language-%language-code%"
your code here
</pre></code>
```

ここで、``%language-code%``は、[Prism.jsがサポートする言語](https://prismjs.com/#supported-languages)によって定義されたコードです。

## Lists

リストは常に空白行で他のコンテンツから分離します。 リストの先頭に空白行を付ける必要があります。

順序付きリストには、次の書式設定を使用します。

```markdown
1. First numbered list item.
1. Second numbered list item.
...
1. Last numbered list item.
```

順序なし箇条書きリストを作成するには、*、+、-.で行を始めます。 しかし、1つの方法を選択し、記事を通して一貫して使用してください。

例：

```markdown
* Unordered list item.
* Unordered list item.
---
* Last unordered list item.
```

リスト項目間にコンテンツを追加するには、行の先頭に4つのスペースを追加します。

```markdown
* List item.
* List item.
    Here's some content between list items.
* Here we continue the list
```

この方法でリストを埋め込むこともできます。

## リンク

外部リンクは簡単です。

```markdown
[Adobe](https://www.adobe.com)
```

### 添付ファイルへのリンク

あらゆる添付ファイルは、.png、.jpg、および.jpeg形式である必要があります。 セキュリティ上の理由から、3つの形式の添付ファイルのみを受け付けます。

画像を挿入するには、記事と同じセクション フォルダーの&#x200B;*assets* サブフォルダーに画像を配置し、次の構文を使用して画像を記事に挿入します。

```markdown
![alt text](assets/image.png)
```

画像のサイズをカスタマイズする場合は、次のHTML タグを使用して設定する必要があります。

```html
<img src = "assets/image.png" alt = "your alt text" width="custom width, ex: 250px">
```

```markdown
[asset_title](assets/%file_name%).
```

### 記事の特定のセクションへのリンク

アーティクル内のセクションを参照する必要がある場合は、別のアンカーを作成する必要はありません。 H2～H6の各見出しに対して、公開時に自動的に生成されます。 アンカーは、すべての単語を小文字にし、「 – 」を使用して単語を区切ることで、ヘッダーから生成されます。

例：

```markdown
## This is header
```

このヘッダーへのリンクです：

```markdown
[this is link to the anchor in the same article](#this-is-header)
```

header以外の要素を参照する必要がある場合は、HTMLを使用して要素を定義し、[id属性](https://www.w3schools.com/html/html_id.asp)を使用します。 その後、MarkdownまたはHTMLを使用して、このIDを参照できます。

### 他の記事への相対リンクとリンク

サポートナレッジベース記事を参照する際は、相対リンクを使用しないでください。 これらのリンクは、[Adobe Commerce ヘルプセンター](https://support.magento.com/hc/en-us)で記事が公開される際には機能しません。
[Adobe Commerce ヘルプセンター](https://support.magento.com/hc/en-us)の完全なハイパーリンクを使用してください。


## 表

テーブル ](https://www.w3schools.com/html/html_tables.asp)に[HTML形式を使用します。


## 警告と情報ブロック

成功メモブロック：

```
>![success]
>
>This is a success note
```

警告ブロック：

```
>![warning]
>
>This is a warning
```

情報メモ ブロック：

```
>![info]
>
>This is a block with additional info
```
