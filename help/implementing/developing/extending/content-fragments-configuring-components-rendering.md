---
title: 轉譯專用內容片段設定元件
description: 轉譯專用內容片段設定元件
exl-id: 6606dc3b-f1b8-4941-8fd0-f69cbd414afa
feature: Developing, Content Fragments
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 5%

---

# 轉譯專用內容片段設定元件{#content-fragments-configuring-components-for-rendering}

有數個[進階服務](#definition-of-advanced-services-that-need-configuration)與轉譯內容片段相關。 若要使用這些服務，這類元件的資源型別必須在內容片段框架中讓使用者知道這些元件。

這可透過設定[OSGi服務 — 內容片段元件設定](#osgi-service-content-fragment-component-configuration)來完成。

在下列情況下，需要此資訊：

* 您需要實作自己的內容片段型元件，
* 而且需要使用進階服務。

Adobe建議使用核心元件。

>[!CAUTION]
>
>* **如果您不需要下述的[進階服務](#definition-of-advanced-services-that-need-configuration)**，您可以忽略此設定。
>
>* **當您擴充或使用現成可用的元件時**，不建議變更OSGi設定。
>
>* **您可以從頭開始撰寫只使用內容片段API且不使用進階服務的元件**。 但是，在這種情況下，您必須開發元件，以便處理適當的處理。
>
>因此，建議使用核心元件。

## 需要設定的進階服務定義 {#definition-of-advanced-services-that-need-configuration}

需要註冊元件的服務包括：

* 在發佈期間正確判斷相依性（也就是說，如果片段和模型自上次發佈後有所變更，請確定片段和模型可以隨頁面自動發佈）。
* 支援全文檢索搜尋的內容片段。
* *中間內容的管理/處理。*
* 管理/處理&#x200B;*混合媒體資產。*
* 參考片段的Dispatcher flush （如果重新發佈包含片段的頁面）。
* 使用段落式演算。

若您需要一或多個這些功能，通常使用現成可用的進階服務會比較容易，而不用從頭開始開發。

## OSGi服務 — 內容片段元件設定 {#osgi-service-content-fragment-component-configuration}

組態必須繫結至OSGi服務&#x200B;**內容片段元件組態**：

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>如需詳細資訊，請參閱[OSGi設定](/help/implementing/deploying/overview.md#osgi-configuration)。

例如：

![OSGi設定內容片段元件設定](assets/cf-component-configuration-osgi.png)

OSGi設定是：

<table>
 <thead>
  <tr>
   <td>標籤</td>
   <td>OSGi設定<br /> </td>
   <td>說明</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><strong>資源類型</strong></td>
   <td><code>dam.cfm.component.resourceType</code></td>
   <td>要登入的資源型別；例如，<br /> <p><span class="cmp-examples-demo__property-value"><code>core/wcm/components/contentfragment/v1/contentfragment</code></code></p> </td>
  </tr>
  <tr>
   <td><strong>參考屬性</strong></td>
   <td><code>dam.cfm.component.fileReferenceProp</code></td>
   <td>包含片段參考的屬性名稱；例如<code>fragmentPath</code>或 <code>fileReference</code></td>
  </tr>
  <tr>
   <td><strong>元素屬性</strong></td>
   <td><code>dam.cfm.component.elementsProp</code></td>
   <td>包含要呈現之元素名稱的屬性名稱；例如，<code>elementName</code></td>
  </tr>
  <tr>
   <td><strong>變數屬性</strong><br /> </td>
   <td><code>dam.cfm.component.variationProp</code></td>
   <td>包含要呈現之變數名稱的屬性名稱；例如，<code>variationName</code></td>
  </tr>
 </tbody>
</table>

對於某些功能，您的元件必須遵循預先定義的慣例。 下表詳細說明必須由元件為每個段落（即每個元件執行個體的`jcr:paragraph`）定義的屬性，以便服務能夠正確偵測和處理這些屬性。

<table>
 <thead>
  <tr>
   <td>屬性名稱</td>
   <td>說明</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><code>paragraphScope</code></td>
   <td><p>字串屬性，定義在<em>單一元素轉譯模式</em>下段落的輸出方式。</p> <p>值：</p>
    <ul>
     <li><code>all</code> ：呈現所有段落</li>
     <li><code>range</code> ：呈現以下專案提供的段落範圍： <code>paragraphRange</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphRange</code></td>
   <td><p>字串屬性，定義在<em>單一元素轉譯模式</em>中要輸出的段落範圍。</p> <p>格式：</p>
    <ul>
     <li><code>1</code> 或<code>1-3</code>或<code>1-3;6;7-8</code>或 <code>*-3;5-*</code>
     <ul>
       <li><code>-</code> 範圍指示器</li>
       <li><code>;</code> 清單分隔符號</li>
       <li><code>*</code> 萬用字元</li>
     </ul>
     </li>
     <li>僅在<code>paragraphScope</code>設定為時評估 <code>range</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphHeadings</code></td>
   <td>定義標題（例如<code>h1</code>、<code>h2</code>、<code>h3</code>）是否計為段落(<code>true</code>)的布林屬性(<code>false</code>)</td>
  </tr>
 </tbody>
</table>

## 範例 {#example}

如需範例，請參閱以下內容(在現成可用的AEM例項上)：

```
/apps/core/wcm/config/com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl-core-comp-v1.config
```

這包含：

```
dam.cfm.component.resourceType="core/wcm/components/contentfragment/v1/contentfragment"
dam.cfm.component.fileReferenceProp="fragmentPath"
dam.cfm.component.elementsProp="elementName"
dam.cfm.component.variationProp="variationName"
```
