---
title: 將DocuSign與最適化表單整合
description: 了解如何使用DocuSign搭配最適化表單來收集電子簽名。
exl-id: fb2e75d6-e454-4999-a079-f663af79051f
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1557'
ht-degree: 8%

---

# 搭配最適化表單使用DocuSign {#integrate-aem-forms-with-DocuSign}

DocuSign是一個著名的電子簽名解決方案。 您可以用它來電子簽署合約。 您可以整合DocuSign與最適化表單。 它可協助您將電子簽名的最適化表單傳送給多個收件者。 使用電子簽名可幫助您：

- 通過完全自動化的計畫書、報價和合同流程從任何設備處理交易。
- 更快完成人力資源流程，並為員工提供數位體驗。
- 縮短合約週期時間，並加快供應商的上線速度。

AEM Formsas a Cloud Service提供 [DocuSign的自訂提交動作](#deploy-custom-submit-action). 提交動作可協助您使用DocuSign API傳送最適化電子簽名表單。

| 您也可以使用Adobe的電子簽名解決方案Adobe Sign，對最適化表單進行電子簽名。 AEM Forms與Adobe Sign有更深入的整合，並提供更精細的控制項，例如循序和平行簽署、多種驗證方法、表單式簽署體驗等。 如需詳細資訊，請參閱 [在適用性表單中使用Adobe Sign](working-with-adobe-sign.md). |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## 必備條件 {#prerequisites}

若要整合DocuSign與AEM Forms，需要下列項目：

- DocuSign [開發人員帳戶](https://developers.docusign.com/platform/account/)
- DocuSign應用程式
- DocuSign API應用程式的憑證（用戶端ID和用戶端密碼）。
- [適用於DocuSign的自訂提交動作和雲端服務](https://github.com/adobe/aem-forms-docusign-sample)
- （僅適用於本機開發環境） [記錄設定文檔](setup-local-development-environment.md#docker-microservices).

## 為DocuSign設定自訂提交動作和雲端服務 {#deploy-custom-submit-action}

AEM Formsas a Cloud Service提供DocuSign的自訂提交動作。 提交動作可協助您使用DocuSign API傳送最適化電子簽名表單。 自訂提交動作的程式碼可在 [AEM Forms範例公開git存放庫](https://github.com/adobe/aem-forms-docusign-sample). 您可以在AEM Forms環境中按原樣部署程式碼，或根據組織需求加以自訂。

執行下列步驟以設定現成的自訂提交動作和DocuSignCloud Service:

1. [複製AEM Formsas a Cloud Service專案](setup-local-development-environment.md#forms-cloud-service-local-development-environment) 或建立 [!DNL Experience Manager Forms] as a [!DNL Cloud Service] 基於 [AEM原型27](https://github.com/adobe/aem-project-archetype) 或更新版本。 若要建立 [!DNL Experience Manager Forms] as a [!DNL Cloud Service] 以AEM原型為基礎的專案：
   </br> 開啟命令提示字元，然後執行以下命令以建立 [!DNL Experience Manager Forms] as a Cloud Service專案：

   ```shell
   mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=27 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
   ```

   此外，變更 `appTitle`, `appId`，和 `groupId`，以反映您的環境。

1. 複製 [aem-forms-samples](https://github.com/adobe/aem-forms-docusign-sample) 存放庫。 此儲存庫包含DocuSign的自定義提交操作以及與DocuSign伺服器連接的配置詳細資訊。

1. 開啟在步驟1中建立的AEM Formsas a Cloud Service專案，以在您選擇的IDE中編輯。

1. 開啟 `[AEM Forms as a Cloud Service project]\pom.xml` 檔案進行編輯，並進行下列變更：

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

1. 在 `all/pom.xml` Cloud Service專案資料夾中可用的檔案：

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

1. 開啟命令提示字元並導覽至 `aem-forms-samples\forms-integration-docusign` （在步驟3中複製），並執行下列命令：

   ```shell
   mvn clean install -Dinstall.dir="<AEM Forms as a Cloud Service project path>/maven_repository"
   ```

   `<AEM Forms as a Cloud Service project path>` 表示在此過程的步驟1中建立的資料夾的名稱。

1. 將專案部署至本機開發環境。 您可以使用下列命令來部署至本機開發環境

   `mvn -PautoInstallPackage clean install`

   執行這些步驟後，您可以檢視新的自訂提交動作 [使用DocuSign電子簽名提交](#enabledocusign) 可在最適化表單和 [DocuSign雲端服務設定](#configure-docusign-with-aem-forms) 在您的本機開發環境中。

1. 編譯和 [將程式碼部署至 [!DNL AEM Forms] as a Cloud Service環境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#customer-releases).

## 整合 [!DNL DocuSign] with [!DNL AEM Forms] {#configure-docusign-with-aem-forms}

準備就緒後，請執行下列步驟以整合 [!DNL DocuSign] with [!DNL AEM Forms] 在Author例項上。

1. 導覽至 **[!UICONTROL 工具]** ![錘](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL DocuSign]** 並選取要托管配置的資料夾。

1. 在設定頁面上，點選 **[!UICONTROL 建立]** 建立 [!DNL DocuSign] 設定(在AEM Forms中)。
1. 在 **[!UICONTROL 一般]** 的 **[!UICONTROL 建立DocuSign配置]** 頁面，指定 **[!UICONTROL 名稱]** ，然後點選 **[!UICONTROL 下一個]**. 您可以選擇指定 **[!UICONTROL 標題]**.

1. 將您目前瀏覽器視窗中的 URL 複製到筆記本。在後續步驟中，需要使用此 URL 設定 [!DNL DocuSign] 應用程式和 [!DNL AEM Forms]。

1. 設定 [!DNL DocuSign] 應用程式的 OAuth 設定：

   1. 開啟瀏覽器視窗並登入您的 [!DNL DocuSign] [開發人員帳戶](https://admindemo.docusign.com/apps-and-keys).
   1. 開啟為 [!DNL AEM Forms].
   1. 在 **[!UICONTROL 重定向URI]** 框中，添加在上一步中複製的URL，然後按一下 **[!UICONTROL 儲存]**.
   1. 記下整合金鑰和機密金鑰。

   如需設定 [!DNL DocuSign] 應用程式的 OAuth 設定並取得金鑰的逐步資訊，請參閱「[設定應用程式的 OAuth 設定](https://support.docusign.com/guides/ndse-admin-guide-api-and-keys)」開發人員文件。

1. 返回 **[!UICONTROL 建立DocuSign配置]** 頁面。 在 **[!UICONTROL 設定]** 標籤 **[!UICONTROL OAuth URL]** 欄位提及下列預設URL:

   `https://account-d.docusign.com/oauth/auth`

1. 指定 **[!UICONTROL 用戶端ID]** （DocuSign整合金鑰）和 **[!UICONTROL 用戶端密碼]** （DocuSign密鑰）。

1. 點選 **[!UICONTROL 連接到DocuSign]**. 出現認證提示時，請提供在建立 [!DNL DocuSign] 應用程式時使用的帳戶使用者名稱和密碼。當要求確認 `your developer account`，按一下 **[!UICONTROL 允許存取]**. 如果憑證正確，則會顯示成功訊息。

1. 點選 **[!UICONTROL 建立]** 建立 [!DNL DocuSign] 設定。

1. 選取設定，然後按一下 **[!UICONTROL 發佈]**，選取設定，然後按一下 **[!UICONTROL 發佈]**. 這會將設定複寫至對應的發佈環境。

1. 請對您的開發人員、中繼及生產執行個體 (無論是哪個) 重複上述步驟，以完成您環境的設定 [!DNL DocuSign] with [!DNL AEM Forms]。

現在，您的AEM Forms環境已設定為使用DocuSign。 請確保您將用於 Cloud Service 的設定容器新增至 [!DNL DocuSign] 啟用的所有最適化表單。您可從最適化表單的屬性指定設定容器。

### 使用 [!DNL DocuSign] 在適用性表單中 {#enabledocusign}

您可以啟用 [!DNL DocuSign] 適用於現有適用性表單，或建立 [!DNL DocuSign] 啟用適用性表單。 選擇以下選項之一：

- [建立 [!DNL DocuSign] 啟用適用性表單](#create-an-adaptive-form-for-docusign)
- [啟用 [!DNL DocuSign] 適用於現有適用性表單](#editafsign).

#### 建立DocuSign適用性表單 {#create-an-adaptive-form-for-docusign}

若要建立啟用符號的適用性表單：

1. 導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 點選 **[!UICONTROL 建立]** 選取 **[!UICONTROL 適用性表單]**. 此時將顯示模板清單。 選取範本並點選 **[!UICONTROL 下一個]**.
1. 在 **[!UICONTROL 基本]** 標籤：

   1. 指定 **[!UICONTROL 名稱]** 和 **[!UICONTROL 標題]** （適用於適用性表單）。

   1. 選取 [組態容器](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) 建立時間 [整合 [!DNL DocuSign] with [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).
   設定容器包含 [!DNL DocuSign] Cloud Services已針對您的環境進行設定。 這些服務可在適用性表單編輯器中選取。

1. 在 **[!UICONTROL 表單模型]** 頁簽，選擇以下選項之一：

   - 如果您有自訂表單範本，並需要根據表單範本的記錄檔案，請選取 **[!UICONTROL 將表單模板與記錄文檔模板關聯]** 選項並選擇「記錄文檔」模板。 使用選項時，為簽名而發送的文檔將僅顯示基於關聯表單模板的那些欄位。 它不會顯示最適化表單的所有欄位。

   - 如果您沒有自訂表單範本，請選取 **[!UICONTROL 生成記錄文檔]** 選項。 使用選項時，為簽署而傳送的檔案會顯示最適化表單的所有欄位。

1. 點選 **[!UICONTROL 建立。]** 已建立啟用符號的適用性表單。 您可以新增 [!DNL DocuSign] 欄位至表單中，並傳送以供簽署。
1. 在編輯模式中開啟最適化表單。 在 **[!UICONTROL 內容]** 標籤，點選 **[!UICONTROL 表單容器]** 點選 ![設定](assets/configure-icon.svg).

1. 在 **[!UICONTROL 提交]** 部分，選擇 **[!UICONTROL 使用DocuSign電子簽名提交]** 從 **[!UICONTROL 提交動作]** 下拉式清單。

1. 在 **[!UICONTROL 動作設定]** 區段，點選 **[!UICONTROL 新增]** 添加收件人並指定收件人的電子郵件地址。 點選 **[!UICONTROL 新增]** 以新增更多收件者。

1. 在 **[!UICONTROL 電子郵件主旨]** 欄位。 選擇 **包含附件** 在電子郵件中包含附件。

1. 點選 ![儲存](assets/save_icon.svg) 以儲存屬性。

#### 啟用 [!DNL DocuSign] 適用於適用性表單 {#editafsign}

使用 [!DNL DocuSign] 在現有適用性表單中：

1. 導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 選取「最適化表單」並點選 **[!UICONTROL 屬性]**.
1. 在 **[!UICONTROL 基本]** 頁簽，選擇 [組態容器](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) 在整合時建立 [!DNL DocuSign] with [!DNL AEM Forms].
1. 在 **[!UICONTROL 表單模型]** 頁簽，選擇以下選項之一：

   - 如果您有自訂表單範本，並需要根據表單範本的記錄檔案，請選取 **[!UICONTROL 將表單模板與記錄文檔模板關聯]** 選項並選擇「記錄文檔」模板。 使用選項時，為簽名而發送的文檔將僅顯示基於關聯表單模板的那些欄位。 它不會顯示最適化表單的所有欄位。

   - 如果您沒有自訂表單範本，請選取 **[!UICONTROL 生成記錄文檔]** 選項。 使用選項時，為簽署而傳送的檔案會顯示最適化表單的所有欄位。

1. 點選 **[!UICONTROL 儲存並關閉]**. 適用性表單已啟用 [!DNL DocuSign]. 現在，您可以將 [!DNL DocuSign] 欄位至表單中，並傳送以供簽署。

1. 在編輯模式中開啟最適化表單。 在 **[!UICONTROL 內容]** 標籤，點選 **[!UICONTROL 表單容器]** 點選 ![設定](assets/configure-icon.svg).

1. 在 **[!UICONTROL 提交]** 部分，選擇 **[!UICONTROL 使用DocuSign電子簽名提交]** 從 **[!UICONTROL 提交動作]** 下拉式清單。

1. 在 **[!UICONTROL 動作設定]** 區段，點選 **[!UICONTROL 新增]** 添加收件人並指定收件人的電子郵件地址。 點選 **[!UICONTROL 新增]** 以新增更多收件者。

1. 在 **[!UICONTROL 電子郵件主旨]** 欄位。 選擇 **包含附件** 在電子郵件中包含附件。

1. 點選 ![儲存](assets/save_icon.svg) 以儲存屬性。
