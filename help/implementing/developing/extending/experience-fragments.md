---
title: 體驗片段概觀
description: 擴充Adobe Experience Manager as a Cloud Service體驗片段。
exl-id: bd4ea763-d17c-40a6-9a86-a24d7600229e
source-git-commit: d361ddc9a50a543cd1d5f260c09920c5a9d6d675
workflow-type: tm+mt
source-wordcount: '1641'
ht-degree: 0%

---

# 體驗片段{#experience-fragments}

## 基本知識 {#the-basics}

一個 [體驗片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md) 是一組一或多個元件，包括可在頁面中參考的內容和版面。

體驗片段主變體（或兩者）會使用：

* `sling:resourceType` ： `/libs/cq/experience-fragments/components/xfpage`

因為沒有 `/libs/cq/experience-fragments/components/xfpage/xfpage.html`，它還原為

* `sling:resourceSuperType` : `wcm/foundation/components/page`

## 純HTML轉譯 {#the-plain-html-rendition}

使用 `.plain.` 在URL的選擇器中，您可以存取純HTML轉譯。

此轉譯可從瀏覽器取得。 不過，其主要用途是允許其他應用程式（例如協力廠商網頁應用程式、自訂行動實作）僅使用URL直接存取體驗片段的內容。

純HTML轉譯會將通訊協定、主機和內容路徑新增至以下路徑：

* 型別： `src`， `href`，或 `action`

* 或結尾為： `-src`，或 `-href`

例如：

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>連結一律會參考發佈執行個體。 這些連結僅供第三方使用，因此連結一律會從發佈執行個體而不是作者執行個體呼叫。

![普通HTML轉譯](assets/xf-14.png)

純轉譯選擇器使用轉換器，而不是其他指令碼。 此 [Sling重寫程式](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) 會作為轉換器使用。 此轉換器設定於下列位置：

* `/libs/experience-fragments/config/rewriter/experiencefragments`

### 設定HTML轉譯產生 {#configuring-html-rendition-generation}

HTML轉譯是使用Sling重寫程式管道產生的。 管道定義於 `/libs/experience-fragments/config/rewriter/experiencefragments`. HTML轉換器支援下列選項：

* `allowedCssClasses`
   * 符合應留在最終轉譯中的CSS類別的RegEx運算式。
   * 如果客戶想要移除某些特定的CSS類別，此選項會很有用
* `allowedTags`
   * 最終轉譯中允許的HTML標籤清單。
   * 預設允許下列標籤（不需要設定）： html、head、title、body、img、p、span、ul、li、a、b、i、em、strong、h1、h2、h3、h4、h5、h6、br、noscript、div、link和script

Adobe建議使用覆蓋來設定重寫程式。 另請參閱 [AEMas a Cloud Service的覆蓋圖](/help/implementing/developing/introduction/overlays.md).

## 體驗片段的範本 {#templates-for-experience-fragments}

>[!CAUTION]
>
>***僅限*** 體驗片段支援可編輯的範本。

<!-- >***Only*** [editable templates](/help/sites-developing/page-templates-editable.md) are supported for Experience Fragments.
-->

為體驗片段開發新範本時，您可以遵循可編輯範本的標準做法。

<!-- When developing a new template for Experience Fragments you can follow the standard practices for an [editable template](/help/sites-developing/page-templates-editable.md).
-->

若要建立由偵測到的體驗片段範本 **建立體驗片段** 精靈，您必須遵循下列其中一個規則集：

1. 兩者:

   1. 樣板的資源型別（初始節點）必須繼承自：
      `cq/experience-fragments/components/xfpage`

   1. 範本名稱的開頭必須是：
      `experience-fragments`
此模式可讓使用者在/content/experience-fragments中建立體驗片段，作為 `cq:allowedTemplates` 此資料夾的屬性包含名稱開頭為的所有範本 `experience-fragment`. 客戶可以更新此屬性，以包含自己的命名配置或範本位置。

