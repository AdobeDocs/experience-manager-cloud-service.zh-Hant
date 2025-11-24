---
title: AEM Forms通訊API — 概觀
description: AEM Forms通訊API概觀，包括驗證方法和完整的API參考
role: Developer, User
feature: Adaptive Forms, APIs & Integrations
hide: true
hidefromtoc: true
index: false
source-git-commit: 580d6505ffdf25f7bfb3a3a84f054dcf76c05cdd
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 4%

---


# AEM Forms通訊API — 概觀

AEM Forms Communications API提供完整的雲端原生API套件，旨在協助企業自動化檔案工作流程。

AEM Forms API的結構化可透過兩個主要主控台進行存取：

* [Adobe Developer Console (ADC)](https://developer.adobe.com/developer-console/) - Adobe Developer Console是Adobe API、事件、執行階段和App Builder的閘道。

* [AEM Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console) - AEM Developer Console提供用於偵錯和檢查AEM as a Cloud Service環境的工具。

每個主控台都可讓您存取不同的API和服務，以執行檔案處理、產生、轉換、加密和通訊工作。 API支援不同的[驗證方法](#authentication-methods)。

## 驗證方法

API支援多種驗證方法，以確保您的應用程式與Adobe服務之間的安全整合：

| 層面 | OAuth伺服器對伺服器（建議使用） | JWT （JSON Web權杖） |
|-------------|------------------------------------------|---------------------------|
| 說明 | 現代且安全的API存取方法，使用者不必另行互動。 | 使用已簽署權杖存取的舊方法。 |
| 設定位置 | Adobe Developer Console與AEM Developer Console | 僅限AEM Developer Console |
| 安全性 | 高 — 使用使用者端憑證和範圍 | 中等 — 取決於金鑰管理 |
| 擴充性 | 可高度擴充的後端整合 | 有限，適合舊版使用 |
| Token Management | 自動產生和續約 | 手動權杖簽署和輪換 |
| 狀態 | 推薦 | 已棄用 |


>[!NOTE]
>
> 按一下下列連結以進一步瞭解:-
> 
> * [OAuth伺服器對伺服器（建議使用）](/help/forms/oauth-api-authetication.md)
> * [JWT （JSON Web權杖）](/help/forms/jwt-api-authentication.md)

<!--### Execution Models

The following table highlights the key differences between Synchronous (On-Demand) and Asynchronous (Batch) execution models supported in AEM Forms Communications APIs:

| Feature | Synchronous (On-Demand) | Batch (Asynchronous) |
|---------|-------------------------|----------------------|
| **Execution Model** | Real-time, immediate | Queued, scheduled |
| **Response Time** | Seconds | Minutes to hours |
| **Volume** | Single or few documents | Hundreds to thousands |
| **Testing Environment** | Author & Publish | Author Only |
| **Use Case** | User-triggered actions | Scheduled bulk operations |
| **Console Access** | ADC & AEM Developer Console | AEM Developer Console Only |-->

## API分類概觀

所有AEM Forms API主要分為兩個部分：

* [最適化表單傳遞和執行階段API](https://developer-stage.adobe.com/experience-cloud/experience-manager-apis/api/stable/forms/)

* [AEM Forms通訊API](#aem-forms-communications-apis)

| 詳細資訊 | 最適化表單傳送和執行階段API | 通訊API |
|--------------|----------------------------|--------------------------|
| 用途 | 處理最適化表單傳遞和執行階段作業 | 檔案產生與操作 |
| 使用案例 |  — 表單轉譯<br> — 資料預填<br> — 表單提交<br> — 草稿管理 | - PDF產生<br> — 檔案合併<br> — 批次處理<br> — 列印作業 |
| 授權方法 | 支援OAuth伺服器對伺服器/使用者驗證方法。 | 僅支援OAuth伺服器對伺服器驗證。 |

### AEM Forms通訊API

通訊API是以檔案為中心的作業的主要焦點。

下表列出所有[AEM Forms Communications API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/)及其支援的驗證方法與執行模型：

#### Document Generation API


| API端點 | 說明 | 執行模型 | 驗證方法 |
| ----- | ------ |------- | ------ |
| [/adobe/forms/batch/output/config](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/CreateBatchConfig) | 為檔案產生作業建立新的批次組態。 | 非同步/批次 | [OAuth伺服器至伺服器](/help/forms/oauth-api-authetication.md)/[JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/{configName}](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/GetBatchConfigbyName) | 擷取特定批次設定的詳細資料。 | 非同步/批次 | [OAuth伺服器至伺服器](/help/forms/oauth-api-authetication.md)/[JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/configs](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/GetAllBatchConfigs) | 傳回所有可用批次設定的清單。 | 非同步/批次 | [OAuth伺服器至伺服器](/help/forms/oauth-api-authetication.md)/[JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/{configName}/execution](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/StartBatchRun) | 使用設定開始批次輸出產生執行。 | 非同步/批次 | [OAuth伺服器至伺服器](/help/forms/oauth-api-authetication.md)/[JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/{configName}/execution/{executionId}](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/GetBatchRunInstanceState) | 擷取批次工作的執行狀態。 | 非同步/批次 | [OAuth伺服器至伺服器](/help/forms/oauth-api-authetication.md)/[JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/{configName}/executions](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/GetAllRunningInstancesForBatch) | 列出特定批次組態的所有執行中執行個體。 | 非同步/批次 | [OAuth伺服器至伺服器](/help/forms/oauth-api-authetication.md)/[JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/doc/v1/generatePDFOutput](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generatePDFOutput/post) | 根據範本和資料同步產生PDF輸出。 | 同步 | [OAuth伺服器至伺服器](/help/forms/oauth-api-authetication.md)/[JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/doc/v1/generatePrintedOutput](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Batch-Execution/operation/GetAllRunningInstancesForBatch) | 產生可供列印的輸出格式(例如PCL、PostScript)。 | 同步 | [OAuth伺服器至伺服器](/help/forms/oauth-api-authetication.md)/[JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/doc/v1/generate/afp](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generate~1afp/post) | 為大量列印產生AFP輸出。 | 同步 | [OAuth伺服器至伺服器](/help/forms/oauth-api-authetication.md)/[JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/document/generate/pdfform](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFForm) | 轉譯含有合併資料的PDF表單(XFA/XDP)。 | 同步 | [OAuth伺服器至伺服器](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/generate/pdfform/jobs/{id}/status](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFFormJobStatus) | 擷取PDF表單產生工作的狀態。 | 同步 | [OAuth伺服器至伺服器](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/generate/pdfform/jobs/{id}/result](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFFormJobResult) | 擷取已完成的PDF表單作業的輸出/結果。 | 同步 | [OAuth伺服器至伺服器](/help/forms/oauth-api-authetication.md) |


#### Document Manipulation API

| API端點 | 說明 | 執行模型 | 驗證方法 |
| ------------------ | ---------------- | ----------| ---------- |
| [/adobe/forms/assembler/ddx/invoke](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/DDX-execution/operation/InvokeDDX) | 執行DDX指令以組合、分割或操控PDF。 | 同步 | [OAuth伺服器至伺服器](/help/forms/oauth-api-authetication.md)/[JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/assembler/pdfa/convert](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/Document-conversion/operation/ConvertToPDFA) | 將PDF檔案轉換為PDF/A格式。 | 同步 | [OAuth伺服器至伺服器](/help/forms/oauth-api-authetication.md)/[JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/assembler/pdfa/validate](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/Document-validation/operation/CheckIsPDFA) | 驗證PDF是否符合PDF/A標準 | 同步 | [OAuth伺服器至伺服器](/help/forms/oauth-api-authetication.md)/[JWT](/help/forms/jwt-api-authentication.md) |

#### 檔案轉換API

| API端點 | 說明 | 執行模型 | 驗證方法 |
|--------- | -------|---------|----------------------|
| [/adobe/document/convert/pdftoxdp](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Conversion/paths/~1convert~1pdftoxdp/post) | 將PDF表單轉換為XDP格式。 | 同步 | [OAuth伺服器至伺服器](/help/forms/oauth-api-authetication.md) |

#### 檔案擷取API

| API端點 | 說明 | 執行模型 | 驗證方法 |
|---------| -------|---------|----------------------|
| [/adobe/forms/doc/v1/extract/pdfproperties](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1pdfproperties/post) | 從PDF中擷取屬性和結構資訊。 | 同步 | [OAuth伺服器至伺服器](/help/forms/oauth-api-authetication.md) |
| [/adobe/forms/doc/v1/extract/usagerights](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/extractUsageRights) | 擷取內嵌於PDF中的使用許可權。 | 同步 | [OAuth伺服器至伺服器](/help/forms/oauth-api-authetication.md) |
| [/adobe/forms/doc/v1/extract/metadata](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1metadata/post) | 擷取中繼資料，例如標題、作者和關鍵字。 | 同步 | [OAuth伺服器至伺服器](/help/forms/oauth-api-authetication.md) |
| [/adobe/forms/doc/v1/extract/data](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/exportData) | 從PDF forms擷取表單資料(XML/JSON)。 | 同步 | [OAuth伺服器至伺服器](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/extract/security](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1security/post) | 擷取安全性設定，例如許可權和加密。 | 同步 | [OAuth伺服器至伺服器](/help/forms/oauth-api-authetication.md) |

#### Document Transformation API


| API端點 | 說明 | 執行模型 | 驗證方法 |
|--------|---------|---------|----------------------|
| [/adobe/document/transform/metadata](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1transform~1metadata/post) | 在PDF檔案中更新或新增中繼資料。 | 同步 | [OAuth伺服器至伺服器](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/field/signature/add](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1add/post) | 將數位簽名欄位新增至PDF。 | 同步 | [OAuth伺服器至伺服器](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/field/signature/clear](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1clear/post) | 清除簽名欄位的內容。 | 同步 | [OAuth伺服器至伺服器](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/field/signature/remove](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1remove/post) | 從PDF移除簽名欄位。 | 同步 | [OAuth伺服器至伺服器](/help/forms/oauth-api-authetication.md) |

#### 檔案Assurance API

| API端點 | 說明 | 執行模型 | 驗證方法 |
|---------|-------|---------|----------------------|
| [/adobe/document/assure/usagerights](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/applyUsageRights) | 將使用許可權套用至PDF （例如，註解、填寫、簽署）。 | 同步 | [OAuth伺服器至伺服器](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/assure/encrypt](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1encrypt/post) | 使用密碼或憑證安全性來加密PDF。 | 同步 | [OAuth伺服器至伺服器](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/assure/decrypt](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1decrypt/post) | 解密受保護的PDF檔案。 | 同步 | [OAuth伺服器至伺服器](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/assure/sign](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1sign/post) | 數位簽署PDF檔案。 | 同步 | [OAuth伺服器至伺服器](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/assure/certify](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1certify/post) | 使用數位憑證來認證PDF。 | 同步 | [OAuth伺服器至伺服器](/help/forms/oauth-api-authetication.md) |


## 後續步驟

瞭解如何設定同步（隨選）和非同步（批次） Forms Communications API的環境：

<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <!-- Synchronous APIs Card -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="AEM Forms Communications APIs - Synchronous">
        <div class="card" style="height: 100%; display: flex; flex-direction: column;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" title="同步API" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/sync-api.png" alt="同步API"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" target="_self" rel="referrer" title="AEM Forms Communications API — 同步">AEM Forms Communications API — 同步</a>
                    </p>
                    <p class="is-size-6">瞭解如何設定同步（隨選） Forms Communications API的環境，以便立即產生或處理檔案。 </p>
                </div>
                <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">了解更多</span>
                </a>
            </div>
        </div>
    </div>
    <!-- Asynchronous APIs Card -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="AEM Forms Communications APIs - Asynchronous">
        <div class="card" style="height: 100%; display: flex; flex-direction: column;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" title="AEM Forms Communications API — 非同步" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/async-api.png" alt="非同步API"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" target="_self" rel="referrer" title="非同步API">AEM Forms Communications API — 非同步（批次）</a>
                    </p>
                    <p class="is-size-6">瞭解如何為非同步（批次） Forms Communications API設定環境，以排程方式產生或處理多個檔案。</p>
                </div>
                <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">了解更多</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->


>[!MORELIKETHIS]
>
>* [AEM Forms as a Cloud Service通訊簡介](/help/forms/aem-forms-cloud-service-communications-introduction.md)
>* 最適化AEM Forms和通訊API的[Forms as a Cloud Service架構](/help/forms/aem-forms-cloud-service-architecture.md)
>* [通訊處理 — 同步API](/help/forms/aem-forms-cloud-service-communications.md)
>* [通訊處理 — 批次API](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
>* [通訊處理 — 隨選API](/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md)