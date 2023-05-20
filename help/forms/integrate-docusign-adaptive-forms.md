---
title: 將DocuSign與自適應表單整合
description: 瞭解如何將DocuSign與自適應表單一起使用以收集電子簽名。
exl-id: fb2e75d6-e454-4999-a079-f663af79051f
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1557'
ht-degree: 8%

---

# 將DocuSign與自適應表單一起使用 {#integrate-aem-forms-with-DocuSign}

DocuSign是一個著名的電子簽名解決方案。 你可以用它來電子簽署協定。 可以將DocuSign與自適應表單整合。 它幫助您向多個收件人發送電子簽名的自適應表單。 使用電子簽名可幫助您：

- 通過完全自動化的計畫書、報價和合同流程從任何設備處成交。
- 更快地完成人力資源流程並為您的員工提供數字型驗。
- 縮短合同週期，加快供應商的上架速度。

AEM Formsas a Cloud Service提供 [DocuSign的自定義提交操作](#deploy-custom-submit-action)。 提交操作可幫助您使用DocuSign API發送電子簽名的自適應表單。

| 您還可以使用Adobe的電子簽名解決方案Adobe Sign來電子簽名自適應表單。 AEM Forms公司與Adobe Sign公司有更深入的整合，提供更精細的控制，如順序和並行簽名、多種驗證方法、格式簽名體驗等。 有關詳細資訊，請參見 [在自適應形式中使用Adobe Sign](working-with-adobe-sign.md)。 |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## 必備條件 {#prerequisites}

將DocuSign與AEM Forms整合需要以下內容：

- DocuSign [開發者帳戶](https://developers.docusign.com/platform/account/)
- DocuSign應用程式
- DocuSign API應用程式的憑據（客戶端ID和客戶端密碼）。
- [DocuSign的自定義提交操作和雲服務](https://github.com/adobe/aem-forms-docusign-sample)
- （僅適用於當地開發環境） [設定記錄文檔](setup-local-development-environment.md#docker-microservices)。

## 為DocuSign配置自定義提交操作和雲服務 {#deploy-custom-submit-action}

AEM Formsas a Cloud Service為DocuSign提供自定義提交操作。 提交操作可幫助您使用DocuSign API發送電子簽名的自適應表單。 自定義提交操作的代碼可在 [AEM Forms示例公共git儲存庫](https://github.com/adobe/aem-forms-docusign-sample)。 您可以在AEM Forms環境中部署代碼，也可以根據組織的要求自定義代碼。

執行以下步驟以配置現成的自定義提交操作和DocuSignCloud Service:

1. [克隆你的AEM Formsas a Cloud Service項目](setup-local-development-environment.md#forms-cloud-service-local-development-environment) 或建立 [!DNL Experience Manager Forms] 作為 [!DNL Cloud Service] 基於 [原AEM型27](https://github.com/adobe/aem-project-archetype) 或稍後。 建立 [!DNL Experience Manager Forms] 作為 [!DNL Cloud Service] 基於原型AEM的項目：
   </br> 開啟命令提示符並運行以下命令以建立 [!DNL Experience Manager Forms] as a Cloud Service項目：

   ```shell
   mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=27 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
   ```

   另外，更改 `appTitle`。 `appId`, `groupId`，以反映您的環境。

1. 克隆 [aem-forms-samples](https://github.com/adobe/aem-forms-docusign-sample) 儲存庫。 此儲存庫包含與DocuSign伺服器連接的DocuSign和配置詳細資訊的自定義提交操作。

1. 開啟在步驟1中建立的用於在您選擇的IDE中編輯的AEM Formsas a Cloud Service項目。

1. 開啟 `[AEM Forms as a Cloud Service project]\pom.xml` 檔案進行編輯並進行以下更改：

   1. 在 `<properties>` 標籤：

      ```shell
      <repository.location>maven_repository</repository.location>
      ```

   1. 在 `<repositories>` 標籤：

      ```shell
       <repository>
          <id>project-repository</id>
          <url>file://${project.basedir}/${repository.location}</url>
       </repository>
      ```

      如果沒有 `<repositories>` 標籤，在 `<properties>` 標籤。

   1. 在 `<dependencyManagement>` 標籤：

      ```shell
       <dependency>
         <groupId>com.adobe.aemforms.samples</groupId>
         <artifactId>forms.integration.docusign.all</artifactId>
         <type>zip</type>
         <version>1.0.0</version>
       </dependency>
      ```

1. 在 `all/pom.xml` 檔案在Cloud Service項目資料夾中可用：

   1. 在 `<embeddeds>` 標籤：

      ```shell
       <embedded>
          <groupId>com.adobe.aemforms.samples</groupId>
          <artifactId>forms.integration.docusign.all</artifactId>
          <type>zip</type>
          <target>/apps/moonlightprodprogram-vendor-packages/application/install</target>
       </embedded>
      ```

   1. 在 `<dependencies>` 標籤：

      ```shell
       <dependency>
          <groupId>com.adobe.aemforms.samples</groupId>
          <artifactId>forms.integration.docusign.all</artifactId>
          <type>zip</type>
       </dependency>
      ```

1. 開啟命令提示符並導航到 `aem-forms-samples\forms-integration-docusign` （在步驟3中克隆）並運行以下命令：

   ```shell
   mvn clean install -Dinstall.dir="<AEM Forms as a Cloud Service project path>/maven_repository"
   ```

   `<AEM Forms as a Cloud Service project path>` 引用在此過程的步驟1中建立的資料夾的名稱。

1. 將項目部署到您的本地開發環境。 可以使用以下命令部署到本地開發環境

   `mvn -PautoInstallPackage clean install`

   執行這些步驟後，您可以查看新的自定義提交操作 [使用DocuSign電子簽名提交](#enabledocusign) 可在自適應表單和 [DocuSign雲服務配置](#configure-docusign-with-aem-forms) 在當地的開發環境中。

1. 編譯和 [將代碼部署到 [!DNL AEM Forms] as a Cloud Service環境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#customer-releases)。

## 整合 [!DNL DocuSign] 與 [!DNL AEM Forms] {#configure-docusign-with-aem-forms}

先決條件就位後，請執行以下步驟來整合 [!DNL DocuSign] 與 [!DNL AEM Forms] 在作者實例上。

1. 導航到 **[!UICONTROL 工具]** ![錘](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL 多庫簽名]** 並選擇一個資料夾來承載配置。

1. 在「配置」頁上，點擊 **[!UICONTROL 建立]** 建立 [!DNL DocuSign] 配置在AEM Forms。
1. 在 **[!UICONTROL 常規]** 頁籤 **[!UICONTROL 建立DocuSign配置]** 頁，指定 **[!UICONTROL 名稱]** ，然後點擊 **[!UICONTROL 下一個]**。 您可以選擇指定 **[!UICONTROL 標題]**。

1. 將您目前瀏覽器視窗中的 URL 複製到筆記本。在後續步驟中，需要使用此 URL 設定 [!DNL DocuSign] 應用程式和 [!DNL AEM Forms]。

1. 設定 [!DNL DocuSign] 應用程式的 OAuth 設定：

   1. 開啟瀏覽器窗口並登錄到 [!DNL DocuSign] [開發者帳戶](https://admindemo.docusign.com/apps-and-keys)。
   1. 開啟為 [!DNL AEM Forms]。
   1. 在 **[!UICONTROL 重定向URI]** 框中，添加上一步中複製的URL，然後按一下 **[!UICONTROL 保存]**。
   1. 記下「Integration and Secret Keys（整合密鑰和密鑰）」。

   如需設定 [!DNL DocuSign] 應用程式的 OAuth 設定並取得金鑰的逐步資訊，請參閱「[設定應用程式的 OAuth 設定](https://support.docusign.com/guides/ndse-admin-guide-api-and-keys)」開發人員文件。

1. 返回 **[!UICONTROL 建立DocuSign配置]** 的子菜單。 在 **[!UICONTROL 設定]** 頁籤 **[!UICONTROL OAuth URL]** 欄位提及以下預設URL:

   `https://account-d.docusign.com/oauth/auth`

1. 指定 **[!UICONTROL 客戶端ID]** （DocuSign整合密鑰）和 **[!UICONTROL 客戶端密碼]** （DocuSign密鑰）。

1. 點擊 **[!UICONTROL 連接到DocuSign]**。 出現認證提示時，請提供在建立 [!DNL DocuSign] 應用程式時使用的帳戶使用者名稱和密碼。當要求確認訪問 `your developer account`按一下 **[!UICONTROL 允許訪問]**。 如果憑據正確，則會顯示成功消息。

1. 點擊 **[!UICONTROL 建立]** 建立 [!DNL DocuSign] 配置。

1. 選擇配置並按一下 **[!UICONTROL 發佈]**，選擇配置，然後按一下 **[!UICONTROL 發佈]**。 這會將設定複寫至對應的發佈環境。

1. 請對您的開發人員、中繼及生產執行個體 (無論是哪個) 重複上述步驟，以完成您環境的設定 [!DNL DocuSign] with [!DNL AEM Forms]。

現在，您的AEM Forms環境已配置為使用DocuSign。 請確保您將用於 Cloud Service 的設定容器新增至 [!DNL DocuSign] 啟用的所有最適化表單。您可從最適化表單的屬性指定設定容器。

### 使用 [!DNL DocuSign] 在自適應窗體中 {#enabledocusign}

您可以啟用 [!DNL DocuSign] 或建立 [!DNL DocuSign] 啟用的自適應窗體。 選擇以下選項之一：

- [建立 [!DNL DocuSign] 啟用的自適應窗體](#create-an-adaptive-form-for-docusign)
- [啟用 [!DNL DocuSign] 用於現有自適應窗體](#editafsign)。

#### 為DocuSign建立自適應窗體 {#create-an-adaptive-form-for-docusign}

要建立啟用符號的自適應表單：

1. 導航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文檔]**。
1. 點擊 **[!UICONTROL 建立]** 選擇 **[!UICONTROL 自適應窗體]**。 此時將顯示模板清單。 選擇模板並點擊 **[!UICONTROL 下一個]**。
1. 在 **[!UICONTROL 基本]** 頁籤：

   1. 指定 **[!UICONTROL 名稱]** 和 **[!UICONTROL 標題]** 的子菜單。

   1. 選擇 [配置容器](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) 建立時 [整合 [!DNL DocuSign] 與 [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md)。
   配置容器包含 [!DNL DocuSign] Cloud Services已為您的環境配置。 這些服務可在Adaptive Form編輯器中進行選擇。

1. 在 **[!UICONTROL 窗體模型]** 頁籤中，選擇以下選項之一：

   - 如果您有自定義表單模板並需要基於表單模板的記錄文檔，請選擇 **[!UICONTROL 將表單模板與記錄文檔模板關聯]** 的子菜單。 使用此選項時，發送用於簽名的文檔只顯示基於關聯表單模板的欄位。 它不顯示自適應表單的所有欄位。

   - 如果沒有自定義表單模板，請選擇 **[!UICONTROL 生成記錄文檔]** 的雙曲餘切值。 使用此選項時，發送用於簽名的文檔將顯示自適應表單的所有欄位。

1. 點擊 **[!UICONTROL 建立。]** 建立啟用符號的自適應表單。 您可以添加 [!DNL DocuSign] 欄位，然後將其發送以進行簽名。
1. 在編輯模式下開啟自適應窗體。 在 **[!UICONTROL 內容]** 頁籤 **[!UICONTROL 窗體容器]** 點擊 ![配置](assets/configure-icon.svg)。

1. 在 **[!UICONTROL 提交]** 選擇 **[!UICONTROL 使用DocuSign電子簽名提交]** 從 **[!UICONTROL 提交操作]** 下拉清單。

1. 在 **[!UICONTROL 操作配置]** 部分，點擊 **[!UICONTROL 添加]** 添加收件人並指定收件人的電子郵件地址。 點擊 **[!UICONTROL 添加]** 來添加更多收件人。

1. 在中為電子郵件指定主題 **[!UICONTROL 電子郵件主題]** 的子菜單。 選擇 **包括附件** 以在電子郵件中包含附件。

1. 點擊 ![保存](assets/save_icon.svg) 的子菜單。

#### 啟用 [!DNL DocuSign] 自適應窗體 {#editafsign}

要使用 [!DNL DocuSign] 在現有的自適應窗體中：

1. 導航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文檔]**。
1. 選擇「自適應表單」並點擊 **[!UICONTROL 屬性]**。
1. 在 **[!UICONTROL 基本]** 頁籤 [配置容器](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) 建立時間 [!DNL DocuSign] 與 [!DNL AEM Forms]。
1. 在 **[!UICONTROL 窗體模型]** 頁籤中，選擇以下選項之一：

   - 如果您有自定義表單模板並需要基於表單模板的記錄文檔，請選擇 **[!UICONTROL 將表單模板與記錄文檔模板關聯]** 的子菜單。 使用此選項時，發送用於簽名的文檔只顯示基於關聯表單模板的欄位。 它不顯示自適應表單的所有欄位。

   - 如果沒有自定義表單模板，請選擇 **[!UICONTROL 生成記錄文檔]** 的雙曲餘切值。 使用此選項時，發送用於簽名的文檔將顯示自適應表單的所有欄位。

1. 點擊 **[!UICONTROL 保存並關閉]**。 已為 [!DNL DocuSign]。 現在，您可以 [!DNL DocuSign] 欄位，然後將其發送以進行簽名。

1. 在編輯模式下開啟自適應窗體。 在 **[!UICONTROL 內容]** 頁籤 **[!UICONTROL 窗體容器]** 點擊 ![配置](assets/configure-icon.svg)。

1. 在 **[!UICONTROL 提交]** 選擇 **[!UICONTROL 使用DocuSign電子簽名提交]** 從 **[!UICONTROL 提交操作]** 下拉清單。

1. 在 **[!UICONTROL 操作配置]** 部分，點擊 **[!UICONTROL 添加]** 添加收件人並指定收件人的電子郵件地址。 點擊 **[!UICONTROL 添加]** 來添加更多收件人。

1. 在中為電子郵件指定主題 **[!UICONTROL 電子郵件主題]** 的子菜單。 選擇 **包括附件** 以在電子郵件中包含附件。

1. 點擊 ![保存](assets/save_icon.svg) 的子菜單。
