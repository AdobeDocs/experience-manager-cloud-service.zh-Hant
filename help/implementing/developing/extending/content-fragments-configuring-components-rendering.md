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

有幾個 [高級服務](#definition-of-advanced-services-that-need-configuration) 與內容片段的呈現相關。 要使用這些服務，此類元件的資源類型必須使內容片段框架知道它們本身。

通過配置 [OSGi服務 — 內容片段元件配置](#osgi-service-content-fragment-component-configuration)。

在以下情況下需要此資訊：

* 您需要實施您自己的基於內容片段的元件，
* 需要利用先進服務。

建議使用核心元件。

>[!CAUTION]
>
>* **如果你不需要 [高級服務](#definition-of-advanced-services-that-need-configuration)** 如下所述，您可以忽略此配置。
>
>* **擴展或使用出廠設定元件時**，建議不要更改OSGi配置。
>
>* **您可以從頭開始編寫僅使用內容片段API的元件，但不提供高級服務**。 但是，在這種情況下，您必須開發元件，以便處理相應的處理。
>
>因此，建議使用核心元件。

## 需要配置的高級服務的定義 {#definition-of-advanced-services-that-need-configuration}

需要註冊元件的服務包括：

* 正確確定發佈期間的依賴關係（即，如果碎片和模型自上次發佈後發生更改，則可以隨頁面自動發佈它們）。
* 支援全文搜索中的內容片段。
* 管理/處理 *內容。*
* 管理/處理 *混合媒體資產。*
* 引用片段的Dispatcher刷新（如果包含片段的頁被重新發佈）。
* 使用基於段落的渲染。

如果您需要這些功能中的一個或多個，則（通常）使用現成的高級服務會更容易，而不是從頭開始開發。

## OSGi服務 — 內容片段元件配置 {#osgi-service-content-fragment-component-configuration}

配置需要綁定到OSGi服務 **內容片段元件配置**:

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>請參閱 [OSGi配置](/help/implementing/deploying/overview.md#osgi-configuration) 的上界。

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
   <td>要註冊的資源類型；例如 <br /> <p><span class="cmp-examples-demo__property-value"><code>core/wcm/components/contentfragment/v1/contentfragment</code></code></p> </td>
  </tr>
  <tr>
   <td><strong>引用屬性</strong></td>
   <td><code>dam.cfm.component.fileReferenceProp</code></td>
   <td>包含對片段的引用的屬性的名稱；例如 <code>fragmentPath</code> 或 <code>fileReference</code></td>
  </tr>
  <tr>
   <td><strong>元素屬性</strong></td>
   <td><code>dam.cfm.component.elementsProp</code></td>
   <td>包含要呈現的元素名稱的屬性的名稱；例如<code>elementName</code></td>
  </tr>
  <tr>
   <td><strong>變數屬性</strong><br /> </td>
   <td><code>dam.cfm.component.variationProp</code></td>
   <td>包含要呈現的變體名稱的屬性的名稱；例如<code>variationName</code></td>
  </tr>
 </tbody>
</table>

對於某些功能，您的元件必須遵守預定義的約定。 下表詳細說明了每個段落需要由元件定義的屬性(即 `jcr:paragraph` 使服務能夠正確檢測和處理它們。

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
   <td><p>一個字串屬性，它定義在中時如何輸出段落 <em>單元渲染模式</em>。</p> <p>值:</p>
    <ul>
     <li><code>all</code> :呈現所有段落</li>
     <li><code>range</code> :呈現由 <code>paragraphRange</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphRange</code></td>
   <td><p>一個字串屬性，它定義要輸出的段落範圍（如果在） <em>單元渲染模式</em>。</p> <p>格式:</p>
    <ul>
     <li><code>1</code> 或 <code>1-3</code> 或 <code>1-3;6;7-8</code> 或 <code>*-3;5-*</code>
     <ul>
       <li><code>-</code> 範圍指示器</li>
       <li><code>;</code> 清單分隔符</li>
       <li><code>*</code> 通配符</li>
     </ul>
     </li>
     <li>僅計算 <code>paragraphScope</code> 設定為 <code>range</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphHeadings</code></td>
   <td>一個布爾屬性，它定義標題(例如， <code>h1</code>。 <code>h2</code>。 <code>h3</code>)作為段落(<code>true</code>)或不(<code>false</code>)</td>
  </tr>
 </tbody>
</table>

## 範例 {#example}

作為示例，請參見以下(在現成實例上AEM):

```
/apps/core/wcm/config/com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl-core-comp-v1.config
```

這包括：

```
dam.cfm.component.resourceType="core/wcm/components/contentfragment/v1/contentfragment"
dam.cfm.component.fileReferenceProp="fragmentPath"
dam.cfm.component.elementsProp="elementName"
dam.cfm.component.variationProp="variationName"
```
