---
title: SPA和伺服器端轉譯
description: 在SPA中使用伺服器端轉譯(SSR)可加速頁面的初始載入，然後將進一步轉譯傳遞至用戶端。
exl-id: be409559-c7ce-4bc2-87cf-77132d7c2da1
source-git-commit: 4965bd30c02536efb81a26fff8da6e5f75dbfae4
workflow-type: tm+mt
source-wordcount: '1502'
ht-degree: 0%

---

# SPA和伺服器端轉譯{#spa-and-server-side-rendering}

單頁應用程式(SPA)可為使用者提供豐富的動態體驗，以熟悉的方式回應和運作，通常就像原生應用程式。 [這是通過依靠客戶端在前面載入內容，然後進行用戶交互的重](introduction.md#how-does-a-spa-work) 擔，從而最小化客戶端和伺服器之間需要的通信量，使應用更加被動。

不過，這可能會導致較長的初始載入時間，尤其是如果SPA很大且內容豐富。 為了最佳化載入時間，某些內容可在伺服器端轉譯。 使用伺服器端轉譯(SSR)可以加速頁面的初始載入，然後將轉譯傳遞給用戶端。

## 何時使用SSR {#when-to-use-ssr}

並非所有項目都需要SSR。 雖然AEM完全支援SPA適用的JS SSR，但Adobe不建議針對每個專案系統實作。

在決定實施SSR時，首先必須估計SSR的實際代表是什麼額外的複雜性、工作量和成本增加，包括長期維護。 只有當增值明顯超過估計成本時，才應選擇SSR架構。

SSR通常在下列任一問題都有明確的「是」時提供一些值：

* **SEO:** 您的網站是否仍需要SSR才能由帶來流量的搜尋引擎正確編列索引？請記住，主要搜尋引擎編目程式現在會評估JS。
* **頁面速度：** SSR是否能在實際環境中大幅提升速度，並為整體使用者體驗增添新元素？

只有在這兩個問題中至少有一個以明確的「是」回答，您的專案才會Adobe建議實作SSR。 以下各節將說明如何使用Adobe I/O Runtime執行此作業。

## Adobe I/O Runtime {#adobe-i-o-runtime}

如果您[確信您的專案需要實作SSR](#when-to-use-ssr)，則Adobe的建議解決方案是使用Adobe I/O Runtime。

如需Adobe I/O Runtime的詳細資訊，請參閱

* [https://www.adobe.io/apis/experienceplatform/runtime.html](https://www.adobe.io/apis/experienceplatform/runtime.html)  — 此服務的概觀
* [https://www.adobe.io/apis/experienceplatform/runtime/docs.html](https://www.adobe.io/apis/experienceplatform/runtime/docs.html)  — 如需有關平台的詳細檔案

以下幾節將詳細說明如何使用Adobe I/O Runtime，在兩種不同的模型中為SPA實作SSR:

* [AEM導向的通訊流程](#aem-driven-communication-flow)
* [Adobe I/O Runtime驅動的通訊流](#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>Adobe建議每個環境（預備、生產、測試等）分別使用Adobe I/O Runtime工作區。 這允許典型的系統開發生命週期(SDLC)模式，將不同版本的單個應用程式部署到不同的環境。 如需詳細資訊，請參閱適用於Project Firefly Applications](https://www.adobe.io/apis/experienceplatform/project-firefly/docs.html#!AdobeDocs/project-firefly/master/guides/ci_cd_for_firefly_apps.md)的檔案[CI/CD 。
>
>每個例項（製作、發佈）不需要個別的工作區，除非每個例項類型在執行階段實施中有差異。

## 遠程渲染器配置{#remote-content-renderer-configuration}

AEM必須知道可在何處擷取遠端轉譯的內容。 無論您選擇為SSR實作哪個模型[，都需要指定](#adobe-i-o-runtime)以AEM如何存取此遠端轉譯服務。

這是通過&#x200B;**RemoteContentRenderer - Configuration Factory OSGi服務**&#x200B;完成的。 在位於`http://<host>:<port>/system/console/configMgr`的Web控制台配置控制台中搜索字串&quot;RemoteContentRenderer&quot;。

![轉譯器配置](assets/renderer-configuration.png)

下列欄位適用於設定：

* **內容路徑模式**  — 必要時，用來比對部分內容的規則運算式
* **遠端端點URL**  — 負責產生內容之端點的URL
   * 如果本地網路中沒有，請使用安全的HTTPS協定。
* **其他請求標題**  — 要新增至傳送至遠端端點之請求的其他標題
   * 模式：`key=value`
* **請求超時**  — 遠程主機請求超時（毫秒）

>[!NOTE]
>
>無論您選擇實作[AEM導向的通訊流](#aem-driven-communication-flow)或[Adobe I/O Runtime導向的流量，](#adobe-i-o-runtime-driven-communication-flow)您都必須定義遠端內容轉譯器設定。

>[!NOTE]
>
>此配置利用[遠程內容呈現器](#remote-content-renderer)，該呈現器具有其他可用的擴展和自定義選項。

## AEM驅動通信流{#aem-driven-communication-flow}

使用SSR時，AEM中SPA的[元件互動工作流程](introduction.md#interaction-with-the-spa-editor)包含Adobe I/O Runtime上產生應用程式初始內容的階段。

1. 瀏覽器會向AEM要求SSR內容。
1. AEM會將模型發佈至Adobe I/O Runtime。
1. Adobe I/O Runtime會傳回產生的內容。
1. AEM會透過後端頁面元件的HTL範本，提供Adobe I/O Runtime傳回的HTML。

![SSE CMS驅動的AEMAdobe I/O](assets/ssr-cms-drivenaemnode-adobeio.png)

## Adobe I/O Runtime驅動通信流{#adobe-i-o-runtime-driven-communication-flow}

上一節將說明針對AEM中的SPA而執行伺服器端轉譯的標準和建議實作，AEM會執行內容的引導及服務。

或者，SSR可以實現，使Adobe I/O Runtime負責引導，有效地逆轉通信流。

這兩種模型均有效，且受AEM支援。 然而，在實施特定模式之前，應考慮每種模式的利弊。

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
     <li>AEM會視需要管理注入程式庫</li>
     <li>只需在AEM<br />上維護資源 </li>
    </ul> </td>
   <td>
    <ul>
     <li>可能不熟悉SPA開發人員<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>透過Adobe I/O Runtime<br /> </strong></th>
   <td>
    <ul>
     <li>更熟悉SPA開發人員<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>應用程式所需的Clientlib資源（例如CSS和JavaScript）將需要由AEM開發人員透過<code><a href="/help/implementing/developing/introduction/clientlibs.md">allowProxy</a></code>屬性<br />提供 </li>
     <li>必須在AEM和Adobe I/O Runtime之間同步資源<br /> </li>
     <li>若要啟用SPA的編寫功能，可能需要Adobe I/O Runtime的代理伺服器</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## SSR {#planning-for-ssr}規劃

通常，只有應用程式的一部分需要呈現在伺服器端。 常見的範例是，在頁面初始載入時，會在折頁上方顯示的內容會呈現在伺服器端。 這樣可將已呈現的內容傳送給用戶端，節省時間。 當使用者與SPA互動時，用戶端會轉譯其他內容。

當您考慮為SPA實作伺服器端轉譯時，需要檢閱應用程式的哪些部分是必要的。

## 使用SSR {#developing-an-spa-using-ssr}開發SPA

SPA元件可由用戶端（在瀏覽器中）或伺服器端轉譯。 呈現伺服器端時，瀏覽器屬性（例如視窗大小和位置）不存在。 因此，SPA元件應為同構，不須假設其轉譯位置。

若要運用SSR，您必須在AEM和Adobe I/O Runtime中部署程式碼，後者負責伺服器端轉譯。 大部分的程式碼會相同，但伺服器特定的工作會有所不同。

## AEM中SPA的SSR {#ssr-for-spas-in-aem}

AEM中的SPA適用的SSR需要Adobe I/O Runtime，這是轉譯應用程式內容伺服器端所呼叫的功能。 在應用程式的HTL內，會呼叫Adobe I/O Runtime上的資源來呈現內容。

正如AEM可立即支援Angular和React SPA架構，Angular和React應用程式也支援伺服器端轉譯。 如需詳細資訊，請參閱這兩個架構的NPM檔案。

## 遠程內容呈現器{#remote-content-renderer}

在AEM中搭配SPA使用SSR所需的[遠端內容轉譯器設定](#remote-content-renderer-configuration)會點選更廣義的轉譯服務，以符合您的需求並加以擴充和自訂。

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` 是OSGi服務，用於擷取在遠端伺服器上轉譯的內容，例如從Adobe I/O。傳送至遠端伺服器的內容是根據所傳遞的要求參數。

`RemoteContentRenderingService` 可在需要進行其他內容操作時，透過相依性反轉插入自訂Sling模型或servlet中。

此服務由[RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet)在內部使用。

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

`RemoteContentRendererRequestHandlerServlet`可用來以程式設計方式設定請求配置。 `DefaultRemoteContentRendererRequestHandlerImpl`，提供預設請求處理常式實作，可讓您建立多個OSGi設定，以將內容結構中的位置對應至遠端端點。

若要新增自訂請求處理常式，請實作`RemoteContentRendererRequestHandler`介面。 請務必將`Constants.SERVICE_RANKING`元件屬性設定為大於100的整數，即`DefaultRemoteContentRendererRequestHandlerImpl`的排名。

```javascript
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### 配置預設處理程式{#configure-default-handler}的OSGi配置

預設處理程式的配置必須如[遠程內容呈現器配置](#remote-content-renderer-configuration)一節中所述配置。

### 遠端內容轉譯器用途 {#usage}

若要讓servlet擷取並傳回可插入頁面的某些內容：

1. 確保您的遠程伺服器可訪問。
1. 將下列其中一個程式片段新增至AEM元件的HTL範本。
1. （可選）建立或修改OSGi設定。
1. 瀏覽您網站的內容

頁面元件的HTL範本通常是此類功能的主要收件者。

```html
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### 需求 {#requirements}

servlet會利用Sling模型匯出工具來序列化元件資料。 預設情況下，`com.adobe.cq.export.json.ContainerExporter`和`com.adobe.cq.export.json.ComponentExporter`都支援作為Sling模型適配器。 如有必要，您可以新增應調整請求以使用`RemoteContentRendererServlet`和實作`RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`的類。 其他類必須擴展`ComponentExporter`。
