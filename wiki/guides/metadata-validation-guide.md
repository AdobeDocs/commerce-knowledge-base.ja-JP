---
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%
---

# メタデータ検証ガイド

MD ファイル内のメタデータの正しいフォーマットを確保するために、メタデータ検証テストを導入しました。 このドキュメントでは、最も一般的なメタデータ検証エラーの一部を避けるためのガイドラインを提供します。

**メタデータの例：**

```markdown
---
title: This is a title
labels: article,labels,tags
---

Article content...
```

## 一般的な検証エラーとその回避/修正方法

メタデータ検証エラーが発生する最も一般的なシナリオを次に示します。

### メタデータのコロン

タイトルまたはラベル、またはその両方にコロンがある場合、検証エラーが発生します。

**例：**

```markdown
---
title: Patch: Unable to validate VAT number - Adobe Commerce on cloud infrastructure
labels: patch: 2041.1,article,labels,tags
---
```

このエラーを回避するには、**一重引用符**&#x200B;でタイトルまたはラベル（または両方にコロンがある場合はその両方）を折り返します。

**例：**

```markdown
---
title: 'Patch: Unable to validate VAT number - Adobe Commerce on cloud infrastructure'
labels: 'patch: 2041.1,article,labels,tags'
---
```

### メタデータ内のコロンと一重引用符またはアポストロフィ

タイトルまたはラベルにコロン、一重引用符、アポストロフィがある場合、前のソリューションは機能しません。

**例：**

```markdown
---
title: Patch: Can't validate 'VAT' number - Adobe Commerce on cloud infrastructure
labels: patch: 2041.1,'article',labels,tags
---
```

このエラーは、**二重引用符**&#x200B;でタイトルまたはラベル（またはその両方）を折り返すことによって修正されます。

**例：**

```markdown
---
title: "Patch: Can't validate 'VAT' number - Adobe Commerce on cloud infrastructure"
labels: "patch: 2041.1,'article',labels,tags"
---
```

### メタデータ内のコロン、二重引用符、および一重引用符またはアポストロフィ

**例：**

```markdown
---
title: Patch: Can't validate 'VAT' number - Adobe "Commerce" on cloud infrastructure
labels: patch: 2041.1,'article',"labels",can't,tags
---
```

この場合、タイトルまたはラベル（またはその両方）を&#x200B;**二重引用符**&#x200B;で囲み、**バックスラッシュ**&#x200B;を使用して、タイトルとラベルのすべての二重引用符をエスケープします。

**例：**

```markdown
---
title: "Patch: Can't validate 'VAT' number - Adobe \"Commerce\" on cloud infrastructure"
labels: "patch: 2041.1,'article',\"labels\",can't,tags"
---
```

### メタデータにフィールドがありません

タイトルフィールドまたはラベルフィールドがメタデータにない場合、検証エラーが発生します。

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

「ラベル」フィールドは空のままにしておくことができ、エラーは発生しませんが、「タイトル」フィールドに入力する必要があります。

**例：**

```markdown
---
title: Unlike labels the title field must be filled
labels:
---
```
