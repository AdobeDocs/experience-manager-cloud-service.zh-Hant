---
title: SPA和伺服器端轉譯
description: 在SPA中使用伺服器端轉譯(SSR)可以加速頁面的初始載入，然後將進一步的轉譯傳遞給使用者端。
exl-id: be409559-c7ce-4bc2-87cf-77132d7c2da1
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1492'
ht-degree: 0%

---

# SPA和伺服器端轉譯{#spa-and-server-side-rendering}

單頁應用程式(SPA)可為使用者提供豐富的動態體驗，以熟悉的方式反應和行為，通常就像原生應用程式一樣。 [此功能是藉由依賴使用者端先載入內容，然後再處理使用者互動來達成](introduction.md#how-does-a-spa-work)。 此程式可將使用者端與伺服器之間所需的通訊量降至最低，讓應用程式更具反應性。

不過，此程式可能會導致較長的初始載入時間，尤其是當SPA較大且內容豐富時。 為了最佳化載入時間，部分內容可以在伺服器端轉譯。 使用伺服器端轉譯(SSR)可以加速頁面的初始載入，然後將進一步的轉譯傳遞給使用者端。

## 何時使用SSR {#when-to-use-ssr}

並非所有專案都需要SSR。 雖然AEM完全支援適用於SPA的JS SSR，但Adobe不建議將其系統地實作到每個專案。

決定實作SSR時，您必須先估計增加SSR對專案實際代表的其他複雜性、工作量和成本，包括長期維護。 只有在增加值明顯超過預估成本時，才應選擇SSR架構。

SSR通常會在下列任一問題明確為「是」時提供某些值：

* **SEO：**&#x200B;您的網站是否仍需要SSR才能由帶來流量的搜尋引擎正確編制索引？ 請記住，主要搜尋引擎編目程式現在會評估JS。
* **頁面速度：** SSR是否能在真實環境中提供可衡量的速度提升，並增加整體使用者體驗？

只有當這兩個問題中至少有一個問題得到明確的「是」回答時，Adobe才會建議實作SSR。 以下章節說明如何使用[App Builder](https://developer.adobe.com/app-builder)中的Adobe I/O Runtime執行此工作。

## Adobe I/O Runtime {#adobe-i-o-runtime}

如果您[確信您的專案需要實作SSR](#when-to-use-ssr)，Adobe建議的解決方案是使用Adobe I/O Runtime。

如需Adobe I/O Runtime的詳細資訊，請參閱下列內容：

* [https://developer.adobe.com/runtime](https://developer.adobe.com/runtime) — 概述App Builder的執行階段功能
* [https://developer.adobe.com/app-builder](https://developer.adobe.com/app-builder) — 如需完整App Builder產品的詳細資訊
* [https://developer.adobe.com/runtime/docs/](https://developer.adobe.com/runtime/docs) — 如需詳細檔案

以下章節詳細說明如何使用Adobe I/O Runtime在兩種不同的模型中為您的SPA實作SSR：

* [AEM導向的通訊流程](#aem-driven-communication-flow)
* [Adobe I/O Runtime導向的通訊流程](#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>Adobe建議每個環境使用個別的Adobe I/O Runtime工作區（預備、生產、測試等）。 如此一來，典型系統開發生命週期(SDLC)模式便可以適用於部署至不同環境的單一應用程式不同版本。 如需詳細資訊，請參閱App Builder應用程式的[CI/CD](https://developer.adobe.com/app-builder/docs/guides/deployment/ci_cd_for_firefly_apps/)。
>
>除非每個執行個體型別的執行階段實施有所差異，否則不需要為每個執行個體（作者、發佈）使用個別的工作區。

>[!NOTE]
>
>Cloud Manager不支援部署至Adobe I/O Runtime。 因此，您必須設定自己的基礎結構，將SSR程式碼部署至Adobe I/O Runtime。

## 遠端轉譯器設定 {#remote-content-renderer-configuration}

AEM必須知道可在何處擷取遠端呈現的內容。 無論您選擇為SSR實作哪種[模型，](#adobe-i-o-runtime)您必須指定給AEM如何存取此遠端轉譯服務。

此服務是透過&#x200B;**RemoteContentRenderer - Configuration Factory OSGi服務**&#x200B;完成的。 在`http://<host>:<port>/system/console/configMgr`的Web主控台組態主控台中搜尋字串「RemoteContentRenderer」。

![轉譯器組態](assets/renderer-configuration.png)

下列欄位可供設定使用：

* **內容路徑模式** — 符合部分內容的規則運算式（如有必要）
* **遠端端點URL** — 負責產生內容的端點URL
   * 若不在本機網路中，請使用安全的HTTPS通訊協定。
* **其他要求標頭** — 要新增至傳送至遠端端點之要求的其他標頭
   * 模式： `key=value`
* **要求逾時** — 遠端主機要求逾時（毫秒）

>[!NOTE]
>
>無論您選擇實作[AEM導向的通訊流程](#aem-driven-communication-flow)或[Adobe I/O Runtime導向的流程](#adobe-i-o-runtime-driven-communication-flow)，您都必須定義遠端內容轉譯器組態。

>[!NOTE]
>
>此設定使用[遠端內容轉譯器](#remote-content-renderer)，它具有其他可用的擴充和自訂選項。

## AEM導向的通訊流程 {#aem-driven-communication-flow}

使用SSR時，AEM中SPA的[元件互動工作流程](introduction.md#interaction-with-the-spa-editor)包含在Adobe I/O Runtime上產生應用程式初始內容的階段。

1. 瀏覽器向AEM要求SSR內容。
1. AEM會將模型發佈至Adobe I/O Runtime。
1. Adobe I/O Runtime會傳回產生的內容。
1. AEM透過後端頁面元件的HTL範本，提供Adobe I/O Runtime傳回的HTML。

![SSE CMS驅動的AEMAdobe I/O](assets/ssr-cms-drivenaemnode-adobeio.png)

## Adobe I/O Runtime導向的通訊流程 {#adobe-i-o-runtime-driven-communication-flow}

上一節將說明有關AEM中SPA之伺服器端轉譯的標準與建議實作，AEM在此會執行內容的自訂與提供。

或者，您也可以實作SSR，讓Adobe I/O Runtime負責啟動程式，有效反轉通訊流程。

這兩種模式都有效，並受到AEM支援。 不過，在實作特定模型之前，您應該先考量各別的優缺點。

<table>
 <tbody>
  <tr>
   <th><strong>Bootstrapping</strong></th>
   <th><strong>優點</strong></th>
   <th><strong>缺點</strong></th>
  </tr>
  <tr>
   <th><strong>透過AEM</strong><br /> </th>
   <td>
    <ul>
     <li>AEM會視需要管理插入程式庫</li>
     <li>僅在AEM上維護資源<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>SPA開發人員可能不熟悉<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>透過Adobe I/O Runtime<br /> </strong></th>
   <td>
    <ul>
     <li>SPA開發人員更熟悉<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>應用程式所需的Clientlib資源(例如CSS和JavaScript)必須由AEM開發人員透過<code><a href="/help/implementing/developing/introduction/clientlibs.md">allowProxy</a></code>屬性<br />提供 </li>
     <li>資源必須在AEM與Adobe I/O Runtime<br />之間同步 </li>
     <li>若要啟用SPA的製作功能，可能需要Adobe I/O Runtime的Proxy伺服器</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 計畫SSR {#planning-for-ssr}

一般而言，只有部分應用程式必須呈現在伺服器端。 常見的範例是，在頁面初始載入時，顯示在摺疊上方的內容會在伺服器端轉譯。 此程式會將已轉譯的內容傳遞給使用者端，以節省時間。 當使用者與SPA互動時，其他內容會由使用者端轉譯。

當您考慮為SPA實作伺服器端轉譯時，請檢閱應用程式的哪些部分有必要。

## 使用SSR開發SPA {#developing-an-spa-using-ssr}

SPA元件可由使用者端（在瀏覽器中）或伺服器端轉譯。 在轉譯伺服器端時，不會出現瀏覽器屬性，例如視窗大小和位置。 因此，SPA元件應同構，不對其演算位置做任何假設。

若要使用SSR，您必須在AEM和Adobe I/O Runtime上部署程式碼，由伺服器端轉譯。 大部分的程式碼都相同，但伺服器特定的工作有所不同。

## AEM中SPA的SSR {#ssr-for-spas-in-aem}

AEM中適用於SPA的SSR需要Adobe I/O Runtime，此模組會在轉譯應用程式內容伺服器端時呼叫。 在應用程式的HTL中，會呼叫Adobe I/O Runtime上的資源來呈現內容。

就像AEM可立即支援Angular和React SPA架構一樣，Angular和React應用程式也支援伺服器端轉譯。 如需詳細資訊，請參閱這兩個架構的NPM檔案。

## 遠端內容轉譯器 {#remote-content-renderer}

在AEM中搭配使用SSR與SPA所需的[遠端內容轉譯器組態](#remote-content-renderer-configuration)，會進入更一般的轉譯服務，您可以擴充和自訂這些服務，以符合您的需求。

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService`用於擷取遠端伺服器上轉譯之內容的OSGi服務，例如從Adobe I/O。傳送至遠端伺服器的內容是根據傳遞的請求引數。

`RemoteContentRenderingService`當需要額外的內容操作時，可由相依性反轉插入自訂Sling模型或servlet中。

此服務是由[RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet)在內部使用。

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

`RemoteContentRendererRequestHandlerServlet`可用來以程式設計方式設定要求組態。 `DefaultRemoteContentRendererRequestHandlerImpl`是提供的預設要求處理常式實作，可讓您建立多個OSGi設定，以便將內容結構中的位置對應到遠端端點。

若要新增自訂要求處理常式，請實作`RemoteContentRendererRequestHandler`介面。 請務必將`Constants.SERVICE_RANKING`元件屬性設為大於100的整數，這是`DefaultRemoteContentRendererRequestHandlerImpl`的排名。

```javascript
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### 設定預設處理常式的OSGi設定 {#configure-default-handler}

預設處理常式的組態必須依照區段[遠端內容轉譯器組態](#remote-content-renderer-configuration)中的說明進行設定。

### 遠端內容轉譯器使用情形 {#usage}

讓servlet擷取並傳回一些插入頁面的內容：

1. 確定您的遠端伺服器可以存取。
1. 將下列其中一個片段新增至AEM元件的HTL範本。
1. 選擇性地建立或修改OSGi設定。
1. 瀏覽網站內容

通常，頁面元件的HTL範本是這類功能的主要收件者。

```html
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### 要求 {#requirements}

此servlet會使用Sling模型匯出工具來序列化元件資料。 依預設，`com.adobe.cq.export.json.ContainerExporter`和`com.adobe.cq.export.json.ComponentExporter`都支援作為Sling模型介面卡。 如有必要，您可以新增類別，讓請求能夠調整為使用`RemoteContentRendererServlet`並實作`RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`。 其他類別必須擴充`ComponentExporter`。
