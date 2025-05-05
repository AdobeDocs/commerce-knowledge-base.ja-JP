---
source-git-commit: 0cfb7dc0dce68bcb0933a5ae49b0cd5a8b5b5a39
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---
# メタデータ検証ガイド

MD ファイル内のメタデータが正しくフォーマットされるように、メタデータ検証テストを導入しました。 このドキュメントでは、最も一般的なメタデータ検証エラーのいくつかを投稿者が回避するのに役立つガイドラインを提供します。

**メタデータの例：**

```markdown
---
title: This is a title
labels: article,labels,tags
---

Article content...
```

## 一般的な検証エラーとその回避方法/修正方法

メタデータの検証エラーが発生する最も一般的なシナリオの一部を次に示します。

### メタデータのコロン

タイトルまたはラベル、またはその両方にコロンが含まれている場合、検証エラーが発生します。

**例：**

```markdown
---
title: Patch: Unable to validate VAT number - Adobe Commerce on cloud infrastructure
labels: patch: 2041.1,article,labels,tags
---
```

このエラーを回避するには、タイトルまたはラベル（両方にコロンがある場合は両方）を **一重引用符** で囲みます。

**例：**

```markdown
---
title: 'Patch: Unable to validate VAT number - Adobe Commerce on cloud infrastructure'
labels: 'patch: 2041.1,article,labels,tags'
---
```

### メタデータのコロンと一重引用符またはアポストロフィ

タイトルまたはラベルにコロン、一重引用符またはアポストロフィが含まれている場合、以前のソリューションは機能しません。

**例：**

```markdown
---
title: Patch: Can't validate 'VAT' number - Adobe Commerce on cloud infrastructure
labels: patch: 2041.1,'article',labels,tags
---
```

このエラーは、タイトルまたはラベル（またはその両方）を **二重引用符** で囲むことで修正します。

**例：**

```markdown
---
title: "Patch: Can't validate 'VAT' number - Adobe Commerce on cloud infrastructure"
labels: "patch: 2041.1,'article',labels,tags"
---
```

### メタデータのコロン、二重引用符、一重引用符またはアポストロフィ

**例：**

```markdown
---
title: Patch: Can't validate 'VAT' number - Adobe "Commerce" on cloud infrastructure
labels: patch: 2041.1,'article',"labels",can't,tags
---
```

この場合は、タイトルまたはラベル（またはその両方 **を二重引用符で囲み**&#x200B;**バックスラッシュ** を使用して、タイトルとラベルのすべての二重引用符をエスケープします。

**例：**

```markdown
---
title: "Patch: Can't validate 'VAT' number - Adobe \"Commerce\" on cloud infrastructure"
labels: "patch: 2041.1,'article',\"labels\",can't,tags"
---
```

### メタデータにフィールドがありません

タイトルフィールドまたはラベルフィールドがメタデータにない場合は、検証エラーが発生します。

**例：**

```markdown
---
title: This is a title
---
```

または

```markdown
---
labels: article,labels,tags
---
```

このエラーを回避するには、両方のフィールドをメタデータに含めます。

「ラベル」フィールドは空のままにすることもできますが、エラーは発生しませんが、「タイトル」フィールドには入力する必要があります。

**例：**

```markdown
---
title: Unlike labels the title field must be filled
labels:
---
```
