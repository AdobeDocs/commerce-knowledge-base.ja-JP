---
title: Adobe Commerceへの新しい国の追加方法
description: この文書では、Adobe Commerceと Zend ロケールライブラリに存在しない国を追加する方法を説明します。 これには、該当する契約条件の下で顧客のカスタマイズを構成するコードとデータベースの変更が必要です。 この記事に含まれるサンプル資料は、いかなる保証もなく「現状のまま」提供されることに注意してください。 Adobeまたは関連会社は、これらの資料を維持、修正、更新、変更、修正、またはその他の方法でサポートする義務を負いません。 ここでは、これを達成するために行う必要があるものの基本原則を説明します。
exl-id: af499add-4966-4a3a-972a-62a34c169a1b
feature: Build, Cache
source-git-commit: f11c8944b83e294b61d9547aefc9203af344041d
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 0%

---

# Adobe Commerceへの新しい国の追加方法

この文書では、Adobe Commerceと Zend ロケールライブラリに存在しない国を追加する方法を説明します。 これには、該当する契約条件の下で顧客のカスタマイズを構成するコードとデータベースの変更が必要です。 この記事に含まれるサンプル資料は、いかなる保証もなく「現状のまま」提供されることに注意してください。 Adobeまたは関連会社は、これらの資料を維持、修正、更新、変更、修正、またはその他の方法でサポートする義務を負いません。 ここでは、これを達成するために行う必要があるものの基本原則を説明します。

