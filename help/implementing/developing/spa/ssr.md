---
title: SPA和伺服器端演算
description: 在SPA中使用伺服器端演算(SSR)可加速頁面的初始載入，然後將進一步演算傳遞給用戶端。
translation-type: tm+mt
source-git-commit: 056fb27108d8f78acfc4658daa92912a48112f1f
workflow-type: tm+mt
source-wordcount: '1436'
ht-degree: 0%

---


# SPA和伺服器端演算{#spa-and-server-side-rendering}

單頁應用程式(SPA)可為使用者提供多樣化的動態體驗，以熟悉的方式反應和運作，通常就像原生應用程式。 [這是透過依賴用戶端在前面載入內容，然後進行繁重的使用者互動處理](introduction.md#how-does-a-spa-work) ，進而將用戶端與伺服器之間所需的通訊量減至最少，讓應用程式更具反應性。

不過，這可能會延長初始載入時間，尤其是當SPA大而內容豐富時。 為了最佳化載入時間，有些內容可在伺服器端轉譯。 使用伺服器端轉譯(SSR)可加速頁面的初始載入，並進一步將轉譯傳遞給用戶端。

## 何時使用SSR {#when-to-use-ssr}

並非所有項目都需要SSR。 雖然AEM完全支援SPA的JS SSR，但Adobe不建議針對每個專案系統實作SSR。

在決定實施SSR時，首先必須估計項目的額外複雜性、努力和成本增加的實際表現，包括長期維護。 只有當增加值明顯超過估計成本時，才應選擇SSR結構。

SSR通常在以下任一問題有明確的「是」時提供一些值：

* **SEO:** SSR是否仍需要SSR才能讓帶來流量的搜尋引擎正確建立索引？ 請記住，主要搜尋引擎爬蟲程式現在會評估JS。
* **頁面速度：** SSR是否可大幅提升實際環境中的速度，並增加整體使用體驗？

只有當這兩個問題中至少有一個問題以明確的「是」回答時，Adobe才建議實作SSR。 以下各節將說明如何使用Adobe I/O Runtime進行此項作業。

## Adobe I/O Runtime {#adobe-i-o-runtime}

如果您 [確信專案需要實作SSR](#when-to-use-ssr),Adobe建議的解決方案是使用Adobe I/O Runtime。

如需Adobe I/O Runtime的詳細資訊，請參閱

* [https://www.adobe.io/apis/experienceplatform/runtime.html](https://www.adobe.io/apis/experienceplatform/runtime.html) —— 如需服務的概觀
* [https://www.adobe.io/apis/experienceplatform/runtime/docs.html](https://www.adobe.io/apis/experienceplatform/runtime/docs.html) —— 如需平台的詳細檔案

以下各節將詳細說明如何使用Adobe I/O Runtime在兩種不同的模型中為您的SPA實施SSR:

* [AEM導向的通訊流程](#aem-driven-communication-flow)
* [Adobe I/O執行時期導向的通訊流程](#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>Adobe建議針對每個AEM環境（作者、發佈、舞台等）使用個別的Adobe I/O Runtime執行個體。

## 遠程渲染器配置 {#remote-content-renderer-configuration}

AEM必須知道可擷取遠端轉譯內容的位置。 不論您 [選擇為SSR建置何種模型，](#adobe-i-o-runtime) 都需要指定AEM如何存取此遠端轉譯服務。

這是通過RemoteContentRenderer - Configuration Factory OSGi服 **務完成的**。 在「Web控制台配置」控制台中搜索「RemoteContentRenderer」字串，網址為 `http://<host>:<port>/system/console/configMgr`。

![轉譯器設定](assets/renderer-configuration.png)

下列欄位可用於設定：

* **內容路徑模式** -規則運算式，以符合部分內容（如有必要）
* **遠端端點URL** —— 負責產生內容的端點的URL
   * 如果不在本地網路中，請使用安全的HTTPS協定。
* **其他請求標題** -要新增至傳送至遠端端點之請求的其他標題
   * 模式： `key=value`
* **請求超時** -遠程主機請求超時（以毫秒為單位）

>[!NOTE]
>
>不論您選擇實作 [AEM導向的通訊流程](#aem-driven-communication-flow) ，或 [](#adobe-i-o-runtime-driven-communication-flow) Adobe I/O Runtime導向的流程，您都必須定義遠端內容轉譯器設定。

>[!NOTE]
>
>此配置利用「遠 [程內容呈現器」](#remote-content-renderer) ，該轉換器還提供其他擴展和自定義選項。

## AEM導向的通訊流程 {#aem-driven-communication-flow}

使用SSR時，AEM中 [SPA的元件互動工作流程](introduction.md#interaction-with-the-spa-editor) ，包含在Adobe I/O Runtime上產生應用程式初始內容的階段。

1. 瀏覽器會向AEM要求SSR內容。
1. AEM會將模型張貼至Adobe I/O Runtime。
1. Adobe I/O Runtime會傳回產生的內容。
1. AEM會透過後端頁面元件的HTL範本，來支援Adobe I/O Runtime傳回的HTML。

![SSE CMS導向的AEM Adobe I/O](assets/ssr-cms-drivenaemnode-adobeio.png)

## Adobe I/O執行時期導向的通訊流程 {#adobe-i-o-runtime-driven-communication-flow}

上節說明在AEM中，AEM會執行內容的引導載入和伺服時，針對SPA的伺服器端轉譯標準和建議實作。

或者，SSR可以實現，使Adobe I/O Runtime負責引導，有效地逆轉通信流。

這兩種機型都有效，且受AEM支援。 但是，在實施特定模式之前，應先考慮各自的優缺點。

<table>
 <tbody>
  <tr>
   <th><strong>引導</strong></th>
   <th><strong>優勢</strong></th>
   <th><strong>缺點</strong></th>
  </tr>
  <tr>
   <th><strong>透過AEM</strong><br /> </th>
   <td>
    <ul>
     <li>AEM可管理視需要注入的程式庫</li>
     <li>只需在AEM上維護資源<br /> </li>
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
     <li>AEM開發人員必須透過屬性提供應用程式（例如CSS和JavaScript）所需的Clientlib資 <code><a href="/help/implementing/developing/introduction/clientlibs.md">allowProxy</a></code> 源<br /> </li>
     <li>資源必須在AEM和Adobe I/O Runtime之間同步<br /> </li>
     <li>若要啟用SPA的編寫功能，可能需要Adobe I/O Runtime的代理伺服器</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## SSR規劃 {#planning-for-ssr}

通常只需要轉換應用程式的一部分， 常見的範例是，在頁面初始載入時，會在折疊上方顯示的內容會轉譯為伺服器端。 如此可將已轉譯的內容傳送至用戶端，以節省時間。 當使用者與SPA互動時，用戶端會轉譯其他內容。

當您考慮為SPA實作伺服器端演算時，需要檢閱應用程式中需要哪些部分。

## 利用SSR技術開發SPA {#developing-an-spa-using-ssr}

SPA元件可由用戶端（在瀏覽器中）或伺服器端轉譯。 在轉譯伺服器端時，瀏覽器屬性（例如視窗大小和位置）不存在。 因此，SPA元件應該是同構的，對於它們的渲染位置不作任何假設。

若要運用SSR，您必須在AEM以及負責伺服器端轉譯的Adobe I/O Runtime上部署程式碼。 大部分的程式碼都相同，但伺服器特定的工作會有所不同。

## AEM中SSR的研究 {#ssr-for-spas-in-aem}

AEM中SSR的SPA需要Adobe I/O Runtime，這是轉換應用程式內容伺服器端的呼叫。 在應用程式的HTL中，會呼叫Adobe I/O Runtime上的資源來呈現內容。

就像AEM支援Angular和React SPA架構的現成功能一樣，Angular和React應用程式也支援伺服器端演算。 如需詳細資訊，請參閱兩個架構的NPM檔案。

## 遠端內容轉譯器 {#remote-content-renderer}

在AEM [中搭配SPA使用SSR所需的遠端內容轉譯器設定](#remote-content-renderer-configuration) ，可點選更廣泛的轉譯服務，以因應您的需求加以擴充和自訂。

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` 是OSGi服務，可擷取在遠端伺服器上轉譯的內容，例如從Adobe I/O轉譯。傳送至遠端伺服器的內容是根據傳遞的要求參數。

`RemoteContentRenderingService` 可在需要額外的內容控制時，透過互依性反轉插入自訂Sling模型或servlet。

此服務由 [RemoteContentRendererRequestHandlerServlet在內部使用](#remotecontentrendererrequesthandlerservlet)。

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

您可 `RemoteContentRendererRequestHandlerServlet` 以使用程式設計方式設定請求組態。 `DefaultRemoteContentRendererRequestHandlerImpl`，提供的預設請求處理常式實作，可讓您建立多個OSGi組態，以便將內容結構中的位置對應至遠端端點。

若要新增自訂請求處理常式，請實作 `RemoteContentRendererRequestHandler` 介面。 請務必將 `Constants.SERVICE_RANKING` component屬性設為大於100的整數，即排名 `DefaultRemoteContentRendererRequestHandlerImpl`。

```javascript
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### 配置預設處理程式的OSGi配置 {#configure-default-handler}

預設處理程式的配置必須按照「遠程內容渲染器配置」一節中 [的說明進行配置](#remote-content-renderer-configuration)。

### 遠端內容轉譯器使用 {#usage}

若要讓servlet擷取並傳回某些可插入頁面的內容：

1. 確保遠程伺服器可以訪問。
1. 將下列其中一個程式碼片段新增至AEM元件的HTL範本。
1. 或者，建立或修改OSGi配置。
1. 瀏覽您網站的內容

通常，頁面元件的HTL範本是此類功能的主要收件者。

```html
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### 需求 {#requirements}

Servlet運用Sling Model Exporter序列化元件資料。 依預設，和 `com.adobe.cq.export.json.ContainerExporter` 都 `com.adobe.cq.export.json.ComponentExporter` 支援做為Sling Model適配器。 如有必要，您可以添加類，請求應適應使用和實 `RemoteContentRendererServlet` 施類 `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`。 其他類必須擴展 `ComponentExporter`。
