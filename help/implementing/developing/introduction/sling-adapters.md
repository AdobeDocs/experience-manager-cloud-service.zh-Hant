---
title: 使用 Sling 介面卡
description: Sling提供轉接器模式，可方便翻譯實作轉接器介面的物件
exl-id: 8ffe3bbd-01fe-44c2-bf60-7a4d25a6ba2b
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 3%

---

# 使用 Sling 介面卡 {#using-sling-adapters}

[Sling](https://sling.apache.org)提供[介面卡模式](https://sling.apache.org/documentation/the-sling-engine/adapters.html)，以方便翻譯實作[介面](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29)介面的物件。 此介面提供泛型[adaptTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29)方法，將物件轉譯成作為引數傳遞的類別型別。

例如，若要將Resource物件轉譯為對應的Node物件，您只需執行下列動作即可：

```java
Node node = resource.adaptTo(Node.class);
```

## 使用案例 {#use-cases}

有以下使用案例：

* 取得實作特定的物件。

  例如，泛型[`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html)介面的JCR型實作提供對基礎JCR [`Node`](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html)的存取權。

* 需要傳遞內部前後關聯物件的物件的快速鍵建立。

  例如，以JCR為基礎的[`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html)保留對請求的[`JCR Session`](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html)的參考，而許多根據該請求工作階段工作的物件需要該參考，例如[`PageManager`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageManager.html)或[`UserManager`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/security/UserManager.html)。

* 服務的捷徑。

  罕見的情況 — `sling.getService()`也相當簡單。

### 空值傳回值 {#null-return-value}

`adaptTo()`可傳回null。

null傳回有多種原因，包括：

* 實作不支援目標型別
* 處理此情況的介面卡工廠未啟用（例如，因為遺失服務參考）
* 內部條件失敗
* 服務無法使用

請務必謹慎處理Null案例。 對於jsp呈現，如果jsp失敗導致內容空白，這是可以接受的。

### 快取 {#caching}

若要改善效能，實作可自由快取`obj.adaptTo()`呼叫傳回的物件。 如果`obj`相同，則傳回的物件也相同。

已針對所有`AdapterFactory`個案例執行此快取。

但是，沒有一般規則 — 物件可能是新例項或現有例項。 因此，這表示您無法信賴任一行為。 因此，物件在此情境中可重複使用很重要，尤其是在`AdapterFactory`內。

### 運作方式 {#how-it-works}

有多種方式可以實作`Adaptable.adaptTo()`：

* 物件本身；實作方法本身並對應至特定物件。
* [`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html)可以對應任意物件。

  物件仍必須實作`Adaptable`介面且必須延伸[`SlingAdaptable`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/adapter/SlingAdaptable.html) （這會將`adaptTo`呼叫傳遞給中央介面卡管理員）。

  此方法允許連結到現有類別（例如`Resource`）的`adaptTo`機制。

* 兩者的組合。

對於第一種情況，Java™檔案可以說明哪些`adaptTo-targets`是可能的。 不過，對於特定子類別（例如JCR型資源），此陳述式通常無法執行。 在後一種情況下，`AdapterFactory`的實施通常是套件組合私用類別的一部分，因此不會在使用者端API中公開，也不會列在Java™檔案中。 理論上來說，可以從[OSGi](/help/implementing/deploying/configuring-osgi.md)服務執行階段存取所有`AdapterFactory`實作，並檢視其「可適配」（來源和目標）組態，但無法相互對應。 最後，這取決於內部邏輯，而這必須記錄在案。 因此，請參閱此參考檔案。

## 參考 {#reference}

### Sling {#sling}

[**資源**](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html)已調整為：

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">節點</a></td>
   <td>如果是JCR節點型資源或JCR屬性，則參照節點</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Property.html">屬性</a></td>
   <td>如果是JCR屬性型資源</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Item.html">項目</a></td>
   <td>如果是JCR型資源（節點或屬性）</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Map.html">地圖</a></td>
   <td>如果是JCR節點型資源（或其他支援值的資源對應），則傳回屬性的對應</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/ValueMap.html">值圖</a></td>
   <td>如果屬性是以JCR節點為基礎的資源（或其他支援值的資源對應），則傳回方便使用的屬性對應。 也可以使用<br /> <code><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/ResourceUtil.html">ResourceUtil.getValueMap(Resource)</a></code> （處理null大小寫等）來達成（更簡單）</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">InheritanceValueMap</a></td>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a>的延伸模組，可在尋找屬性時考慮資源的階層</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/ModifiableValueMap.html">ModifiableValueMap</a></td>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a>的延伸模組，可讓您修改該節點上的屬性</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/io/InputStream.html">輸入資料流</a></td>
   <td>傳回檔案資源的二進位內容（如果是JCR節點型資源，且節點型別是<code>nt:file</code>或<code>nt:resource</code>；如果是bundle資源；如果是file system資源，則傳回檔案內容）。 或者，會傳回二進位JCR屬性資源的資料。</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/net/URL.html">URL</a></td>
   <td>傳回資源的URL （若此節點為JCR節點型資源，則傳回該節點的存放庫URL；若為套裝資源，則傳回jar套裝URL；若為檔案系統資源，則傳回檔案URL）</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/io/File.html">檔案</a></td>
   <td>如果是檔案系統資源</td>
  </tr>
  <tr>
   <td><a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/api/scripting/SlingScript.html">SlingScript</a></td>
   <td>如果資源是指令碼（例如jsp檔案），其指令碼引擎已在sling中註冊</td>
  </tr>
  <tr>
   <td><a href="https://www.oracle.com/java/technologies/servlet-technology.html">Servlet</a></td>
   <td>如果資源是向sling註冊指令碼引擎的指令碼（例如jsp檔案），或是servlet資源</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/String.html">String</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Boolean.html">Boolean</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Long.html">Long</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Double.html">Double</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Calendar.html">行事曆</a><br /> <a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">值</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/String.html">String[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Boolean.html">Boolean[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Long.html">Long[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Calendar.html">行事曆[]</a><br /> <a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">值[]</a></td>
   <td>如果是以JCR屬性為基礎的資源，則傳回值（且值符合）</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>如果是JCR節點型資源</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/Page.html">頁面</a></td>
   <td>如果它是JCR節點型資源，而且節點是<code>cq:Page</code> （或<code>cq:PseudoPage</code>）</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/components/Component.html">元件</a></td>
   <td>如果它是<code>cq:Component</code>節點資源</td>
  </tr>  
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/designer/Design.html">設計</a></td>
   <td>如果它是設計節點(<code>cq:Page</code>)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/Template.html">範本</a></td>
   <td>如果它是<code>cq:Template</code>節點資源</td>
  </tr>  
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/msm/api/Blueprint.html">藍圖</a></td>
   <td>如果它是<code>cq:Template</code>節點資源</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/dam/api/Asset.html">資產</a></td>
   <td>如果是dam：Asset節點資源</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/dam/api/Rendition.html">轉譯</a></td>
   <td>如果是dam：Asset轉譯（nt：file，在dam：Assert的轉譯資料夾下）</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/Tag.html">標記</a></td>
   <td>如果它是<code>cq:Tag</code>節點資源</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/security/UserManager.html">使用者管理員</a></td>
   <td>根據JCR工作階段，如果這是JCR型資源，而且使用者有權存取UserManager</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">可授權項目</a></td>
   <td>「可授權專案」是「使用者」和「群組」的共同基礎介面</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/jackrabbit/api/security/user/User.html">使用者</a></td>
   <td>使用者是可驗證及模擬的特殊可授權專案</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/SimpleSearch.html">Simplesearch</a></td>
   <td>在資源底下搜尋(或使用setSearchIn()) （如果它是以JCR為基礎的資源）</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/workflow/status/WorkflowStatus.html">工作流程狀態</a></td>
   <td>特定頁面/工作流程裝載節點的工作流程狀態</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/replication/ReplicationStatus.html">復寫狀態</a></td>
   <td>指定資源或其jcr：content子節點的復寫狀態（請先核取）</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/connector/ConnectorResource.html">聯結器資源</a></td>
   <td>如果是JCR節點型資源，則傳回適合特定型別的聯結器資源</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/contentsync/config/package-summary.html">設定</a></td>
   <td>如果它是<code>cq:ContentSyncConfig</code>節點資源</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/contentsync/config/package-summary.html">ConfigEntry</a></td>
   <td>如果它在<code>cq:ContentSyncConfig</code>節點資源之下</td>
  </tr>
 </tbody>
</table>

[**ResourceResolver**](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/ResourceResolver.html)適配：

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html">工作階段</a></td>
   <td>請求的JCR工作階段，如果是JCR型資源解析器（預設）</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageManager.html">PageManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/components/ComponentManager.html">元件管理員</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/designer/Designer.html">Designer</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/dam/api/AssetManager.html">Assetmanager</a></td>
   <td>根據JCR工作階段，如果是JCR型資源解析程式</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/TagManager.html">標籤管理員</a></td>
   <td>根據JCR工作階段，如果是JCR型資源解析程式</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/jackrabbit/api/security/user/UserManager.html">使用者管理員</a></td>
   <td>UserManager提供可授權物件（即使用者和群組）的存取權及維護方法。 UserManager繫結至特定工作階段
   </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">可授權</a> </td>
   <td>目前使用者</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/jackrabbit/api/security/user/User.html">使用者</a><br /> </td>
   <td>目前使用者</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/QueryBuilder.html">Querybuilder</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html">Externalizer</a></td>
   <td>用於將絕對URL外部化，即使沒有要求物件<br /> </td>
  </tr>
 </tbody>
</table>

[**SlingHttpServletRequest**](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/SlingHttpServletRequest.html)已調整為：

尚未有目標，但實作可調整的，而且可以在自訂AdapterFactory中作為來源使用。

[**SlingHttpServletResponse**](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/SlingHttpServletResponse.html)已調整為：

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/org/xml/sax/ContentHandler.html">ContentHandler</a><br /> (XML)</td>
   <td>如果這是Sling重寫程式回應</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

**[頁面](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/Page.html)**&#x200B;已調整為：

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html">Resource</a><br /> </td>
   <td>頁面的資源。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>已標示的資源(==此)。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">節點</a></td>
   <td>頁面的節點。</td>
  </tr>
  <tr>
   <td>...</td>
   <td>頁面資源可適應的所有內容。</td>
  </tr>
 </tbody>
</table>

**[元件](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/components/Component.html)**&#x200B;已調整：

| [Resource](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html) | 元件的資源。 |
|---|---|
| [LabeledResource](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/LabeledResource.html) | 已標示的資源(==此)。 |
| [節點](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 元件的節點。 |
| ... | 元件資源可適應的所有專案。 |

**[範本](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/Template.html)**&#x200B;適配：

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html">資源</a><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html"><br /> </a></td>
   <td>範本的資源。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>已標示的資源(==此)。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">節點</a></td>
   <td>此範本的節點。</td>
  </tr>
  <tr>
   <td>...</td>
   <td>可調整範本資源的所有內容。</td>
  </tr>
 </tbody>
</table>

#### 安全性 {#security}

**可授權**、**使用者**&#x200B;和&#x200B;**群組**&#x200B;適配：

| [節點](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 傳回使用者/群組主節點。 |
|---|---|
| [ReplicationStatus](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/replication/ReplicationStatus.html) | 傳回使用者/群組主節點的復寫狀態。 |

#### DAM {#dam}

**資產**&#x200B;已調整為：

| [Resource](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html) | 資產的資源。 |
|---|---|
| [節點](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 資產的節點。 |
| ... | 資產資源可適應的所有內容。 |

#### 標記 {#tagging}

**標籤**&#x200B;已調整為：

| [Resource](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html) | 標籤的資源。 |
|---|---|
| [節點](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 標籤的節點。 |
| ... | 標籤的資源可適應的所有內容。 |

#### 其他 {#other}

此外，Sling / JCR / OCM也為自訂OCM （[物件內容對應](https://jackrabbit.apache.org/jcr/object-content-mapping.html)）物件提供[`AdapterFactory`](https://sling.apache.org/documentation/the-sling-engine/adapters.html)。
