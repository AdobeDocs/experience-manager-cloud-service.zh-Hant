---
title: 內容片段設定要轉譯的元件
description: 內容片段設定要轉譯的元件
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14

---


# 內容片段設定要轉譯的元件{#content-fragments-configuring-components-for-rendering}

有數項進 [階服務](#definition-of-advanced-services-that-need-configuration) ，與轉換內容片段相關。 要使用這些服務，此類元件的資源類型必須使內容片段框架自己知道。

這是通過配置 [OSGi服務——內容片段元件配置來完成的](#osgi-service-content-fragment-component-configuration)。

在下列情況下，需要此資訊：

* 您需要實作您自己的內容片段元件，
* 需要運用進階服務。

不過，建議使用核心元件。

>[!CAUTION]
>
>* **如果您不需要下面所述[的進階服務](#definition-of-advanced-services-that-need-configuration)**，則可忽略此設定。
   >
   >
* **When you are extending or using the out-of-the-box component(s)**, it is not recommended to change the OSGi configuration.
   >
   >
* **You can write a component from scratch that uses the Content Fragments API only, with no advanced services**. 不過，在這種情況下，您必須開發元件，以便處理適當的處理。
>
>
因此，建議使用核心元件。

## 需要配置的高級服務的定義 {#definition-of-advanced-services-that-need-configuration}

需要註冊元件的服務包括：

* 在發佈期間正確判斷相依性（即，如果片段和模型自上次發佈後已變更，請確定它們可自動與頁面一起發佈）。
* 支援全文搜尋的內容片段。
* 管理／處理 *中間內容。*
* 管理／處理混 *合媒體資產。*
* Dispatcher flush for referenced fragments(if a page containing a fragment is re-published)。
* Using paragraph-based rendering.

如果您需要其中一項或多項功能，則（通常）使用現成可用的進階服務會比較容易，而不是從頭開發。

## OSGi服務——內容片段元件配置 {#osgi-service-content-fragment-component-configuration}

配置需要綁定到OSGi服務內 **容片段元件配置**:

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>如需詳 [細資訊，請參閱](/help/implementing/deploying/overview.md#osgi-configuration) OSGi設定。

例如：

![OSGi配置內容片段元件配置](assets/cf-component-configuration-osgi.png)

OSGi配置為：

<table>
 <thead>
  <tr>
   <td>標籤</td>
   <td>OSGi配置<br /> </td>
   <td>說明</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><strong>資源類型</strong></td>
   <td><code>dam.cfm.component.resourceType</code></td>
   <td>要註冊的資源類型；例如， <br /> <p><span class="cmp-examples-demo__property-value"><code>core/wcm/components/contentfragment/v1/contentfragment</code></code></p> </td>
  </tr>
  <tr>
   <td><strong>參考屬性</strong></td>
   <td><code>dam.cfm.component.fileReferenceProp</code></td>
   <td>包含對片段的引用的屬性的名稱；例如 <code>fragmentPath</code> <code>fileReference</code></td>
  </tr>
  <tr>
   <td><strong>元素屬性</strong></td>
   <td><code>dam.cfm.component.elementsProp</code></td>
   <td>包含要渲染的元素名稱的屬性的名稱；例如，<code>elementName</code></td>
  </tr>
  <tr>
   <td><strong>變數屬性</strong><br /> </td>
   <td><code>dam.cfm.component.variationProp</code></td>
   <td>包含要呈現的變數名稱的屬性名稱；例如，<code>variationName</code></td>
  </tr>
 </tbody>
</table>

對於某些功能，您的元件必須遵循預先定義的慣例。 下表詳細說明了元件需要為每個段落（即每個元件實例）定義的屬性，以便服務能夠正確檢測和處理這些屬性 `jcr:paragraph` 。

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
   <td><p>字串屬性，定義在單一元素演算模式下如何輸 <em>出段落</em>。</p> <p>值:</p>
    <ul>
     <li><code>all</code> :來呈現所有段落</li>
     <li><code>range</code> :來轉換 <code>paragraphRange</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphRange</code></td>
   <td><p>字串屬性，定義在單一元素演算模式中要輸出的 <em>段落範圍</em>。</p> <p>格式:</p>
    <ul>
     <li><code>1</code> 或 <code>1-3</code> 或 <code>1-3;6;7-8</code> 或 <code>*-3;5-*</code>
     <ul>
       <li><code>-</code> 範圍指示符</li>
       <li><code>;</code> 清單分隔符</li>
       <li><code>*</code> wildcard</li>
     </ul>
     </li>
     <li>只有設為 <code>paragraphScope</code> 時才會評估 <code>range</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphHeadings</code></td>
   <td>一種布林屬性，定義標題( <code>h1</code>例如 <code>h2</code>, <code>h3</code>,)是否計為段落(<code>true</code>)<code>false</code></td>
  </tr>
 </tbody>
</table>

## 例如 {#example}

例如，請參閱下列（在現成可用的AEM例項上）:

```
/apps/core/wcm/config/com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl-core-comp-v1.config
```

其中包含：

```
dam.cfm.component.resourceType="core/wcm/components/contentfragment/v1/contentfragment"
dam.cfm.component.fileReferenceProp="fragmentPath"
dam.cfm.component.elementsProp="elementName"
dam.cfm.component.variationProp="variationName"
```