1. [允許的範本](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#configure-allowed-templates-folder) 可在體驗片段主控台中設定。

<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## 體驗片段的元件 {#components-for-experience-fragments}

開發要與/在體驗片段中使用的元件會遵循標準實務。

唯一額外的設定是確保範本上允許元件。 此津貼是透過內容原則來達成。

<!--
[Developing components](/help/sites-developing/components.md) for use with/in Experience Fragments follow standard practices.

The only additional configuration is to ensure that the components are [allowed on the template, this is achieved with the Content Policy](/help/sites-developing/page-templates-editable.md#content-policies).
-->

## 體驗片段連結重寫器提供者 — HTML {#the-experience-fragment-link-rewriter-provider-html}

在AEM中，您可以建立體驗片段。 體驗片段：

* 由一組元件及配置圖組成，
* 可以獨立於AEM頁面存在。

這類群組的使用案例之一，是將內容內嵌於第三方接觸點，例如Adobe Target。

### 預設連結重寫 {#default-link-rewriting}

<!--Using the [Export to Target](/help/sites-administering/experience-fragments-target.md) feature, you can:
-->

使用「匯出至目標」功能，您可以：

* 建立體驗片段，
* 新增元件，
* 然後以HTML格式或JSON格式將其匯出為Adobe Target選件。

此功能可在AEM的作者執行個體上啟用。 它需要有效的Adobe Target設定，以及Link Externalizer設定。

<!--
This feature can be [enabled on an author instance of AEM](/help/sites-administering/experience-fragments-target.md#Prerequisites). It requires a valid Adobe Target Configuration, and configurations for the Link Externalizer.
-->

Link Externalizer可用來判斷建立Target選件的HTML版本時需要正確的URL，然後傳送至Adobe Target。 此程式是必要的，因為Adobe Target要求可以公開存取TargetHTML選件內的所有連結。 這表示連結參照的任何資源以及體驗片段本身，都必須先發佈，才能使用。

根據預設，當您建構TargetHTML選件時，要求會傳送至AEM中的自訂Sling選取器。 此選取器稱為 `.nocloudconfigs.html`. 顧名思義，它會建立體驗片段的純HTML轉譯，但不包括雲端設定（這會是多餘的資訊）。

產生HTML頁面後，Sling重寫程式管線會修改為輸出：

1. 此 `html`， `head`、和 `body` 元素取代為 `div` 元素。 此 `meta`， `noscript`、和 `title` 元素會被移除（它們是原始元素的子元素） `head` 元素，且取代為時不予以考慮 `div` 元素)。

   完成此程式是為了確保Target活動中可包含HTMLTarget選件。

2. AEM會修改HTML中出現的任何內部連結，使其指向已發佈的資源。

   若要決定要修改的連結，AEM會對HTML元素的屬性遵循此模式：

   1. `src` 屬性
   2. `href` 屬性
   3. `*-src` 屬性(例如 `data-src`、和 `custom-src`)
   4. `*-href` 屬性(例如 `data-href`， `custom-href`、和 `img-href`)

   >[!NOTE]
   >
   >HTML中的內部連結是相對連結，但自訂元件在HTML中提供完整URL時可能會發生這種情況。 依預設，AEM會忽略這些完整的URL且不會進行任何修改。

   這些屬性中的連結會透過AEM Link Externalizer執行 `publishLink()` 將URL重新建立為在已發佈的例項上，如此便可公開使用。

使用現成可用的實作時，上述流程應足以從體驗片段產生Target選件，然後將其匯出至Adobe Target。 不過，此程式並未說明部分使用案例。 未說明的這些案例包括下列幾項：

* Sling對應僅在發佈執行個體上可用
* Dispatcher重新導向

對於這些使用案例，AEM會提供連結重寫程式提供者介面。

### 連結重寫程式提供者介面 {#link-rewriter-provider-interface}

對於較複雜的情況，不在 [預設](#default-link-rewriting)，AEM提供連結重寫程式提供者介面。 此介面是 `ConsumerType` 介面，可實作於套件組合中，作為服務。 它會繞過AEM對HTML選件的內部連結（從體驗片段轉譯）執行的修改。 此介面可讓您自訂重寫內部HTML連結的程式，以符合您的業務需求。

實作此介面作為服務的使用案例範例包括：

* Sling對應已在發佈執行個體上啟用，但在作者執行個體上未啟用
* Dispatcher或類似技術可用來在內部重新導向URL
* 此 `sling:alias mechanisms` 資源已準備就緒

>[!NOTE]
>
>此介面只會處理來自所產生Target選件的內部HTML連結。

連結重寫程式提供者介面( `ExperienceFragmentLinkRewriterProvider`)如下所示：

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### 如何使用連結重寫程式提供者介面 {#how-to-use-the-link-rewriter-provider-interface}

若要使用介面，您必須先建立包含實作連結重寫程式提供者介面之新服務元件的組合。

此服務用於插入Experience Fragment Export to Target重新寫入，以便能夠存取各種連結。

例如， `ComponentService`：

```java
import com.adobe.cq.xf.ExperienceFragmentLinkRewriterProvider;
import com.adobe.cq.xf.ExperienceFragmentVariation;
import org.osgi.service.component.annotations.Service;
import org.osgi.service.component.annotations.Component;

@Component
@Service
public class GeneralLinkRewriter implements ExperienceFragmentLinkRewriterProvider {

    @Override
    public String rewriteLink(String link, String tag, String attribute) {
        return null;
    }

    @Override
    public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
        return false;
    }

    @Override
    public int getPriority() {
        return 0;
    }

}
```

為了讓服務運作，現在必須在服務內實作三種方法：

* `[shouldRewrite](#shouldrewrite)`
* `[rewriteLink](#rewritelink)`

   * `rewriteLinkExample2`

* `[getPriority](#priorities-getpriority)`

#### shouldRewrite {#shouldrewrite}

向系統指出是否必須在呼叫特定體驗片段變數的「匯出至Target」時重寫連結。 您可以實作下列方法：

`shouldRewrite(ExperienceFragmentVariation experienceFragment);`

例如：

```java
@Override
public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
    return experienceFragment.getPath().equals("/content/experience-fragment/master");
}
```

此方法會以引數形式接收「匯出至目標」系統正在重寫的體驗片段變數。

在上述範例中，您想要重寫：

* 中的連結 `src`

* `href` 僅限屬性

* 針對特定體驗片段：
  `/content/experience-fragment/master`

任何透過「匯出至目標」系統的其他體驗片段會遭忽略，且不會受到此服務中實作的變更影響。

#### rewriteLink {#rewritelink}

對於受重寫程式影響的體驗片段變數，它會繼續讓服務處理連結重寫。 每當內部HTML中出現連結時，就會叫用下列方法：

`rewriteLink(String link, String tag, String attribute)`

作為輸入，方法會接收引數：

* `link`
此 `String` 表示正在處理的連結。 此表示通常是指向作者執行個體上資源的相對URL。

* `tag`
正在處理的HTML元素的名稱。

* `attribute`
確切的屬性名稱。

例如，如果「匯出至目標」系統正在處理此元素，您可以定義 `CSSInclude` 作為：

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

對的呼叫 `rewriteLink()` 方法可使用下列引數完成：

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

當您建立服務時，您的決定是根據給定的輸入，然後相應地重寫連結。

例如，您想要移除 `/etc.clientlibs` URL的一部分並新增適當的外部網域。 為了簡單起見，請考量您有權存取您服務的資源解析器，例如 `rewriteLinkExample2`：

>[!NOTE]
>
>如需如何透過服務使用者取得資源解析器的詳細資訊，請參閱AEM中的服務使用者。

<!--
>For more information on how to get a resource resolver through a service user see [Service Users in AEM](/help/sites-administering/security-service-users.md).
-->

```java
private ResourceResolver resolver;

private Externalizer externalizer;

@Override
public String rewriteLink(String link, String tag, String attribute) {

    // get the externalizer service
    externalizer = resolver.adaptTo(Externalizer.class);
    if(externalizer == null) {
        // if there was an error, then we do not modify the link
        return null;
    }

    // remove leading /etc.clientlibs from resource link before externalizing
    link = link.replaceAll("/etc.clientlibs", "");

    // considering that we configured our publish domain, we directly apply the publishLink() method
    link = externalizer.publishLink(resolver, link);

    return link;
}
```

>[!NOTE]
>
>如果上述方法傳回 `null`，則「匯出至Target」系統會將連結維持不變，即資源的相對連結。

#### 優先順序 — getPriority {#priorities-getpriority}

需要多個服務來迎合不同體驗片段的型別並不罕見，甚至需要有一個通用服務來處理所有體驗片段的外部化和對應。 在這些情況下，可能會發生與使用哪個服務相關的衝突，因此AEM提供了定義 **優先順序** 適用於不同服務。 使用下列方法指定優先順序：

* `getPriority()`

此方法允許使用多項服務，其中 `shouldRewrite()` 對於相同的體驗片段，方法會傳回true。 從中傳回最高數字的服務 `getPriority()`方法是處理體驗片段變數的服務。

例如，您可以建立 `GenericLinkRewriterProvider` 會處理所有體驗片段的基本對應，以及當 `shouldRewrite()` 方法傳回 `true` 適用於所有體驗片段變數。 針對數個特定體驗片段，您可能需要特殊處理，因此在此情況下，您可以提供 `SpecificLinkRewriterProvider` 對於 `shouldRewrite()` 方法只會傳回部分體驗片段變數的true。 若要確保 `SpecificLinkRewriterProvider` 被選擇用於處理這些體驗片段變數，它必須返回其 `getPriority()` 方法數字大於 `GenericLinkRewriterProvider.`
