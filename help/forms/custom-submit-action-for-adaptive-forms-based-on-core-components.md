---
title: 如何根據核心元件建立最適化表單的自訂提交動作？
description: 瞭解如何為最適化Forms建立自訂提交動作，以便在使用自訂提交動作提交資料之前處理資料。
feature: Adaptive Forms, Core Components
role: User, Developer
level: Intermediate
exl-id: a369b585-d148-4b5a-8afe-d5673ea865d0
source-git-commit: 03e46bb43e684a6b7057045cf298f40f9f1fe622
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 4%

---

# 建立最適化Forms （核心元件）的自訂提交動作

提交動作可讓使用者為從表單擷取的資料選擇目的地，並定義要在表單提交上執行的其他功能。 AEM表單支援多個[立即可用的提交動作(OOTB)](/help/forms/configure-submit-actions-core-components.md)，例如傳送電子郵件或儲存資料至SharePoint或OneDrive。

您也可以建立自訂提交動作，以新增[現成可用的選項](/help/forms/configure-submit-actions-core-components.md#select-and-configure-a-submit-action-for-an-adaptive-form-select-and-configure-submit-action)中未包含的功能。 例如，將表單資料與第三方應用程式整合，或根據使用者輸入觸發個人化SMS通知。

<!-- ![Custom Submit Image](/help/forms/assets/custom-submit-action-hero-image.png)
-->

## 必要條件

開始建立Adaptive Forms的第一個自訂提交動作之前，請確定您具備下列條件：

* **純文字編輯器(IDE)**：雖然任何純文字編輯器都可以運作，但Microsoft Visual Studio Code之類的整合式開發環境(IDE)可提供進階功能，讓編輯更輕鬆。

* **Git**：管理程式碼變更需要此版本控制系統。 如果您尚未安裝，請從https://git-scm.com下載。

## 建立您的第一個自訂表單提交動作

下圖說明為最適化表單建立自訂提交動作的步驟：

![自訂提交動作工作流程](/help/forms/assets/custom-submit-action-workflow.png){width=50%， height-50%}

### 複製AEM as a Cloud Service Git存放庫。

1. 開啟命令列，並選擇要儲存AEM as a Cloud Service存放庫的目錄，例如`/cloud-service-repository/`。

1. 執行以下命令以複製存放庫：

   ```
   git clone https://git.cloudmanager.adobe.com/<organization-name>/<app-id>/
   ```

   **在哪裡可以找到此資訊？**

   如需尋找這些詳細資訊的逐步指示，請參閱Adobe Experience League文章&quot;[存取Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git)&quot;。

   **您的專案已就緒！**

   當命令成功完成時，您會看到在本機目錄中建立的新資料夾。 此資料夾是以您的應用程式（例如app-id）命名。 此資料夾包含從AEM as a Cloud Service Git存放庫下載的所有檔案和程式碼。 您可以在`<appid>`檔案中找到您AEM專案的`archetype.properties`。

   ![Archetype屬性](/help/forms/assets/custom-submit-action-archetype-app-id.png)

   在本指南中，我們將此資料夾稱為`[AEMaaCS project directory]`。

## 新增提交動作

1. 在編輯器中開啟存放庫資料夾。

   ![克隆的存放庫](/help/forms/assets/custom-submit-action-clone-repo.png)

1. 導覽至`[AEMaaCS project directory]`中的下列目錄：

   ```
   /ui.apps/src/main/content/jcr_root/apps/<app-id>/
   ```

   **重要**：將`<app-id>`取代為您的實際應用程式識別碼。

1. 為您自訂提交動作建立新資料夾，並為它指定您選擇的名稱。 例如，將資料夾命名為`customsubmitaction`。

   ![建立自訂提交動作資料夾](/help/forms/assets/custom-submit-action-create-folder.png)

1. 導覽至新增的自訂提交動作目錄。

   在您的`[AEMaaCS project directory]`內，瀏覽至下列路徑：

   `/ui.apps/src/main/content/jcr_root/apps/<app-id>/customsubmitaction/`

   `Important`：將`<app-id>`取代為您的實際應用程式ID。

1. 建立新的組態檔。
在`customsubmitaction`資料夾中，建立名為`.content.xml`的新檔案。

   ![建立設定檔](/help/forms/assets/custom-submit-action-create-config-folder.png)

1. 開啟此檔案並貼上下列內容，將`[customsubmitaction]`取代為您提交動作的名稱

   ```
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
   jcr:description="[customsubmitaction]"
   jcr:primaryType="sling:Folder"
   
   guideComponentType="fd/af/components/guidesubmittype"
   guideDataModel="basic,xfa,xsd"
   submitService="[customsubmitaction]"/>
   ```

   例如，將`[customsubmitaction]`取代為您自訂的提交動作名稱`Custom Submit Action`。

   ![建立自訂提交動作組態檔](/help/forms/assets/custom-submit-action-config-file.png)

   >[!NOTE]
   >
   > 記住[customsubmitaction]的名稱，因為在撰寫表單時，`Submit action`下拉式清單中會顯示相同的名稱。


**在`filter.xml`**&#x200B;中包含新資料夾

1. 導覽至`/ui.apps/src/main/content/META-INF/vault/filter.xml`AEMaaCS專案目錄[中的]檔案。

1. 開啟檔案，並在結尾新增下列行：

   ```
   <filter root="/apps/<app-id>/[customsubmitaction-folder]"/>
   ```

   例如，新增下列程式碼行以在`customsubmitaction`檔案中新增`filter.xml`資料夾：

   ```
   <filter root="/apps/wknd/customsubmitaction"/>
   ```

   ![在filter.xml中新增建立的資料夾](/help/forms/assets/custom-submit-action-filter-xml.png)

1. 儲存變更。

### 針對新增的提交動作實作服務。

1. 導覽至`[AEMaaCS project directory]`中的下列目錄：
   `/core/src/main/java/com/<app-id>/core/service/`
   `Important`：將`<app-id>`取代為您的實際應用程式ID。
1. 建立新的Java檔案來實作新增提交動作的服務。 例如，將新的Java檔案新增為`CustomSubmitService.java`。

   ![自訂提交動作資料夾](/help/forms/assets/custom-submit-action-custom-submit-folder.png)

1. 開啟此檔案，並新增自訂提交動作實施的程式碼。

   例如，下列Java程式碼是OSGi服務，會記錄提交的資料來處理表單提交，並傳回狀態`OK`。 在`CustomSubmitService.java`檔案中新增下列程式碼：

   ```
   package com.wknd.core.service;
   
   import com.adobe.aemds.guide.model.FormSubmitInfo;
   import com.adobe.aemds.guide.service.FormSubmitActionService;
   import java.util.HashMap;
   import java.util.Map;
   import org.osgi.service.component.annotations.Component;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   
       @Component(
       service = FormSubmitActionService.class,
       immediate = true
           )
       public class CustomSubmitService implements FormSubmitActionService {
   
       private static final String serviceName = "Custom Submit Action";
   
       private static Logger log = LoggerFactory.getLogger(CustomSubmitService.class);
   
       @Override
       public String getServiceName() {
       return serviceName;
       }
   
       @Override
       public Map<String, Object> submit(FormSubmitInfo formSubmitInfo) {
       String data = formSubmitInfo.getData();
       log.info("Using custom submit action service, [data] --> " + data);
       Map<String, Object> result = new HashMap<>();
       result.put("status", "OK");
       return result;
        }
       }
   ```

   ![自訂提交動作服務](/help/forms/assets/custom-submit-action-service.png)

1. 儲存變更。

### 部署程式碼。

**部署本機開發環境的程式碼**

* 將AEM as a Cloud Service `[AEMaaCS project directory]`部署至您的本機開發環境，以在本機電腦上嘗試新的提交動作。 若要部署到您的本機開發環境：

   1. 確認您的本機開發環境已啟動且執行中。 如果您尚未設定本機開發環境，請參閱[為AEM Forms設定本機開發環境](/help/forms/setup-local-development-environment.md)的指南。

   1. 開啟終端機視窗或命令提示。

   1. 導覽至`[AEMaaCS project directory]`。

   1. 執行以下命令：

      ```
      mvn -PautoInstallPackage clean install
      ```

      ![本機部署](/help/forms/assets/custom-submit-action-local-deployment.png)

**部署Cloud Service環境的程式碼**

* 將AEM as a Cloud Service `[AEMaaCS project directory]`部署至您的Cloud Service環境。 若要部署至您的Cloud Service環境：

   1. 提交您的變更：

      新增自訂提交動作設定後，使用清除Git訊息提交您的變更。 （例如，「已新增新的自訂提交動作」）。

   1. 部署更新的程式碼：

      透過[現有的完整棧疊管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=zh-Hant#setup-pipeline)觸發程式碼的部署。 它會透過新的自訂提交動作支援，自動建置及部署更新的程式碼。

      如果您尚未設定管道，請參閱[上的指南以瞭解如何設定AEM Forms as a Cloud Service的管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=zh-Hant#setup-pipeline)。

      ![雲端部署](/help/forms/assets/custom-submit-action-cloud-deployment.png)

      **如何確認安裝？**

      成功建立專案後，自訂提交動作就會在製作表單時顯示在`Submit action`下拉式清單中。

      ![自訂提交動作下拉式清單](/help/forms/assets/custom-submit-action-drop-down-list.png)

  您的環境現在已準備好在製作表單時使用新增的自訂提交動作。

### 使用新增的提交動作預覽最適化表單

1. 登入您的AEM Forms as a Cloud Service執行個體。
1. 移至&#x200B;**Forms** > **Forms和檔案**。

   ![Forms和檔案](/help/forms/assets/custom-submit-action-fnd.png)

1. 選取最適化表單並按一下&#x200B;**編輯**。 表單會在編輯模式中開啟。

   ![編輯表單](/help/forms/assets/custom-submit-action-edit-af.png)

1. 開啟內容瀏覽器，然後選取最適化表單的「**[!UICONTROL 指引容器]**」元件。
1. 按一下「指引容器」屬性 ![指引屬性](/help/forms/assets/configure-icon.svg) 圖示。此時會開啟「最適化表單容器」對話框。
1. 按一下「**[!UICONTROL 提交]**」標籤。
1. 從&#x200B;**[!UICONTROL 提交動作]**&#x200B;下拉式清單中，選取提交動作。 例如，將提交動作選取為`Custom Submit Action`。

   ![自訂提交表單](/help/forms/assets/custom-submit-action-select-submit-action.png)

1. 填寫表單並提交它。

   ![提交表單](/help/forms/assets/custom-submit-action-submit-form.png)

   ![感謝訊息](/help/forms/assets/custom-submit-action-thankyou-msg.png)

   成功提交表單後，您可以檢查&#x200B;**Adobe Experience Manager Web主控台組態**，以驗證本機開發環境中自訂提交動作的動作。
1. 前往 `http://<host>:<port>/system/console/configMgr`。

1. 瀏覽至&#x200B;**的** Adobe Experience Manager Web Console記錄檔支援`http://<host>:<port>/system/console/slinglog`。

   ![ConfigMgr](/help/forms/assets/custom-submit-action-sling-log.png)

1. 按一下`logs/error.log`選項。
   ![開啟error.log檔案](/help/forms/assets/custom-submit-action-error-log.png)

1. 開啟`error.log`檔案以檢視是否已附加資料。

   ![error.log檔案](/help/forms/assets/custom-submit-action-form-data-display.png)

   >[!NOTE]
   >
   > * 若要在AEM as a Cloud Service環境中檢視錯誤記錄檔，您可以使用Splunk。
   > * 如果自訂提交動作服務遇到未處理的錯誤，AEM as a Cloud Service會傳回502錯誤頁面HTML。


## 常見問題

**問：為什麼我的最適化表單在提交後會顯示5.x.x錯誤頁面？**
自訂提交動作服務因未處理的錯誤而失敗。 接著AEM Cloud Service會傳回其預設錯誤頁面。

<!--
## Best practices

 * It is recommended to use the OSGi service approach for creating a custom submit action, as it is faster than the AEM servlet approach. 

## Next steps
-->

## 相關文章

{{af-submit-action}}

<!-- The [Adaptive Forms Core Components](https://github.com/adobe/aem-core-forms-components) repository includes a sample folder, `customsubmission/logsubmit`, to simplify the process of adding new custom submit actions. It also provides the Java service implementation for the `logsubmit` custom submit action, named `CustomAFSubmitService`.java. These resources are available on GitHub. -->
