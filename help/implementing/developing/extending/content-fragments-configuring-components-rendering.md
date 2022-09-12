---
title: 轉譯專用內容片段設定元件
description: 轉譯專用內容片段設定元件
exl-id: 6606dc3b-f1b8-4941-8fd0-f69cbd414afa
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 6%

---

# 轉譯專用內容片段設定元件{#content-fragments-configuring-components-for-rendering}

有幾個 [進階服務](#definition-of-advanced-services-that-need-configuration) 與內容片段的轉譯相關。 若要使用這些服務，此類元件的資源類型必須讓內容片段架構知道。

這可透過設定 [OSGi服務 — 內容片段元件設定](#osgi-service-content-fragment-component-configuration).

下列情況下需要此資訊：

* 您需要實作自己的內容片段型元件，
* 需要利用先進的服務。

建議使用核心元件。

>[!CAUTION]
>
>* **如果您不需要 [進階服務](#definition-of-advanced-services-that-need-configuration)** 如下所述，您可以忽略此配置。
>
>* **延伸或使用現成可用的元件時**，不建議變更OSGi設定。
>
>* **您可以從頭開始撰寫僅使用內容片段API的元件，不需進階服務**. 但在此情況下，您必須開發元件，以便處理適當的處理。
>
>因此，建議使用核心元件。

## 需要配置的高級服務的定義 {#definition-of-advanced-services-that-need-configuration}

需要註冊元件的服務包括：

* 在發佈期間正確判斷相依性（亦即，如果片段和模型自上次發佈以來已變更，則可以透過頁面自動發佈）。
* 支援全文搜尋的內容片段。
* 管理/處理 *內容。*
* 管理/處理 *混合媒體資產。*
* 已參照片段的Dispatcher排清（如果包含片段的頁面已重新發佈）。
* 使用段落式轉譯。

如果您需要其中一或多個功能，則（通常）使用現成可用的進階服務會比從頭開發更容易。

## OSGi服務 — 內容片段元件設定 {#osgi-service-content-fragment-component-configuration}

配置需要綁定到OSGi服務 **內容片段元件設定**:

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>請參閱 [OSGi配置](/help/implementing/deploying/overview.md#osgi-configuration) 以取得詳細資訊。

例如：

![OSGi設定內容片段元件設定](assets/cf-component-configuration-osgi.png)

OSGi設定為：

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
   <td>要註冊的資源類型；例如 <br /> <p><span class="cmp-examples-demo__property-value"><code>core/wcm/components/contentfragment/v1/contentfragment</code></code></p> </td>
  </tr>
  <tr>
   <td><strong>參考屬性</strong></td>
   <td><code>dam.cfm.component.fileReferenceProp</code></td>
   <td>包含片段參考的屬性名稱；例如 <code>fragmentPath</code> 或 <code>fileReference</code></td>
  </tr>
  <tr>
   <td><strong>Element(s)屬性</strong></td>
   <td><code>dam.cfm.component.elementsProp</code></td>
   <td>包含要呈現的元素名稱的屬性名稱；例如<code>elementName</code></td>
  </tr>
  <tr>
   <td><strong>變數屬性</strong><br /> </td>
   <td><code>dam.cfm.component.variationProp</code></td>
   <td>包含要呈現的變數名稱的屬性名稱；例如<code>variationName</code></td>
  </tr>
 </tbody>
</table>

對於某些功能，您的元件必須遵循預先定義的慣例。 下表詳細說明了需要由元件為每個段落(即 `jcr:paragraph` （適用於每個元件例項），讓服務能夠正確偵測和處理。

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
   <td><p>字串屬性，定義如果在中，如何輸出段落 <em>單一元素演算模式</em>.</p> <p>值:</p>
    <ul>
     <li><code>all</code> :轉譯所有段落</li>
     <li><code>range</code> :呈現提供的段落範圍 <code>paragraphRange</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphRange</code></td>
   <td><p>字串屬性，定義要輸出的段落範圍(若為 <em>單一元素演算模式</em>.</p> <p>格式:</p>
    <ul>
     <li><code>1</code> 或 <code>1-3</code> 或 <code>1-3;6;7-8</code> 或 <code>*-3;5-*</code>
     <ul>
       <li><code>-</code> 範圍指標</li>
       <li><code>;</code> 清單分隔符</li>
       <li><code>*</code> 萬用字元</li>
     </ul>
     </li>
     <li>只有 <code>paragraphScope</code> 設為 <code>range</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphHeadings</code></td>
   <td>一個布林值屬性，定義if標題(例如 <code>h1</code>, <code>h2</code>, <code>h3</code>)會計為段落(<code>true</code>)或否(<code>false</code>)</td>
  </tr>
 </tbody>
</table>

## 範例 {#example}

例如，請參閱下列內容(在現成可用的AEM例項上):

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