この例では、Adobe Commerceのインストールまたはアップグレードプロセス時に適用されるデータパッチを含む新しいAdobe Commerce モジュールを作成し、国コード XX を含む抽象 Country をAdobe Commerceに追加します。 [Adobe Commerce ディレクトリ ](https://developer.adobe.com/commerce/php/module-reference/module-directory/) は、最初の国の一覧を作成し、その一覧に地域を追加するために修正プログラムのセットアップを使用します。 この記事では、新しい国をリストに追加する新しいモジュールの作成方法を説明します。 参照用に既存のAdobe Commerce Directory モジュールのコードを確認できます。 これは、次のサンプルモジュールが国と地域のリストを構築するディレクトリモジュールジョブを継続し、Adobe Commerce ディレクトリモジュールの一部のセットアップパッチを再利用するためです。

## 推奨ドキュメント

新しいAdobe Commerce モジュールを作成するには、モジュール開発に関する知識が必要です。

新しいモジュールを作成する前に、開発者向けドキュメントの次のトピックを参照してください。

* [PHP デベロッパーガイド ](https://devdocs.magento.com/guides/v2.4/extension-dev-guide/bk-extension-dev-guide.html)
* [ モジュールの概要 ](https://devdocs.magento.com/guides/v2.4/architecture/archi_perspectives/components/modules/mod_intro.html)
* [ 新しいモジュールの作成 ](https://devdocs.magento.com/videos/fundamentals/create-a-new-module/)
* [ モジュール設定ファイル ](https://devdocs.magento.com/guides/v2.4/config-guide/config/config-files.html)

## 必要な情報

新しい国には、Adobe Commerce全体で一意の名前、国 ID、ISO2 および ISO3 コードが必要です。

## モジュール構造

この例では、次のディレクトリ構造で\&#39;ExtraCountries\&#39;という新しいモジュールを作成します。

（モジュール構造について詳しくは、開発者向けドキュメントの [ モジュールの概要 ](https://devdocs.magento.com/guides/v2.4/architecture/archi_perspectives/components/modules/mod_intro.html) を参照してください）。

<pre><ExtraCountries>
 |
 <etc>
 | |
 | config.xml
 | di.xml
 | module.xml
 |
 <Plugin>
 | |
 | <Framework>
 |   |
 |   <Locale>
 |     |
 |     TranslatedListsPlugin.php
 |
 <Setup>
 | |
 | <Patch>
 |   |
 |   <Data>
 |     |
 |     AddDataForAbstractCountry.php
 |
 composer.json
 registration.php</pre>

>[!NOTE]
>
>この記事の各ヘッダーセクションでは、モジュール構造セクションのファイルについて説明します。

## ExtraCountries/etc/config.xml

この XML ファイルで、新しいモジュール設定が定義されます。 次の設定とタグを編集して、新しい国のデフォルト設定を調整できます。

* `allow` – 新しく追加した国をデフォルトで「国を許可」リストに追加するには、`allow` タグコンテンツの末尾に新しい国コードを追加します。 国コードはコンマで区切ります。 このタグは、`Directory` モジュール設定ファイル *（Directory/etc/config.xml）のデータを上書きすることに注意してください*`allow` タグなので、ここですべてのコードを繰り返し、新しいコードを追加します。
* `optional_zip_countries` – 新しく追加した国の郵便番号をオプションにする必要がある場合は、`optional_zip_countries` タグのコンテンツの末尾に国コードを追加します。 国コードはコンマで区切ります。 このタグは、`Directory` モジュール設定ファイル *（Directory/etc/config.xml）のデータを上書きすることに注意してください*`optional_zip_countries` タグなので、ここですべてのコードを繰り返し、新しいコードを追加します。
* `eu_countries` – 新しく追加した国がデフォルトで EU 諸国リストに含まれる必要がある場合は、`eu_countries` タグのコンテンツの末尾に国コードを追加します。 国コードはコンマで区切ります。 このタグは、`Store` モジュール設定ファイル *（\_Store/etc/config.xml\_）のデータを上書きすることに注意してください*`eu_countries` タグなので、ここですべてのコードを繰り返し、新しいコードを追加します。
* `config.xml` ファイルの例

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_Store:etc/config.xsd">
    <default>
        <general>
            <country>
                <!-- append a new country codes to the end of this list -->
                <allow>AF,AL,DZ,AS,AD,AO,AI,AQ,AG,AR,AM,AW,AU,AT,AX,AZ,BS,BH,BD,BB,BY,BE,BZ,BJ,BM,BL,BT,BO,BQ,BA,BW,BV,BR,IO,VG,BN,BG,BF,BI,KH,CM,CA,CD,CV,KY,CF,TD,CL,CN,CX,CW,CC,CO,KM,CG,CK,CR,HR,CU,CY,CZ,DK,DJ,DM,DO,EC,EG,SV,GQ,ER,EE,ET,FK,FO,FJ,FI,FR,GF,PF,TF,GA,GM,GE,DE,GG,GH,GI,GR,GL,GD,GP,GU,GT,GN,GW,GY,HT,HM,HN,HK,HU,IS,IM,IN,ID,IR,IQ,IE,IL,IT,CI,JE,JM,JP,JO,KZ,KE,KI,KW,KG,LA,LV,LB,LS,LR,LY,LI,LT,LU,ME,MF,MO,MK,MG,MW,MY,MV,ML,MT,MH,MQ,MR,MU,YT,FX,MX,FM,MD,MC,MN,MS,MA,MZ,MM,NA,NR,NP,NL,AN,NC,NZ,NI,NE,NG,NU,NF,KP,MP,NO,OM,PK,PW,PA,PG,PY,PE,PH,PN,PL,PS,PT,PR,QA,RE,RO,RS,RU,RW,SH,KN,LC,PM,VC,WS,SM,ST,SA,SN,SC,SL,SG,SK,SI,SB,SO,ZA,GS,KR,ES,LK,SD,SR,SJ,SZ,SE,CH,SX,SY,TL,TW,TJ,TZ,TH,TG,TK,TO,TT,TN,TR,TM,TC,TV,VI,UG,UA,AE,GB,US,UM,UY,UZ,VU,VA,VE,VN,WF,EH,XK,YE,ZM,ZW,XX</allow>
​
                <!-- if added countries need to belong to the European Union Countries list by default, append their codes to the end of this list -->
                <eu_countries>AT,BE,BG,CY,CZ,DK,EE,FI,FR,DE,GR,HR,HU,IE,IT,LV,LT,LU,MT,NL,PL,PT,RO,SK,SI,ES,SE,GB,XX</eu_countries>
​
                <!-- if added countries are not require zip code, append it's code to the end of this list -->
                <optional_zip_countries>HK,IE,MO,PA,GB,XX</optional_zip_countries>
            </country>
        </general>
    </default>
</config>
```

モジュール設定ファイルについて詳しくは、開発者向けドキュメントの [PHP 開発者ガイド/設定ファイルの定義 ](https://devdocs.magento.com/guides/v2.4/extension-dev-guide/build/required-configuration-files.html) を参照してください。

これらの変更はオプションであり、「国を許可」、「郵便番号はオプションです」および「欧州連合（EU）諸国」リストに対する新しい国のデフォルトに影響するだけです。 このファイルをモジュール構造からスキップした場合でも、新しい国は追加されますが、**管理者**/**ストア**/*設定*/**設定**/**一般**/**国オプション** 設定ページで手動で設定する必要があります。

### ExtraCountries/etc/di.xml

`di.xml` ファイルは、オブジェクトマネージャーによって挿入される依存関係を設定します。 `di.xml` について詳しくは、開発者向けドキュメントの <a>PHP Developer Guide > The di.xml</a> を参照してください。

この例では、Zend Locale Library のローカリゼーションデータにコードが存在しない場合、新たに導入された国コードを完全な国名に変換する `_TranslatedListsPlugin_` を登録する必要があります。

`di.xml` 例

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
    <type name="Magento\Framework\Locale\TranslatedLists">
        <plugin name="Magento_Directory" type="VendorName\ExtraCountries\Plugin\Framework\Locale\TranslatedListsPlugin"/>
    </type>
</config>
```

### ExtraCountries/etc/module.xml

モジュール登録ファイルでは、「Adobe Commerce Directory」モジュールの依存性を指定し、「Extra Countries」モジュールが Directory モジュールの後に登録され、実行されることを確認する必要があります。

モジュールの依存関係について詳しくは、開発者向けドキュメントの [ モジュールの依存関係の管理 ](https://devdocs.magento.com/guides/v2.4/architecture/archi_perspectives/components/modules/mod_depend.html#managing-module-dependencies) を参照してください。

`module.xml` 例

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
    <module name="VendorName_ExtraCountries" >
        <sequence>
            <module name="Magento_Directory"/>
        </sequence>
    </module>
</config>
```

### ExtraCountries/Plugin/Framework/Locale/TranslatedListsPlugin.php

`aroundGetCountryTranslation()` プラグインメソッドでは、国コードを完全な国名に翻訳する必要があります。 これは、Zend ロケールライブラリ内の新しい国コードにフルネームが関連付けられていない国で必須の手順です。

```php
<?php
namespace VendorName\ExtraCountries\Plugin\Framework\Locale;
​
use Magento\Framework\Locale\ListsInterface;
​
/**
 * Plugin to add full names of added countries that are not included in Zend Locale Data
 */
class TranslatedListsPlugin
{
    /**
     * Get the full name of added countries
     *
     * Since the locale data for the added country may not be present in the Zend Locale Library,
     * we need to provide full country name matching the added code
     *
     * @param ListsInterface $subject
     * @param callable $proceed
     * @param $value
     * @param null $locale
     * @return string
     */
    public function aroundGetCountryTranslation(
        ListsInterface $subject,
        callable $proceed,
        $value,
        $locale = null
    )
    {
        if ($value == 'XX') {
            return 'Abstract Country';
        }
​
        return $proceed($value, $locale);
    }
}
```

### ExtraCountries/Setup/Patch/Data/AddDataForAbstractCountry.php

このデータパッチは、Adobe Commerceのインストールまたはアップグレードプロセス中に実行され、新しい国レコードをデータベースに追加します。

データパッチについて詳しくは、開発者向けドキュメントの [ データおよびスキーマパッチの開発 ](https://devdocs.magento.com/guides/v2.4/extension-dev-guide/declarative-schema/data-patches.html) を参照してください。

次の例では、メソッド `apply()` の `$data` 配列に、新しい国の国 ID、ISO2 および ISO3 コードが含まれ、このデータがデータベースに挿入されていることがわかります。

```php
<?php
namespace Magento\ExtraCountries\Setup\Patch\Data;
​
use Magento\Framework\Setup\ModuleDataSetupInterface;
use Magento\Framework\Setup\Patch\DataPatchInterface;
use Magento\Framework\Setup\Patch\PatchVersionInterface;
​
/**
 * Add Abstract Country data to the country list
 *
 * @package Magento\ExtraCountries\Setup\Patch
 */
class AddDataForAbstractCountry implements DataPatchInterface, PatchVersionInterface
{
    /**
     * @var ModuleDataSetupInterface
     */
    private $moduleDataSetup;
​
    /**
     * @param ModuleDataSetupInterface $moduleDataSetup
     */
    public function __construct(
        ModuleDataSetupInterface $moduleDataSetup
    ) {
        $this->moduleDataSetup = $moduleDataSetup;
    }
​
    /**
     * @inheritdoc
     */
    public function apply()
    {
        /**
         * Fill table directory/country
         */
        $data = [
            ['XX', 'XX', 'XX']
        ];
​
        $columns = ['country_id', 'iso2_code', 'iso3_code'];
        $this->moduleDataSetup->getConnection()->insertArray(
            $this->moduleDataSetup->getTable('directory_country'),
            $columns,
            $data
        );
    }
​
    /**
     * @inheritdoc
     */
    public static function getDependencies()
    {
        return [];
    }
​
    /**
     * @inheritdoc
     */
    public static function getVersion()
    {
        return '0.0.1';
    }
​
    /**
     * @inheritdoc
     */
    public function getAliases()
    {
        return [];
    }
}
```

### ExtraCountries/registration.php

次に registration.php ファイルの例を示します。 モジュールの登録について詳しくは、開発者向けドキュメントの [PHP 開発者ガイド > コンポーネントの登録 ](https://devdocs.magento.com/guides/v2.4/extension-dev-guide/build/component-registration.html) を参照してください。

```php
<?php
use Magento\Framework\Component\ComponentRegistrar;
​
ComponentRegistrar::register(ComponentRegistrar::MODULE, 'VendorName_ExtraCountries', __DIR__);
```

### ExtraCountries/composer.json

これは、composer.json ファイルの例です。

composer.json について詳しくは、開発者向けドキュメントの [PHP Developer Guide > The composer.json file](https://devdocs.magento.com/guides/v2.4/extension-dev-guide/build/composer-integration.html) を参照してください。

```json
{
    "name": "vendor_name/module-extra-countries",
    "description": "A module that adds extra countries to magento directory",
    "type": "magento2-module",
    "license": [
    ],
    "require": {
        "php": "~7.3.0||~7.4.0",
        "lib-libxml": "*",
        "magento/framework": "*",
        "magento/module-directory": "*"
    },
    "autoload": {
        "files": [
            "registration.php"
        ],
        "psr-4": {
            "VendorName\\ExtraCountries\\": ""
        }
    },
    "config": {
        "sort-packages": true
    }
}
```

## モジュールのインストール

モジュールのインストール方法については、開発者ドキュメントの [ モジュールの場所 ](https://devdocs.magento.com/guides/v2.4/architecture/archi_perspectives/components/modules/mod_intro.html#module-locations) を参照してください。

モジュールディレクトリが正しい場所に配置されたら、`bin/magento setup:upgrade` を実行してデータパッチを適用し、翻訳プラグインを登録します。

新しい変更が機能するには、ブラウザーのキャッシュをクリーンアップする必要がある場合があります。
