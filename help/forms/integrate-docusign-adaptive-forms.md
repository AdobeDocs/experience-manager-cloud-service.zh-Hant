---
title: 如何將DocuSign與最適化表單整合？
description: 瞭解如何搭配最適化表單使用DocuSign來收集電子簽章。
exl-id: fb2e75d6-e454-4999-a079-f663af79051f
feature: Adaptive Forms, Acrobat Sign
role: User, Developer
source-git-commit: ab84a96d0e206395063442457a61f274ad9bed23
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 8%

---

# 搭配最適化表單使用DocuSign {#integrate-aem-forms-with-DocuSign}

DocuSign是重要的電子簽章解決方案。 您可以用它來簽署合約。 您可以將DocuSign與最適化表單整合。 它可協助您傳送最適化表單以供多個收件者進行電子簽章。 使用電子簽章可協助您：

- 透過完全自動化的提案、報價及合約程式，完成任何裝置的交易。
- 更快地完成人力資源程式，並為員工提供數位體驗。
- 縮短合約週期時間，讓您的廠商更快上線。

AEM Forms as a Cloud Service提供DocuSign[的](#deploy-custom-submit-action)自訂提交動作。 提交動作可協助您使用DocuSign API傳送電子簽章的最適化表單。

| 您也可以使用Adobe的電子簽章解決方案Adobe Sign，在最適化表單上進行電子簽章。 AEM Forms與Adobe Sign的整合更深入，並提供更精細的控制項，例如循序與平行簽署、多種驗證方法、表單內簽署體驗等。 如需詳細資訊，請參閱[在最適化表單中使用Adobe Sign](working-with-adobe-sign.md)。 |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## 先決條件 {#prerequisites}

以下是DocuSign與AEM Forms整合的必要條件：

- DocuSign [開發人員帳戶](https://developers.docusign.com/platform/account/)
- docussign應用程式
- DocuSign API應用程式的認證（使用者端ID和使用者端密碼）。
- [適用於DocuSign的自訂提交動作和雲端服務](https://github.com/adobe/aem-forms-docusign-sample)
- （僅適用於本機開發環境） [設定記錄檔案](setup-local-development-environment.md#docker-microservices)。

## 設定適用於DocuSign的自訂提交動作和雲端服務 {#deploy-custom-submit-action}

AEM Forms as a Cloud Service提供DocuSign的自訂提交動作。 提交動作可協助您使用DocuSign API傳送電子簽章的最適化表單。 自訂提交動作的程式碼可在[AEM Forms範例公用Git存放庫](https://github.com/adobe/aem-forms-docusign-sample)上取得。 您可以在您的AEM Forms環境中部署程式碼，或根據您的組織需求自訂程式碼。

執行以下步驟，設定現成的自訂提交動作和DocuSign Cloud Service：

1. [複製AEM Forms as a Cloud Service專案](setup-local-development-environment.md#forms-cloud-service-local-development-environment)，或根據[!DNL Experience Manager Forms]AEM Archetype 27[!DNL Cloud Service]或更新版本將[建立為](https://github.com/adobe/aem-project-archetype)專案。 若要根據AEM Archetype將[!DNL Experience Manager Forms]建立為[!DNL Cloud Service]專案：
   </br>開啟命令提示字元並執行以下命令以建立[!DNL Experience Manager Forms] as a Cloud Service專案：

   ```shell
   mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=27 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
   ```

   此外，請變更上述命令中的`appTitle`、`appId`和`groupId`，以反映您的環境。

1. 複製[aem-forms-samples](https://github.com/adobe/aem-forms-docusign-sample)存放庫。 此存放庫包含用於DocuSign的自訂提交動作以及連線到DocuSign伺服器的設定詳細資料。

1. 開啟在步驟1建立的AEM Forms as a Cloud Service專案，以便在您選擇的IDE中進行編輯。

1. 開啟`[AEM Forms as a Cloud Service project]\pom.xml`檔案進行編輯，並進行下列變更：

   1. 在`<properties>`標籤的結尾新增下列文字：

      ```shell
      <repository.location>maven_repository</repository.location>
      ```

   1. 在`<repositories>`標籤的結尾新增下列文字：

      ```shell
       <repository>
          <id>project-repository</id>
          <url>file://${project.basedir}/${repository.location}</url>
       </repository>
      ```

      如果沒有`<repositories>`標籤，請在`<properties>`標籤下方建立標籤。

   1. 在`<dependencyManagement>`標籤的結尾新增下列文字：

      ```shell
       <dependency>
         <groupId>com.adobe.aemforms.samples</groupId>
         <artifactId>forms.integration.docusign.all</artifactId>
         <type>zip</type>
         <version>1.0.0</version>
       </dependency>
      ```

1. 在Cloud Service專案資料夾中可用的`all/pom.xml`檔案中執行以下步驟：

   1. 在`<embeddeds>`標籤的結尾新增下列文字：

      ```shell
       <embedded>
          <groupId>com.adobe.aemforms.samples</groupId>
          <artifactId>forms.integration.docusign.all</artifactId>
          <type>zip</type>
          <target>/apps/moonlightprodprogram-vendor-packages/application/install</target>
       </embedded>
      ```

   1. 在`<dependencies>`標籤的結尾新增下列文字：

      ```shell
       <dependency>
          <groupId>com.adobe.aemforms.samples</groupId>
          <artifactId>forms.integration.docusign.all</artifactId>
          <type>zip</type>
       </dependency>
      ```

1. 開啟命令提示字元並導覽至`aem-forms-samples\forms-integration-docusign` （複製於步驟3），然後執行下列命令：

   ```shell
   mvn clean install -Dinstall.dir="<AEM Forms as a Cloud Service project path>/maven_repository"
   ```

   `<AEM Forms as a Cloud Service project path>`參照此程式步驟1中建立的資料夾名稱。

1. 將專案部署到您的本機開發環境。 您可以使用以下命令來部署到您的本機開發環境

   `mvn -PautoInstallPackage clean install`

   執行這些步驟後，您可以檢視新的自訂提交動作[使用DocuSign電子簽章提交](#enabledocusign)，可在您本機開發環境中的最適化表單和[DocuSign雲端服務組態](#configure-docusign-with-aem-forms)的提交選項清單中取得。

1. 編譯程式碼並[將程式碼部署到您的 [!DNL AEM Forms] as a Cloud Service環境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=zh-Hant#customer-releases)。

## 將[!DNL DocuSign]與[!DNL AEM Forms]整合 {#configure-docusign-with-aem-forms}

已具備先決條件後，請執行以下步驟，在作者執行個體上整合[!DNL DocuSign]與[!DNL AEM Forms]。

1. 瀏覽至&#x200B;**[!UICONTROL 工具]** ![hammer](assets/hammer.png) > **[!UICONTROL 雲端服務]** > **[!UICONTROL DocuSign]**，並選取要裝載設定的資料夾。

1. 在設定頁面上，選取「**[!UICONTROL 建立]**」以在AEM Forms中建立[!DNL DocuSign]設定。
1. 在&#x200B;**[!UICONTROL 建立DocuSign組態]**&#x200B;頁面的&#x200B;**[!UICONTROL 一般]**&#x200B;標籤中，指定組態的&#x200B;**[!UICONTROL 名稱]**，並選取&#x200B;**[!UICONTROL 下一步]**。 您可以選擇指定&#x200B;**[!UICONTROL 標題]**。

1. 將您目前瀏覽器視窗中的 URL 複製到筆記本。在後續步驟中，需要使用此 URL 設定 [!DNL DocuSign] 應用程式和 [!DNL AEM Forms]。

1. 設定 [!DNL DocuSign] 應用程式的 OAuth 設定：

   1. 開啟瀏覽器視窗並登入您的[!DNL DocuSign] [開發人員帳戶](https://admindemo.docusign.com/apps-and-keys)。
   1. 開啟為[!DNL AEM Forms]設定的應用程式。
   1. 在&#x200B;**[!UICONTROL 重新導向URI]**&#x200B;方塊中，新增在上一步中複製的URL，然後按一下&#x200B;**[!UICONTROL 儲存]**。
   1. 記下整合與秘密金鑰。

   如需設定 [!DNL DocuSign] 應用程式的 OAuth 設定並取得金鑰的逐步資訊，請參閱「[設定應用程式的 OAuth 設定](https://support.docusign.com/guides/ndse-admin-guide-api-and-keys)」開發人員文件。

1. 返回&#x200B;**[!UICONTROL 建立DocuSign組態]**&#x200B;頁面。 在&#x200B;**[!UICONTROL 設定]**&#x200B;標籤中，**[!UICONTROL OAuth URL]**&#x200B;欄位提及下列預設URL：

   `https://account-d.docusign.com/oauth/auth`

1. 指定&#x200B;**[!UICONTROL 使用者端識別碼]** （DocuSign整合金鑰）和&#x200B;**[!UICONTROL 使用者端密碼]** （DocuSign密碼金鑰）。

1. 選取&#x200B;**[!UICONTROL 連線到DocuSign]**。 出現認證提示時，請提供在建立 [!DNL DocuSign] 應用程式時使用的帳戶使用者名稱和密碼。當要求確認`your developer account`的存取時，請按一下&#x200B;**[!UICONTROL 允許存取]**。 如果認證正確，則會顯示成功訊息。

1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以建立[!DNL DocuSign]組態。

1. 選取組態並按一下&#x200B;**[!UICONTROL 發佈]**，選取組態，然後按一下&#x200B;**[!UICONTROL 發佈]**。 這會將設定複寫至對應的發佈環境。

1. 請對您的開發人員、中繼及生產執行個體 (無論是哪個) 重複上述步驟，以完成您環境的設定 [!DNL DocuSign] with [!DNL AEM Forms]。

現在，您的AEM Forms環境已設定為使用DocuSign。 請確保您將用於 Cloud Service 的設定容器新增至 [!DNL DocuSign] 啟用的所有最適化表單。您可以從最適化表單的屬性指定設定容器。

### 在最適化表單中使用[!DNL DocuSign] {#enabledocusign}

您可以為現有的調適型表單啟用[!DNL DocuSign]，或建立啟用[!DNL DocuSign]的調適型表單。 選擇下列其中一項：

- [建立啟用 [!DNL DocuSign] 的最適化表單](#create-an-adaptive-form-for-docusign)
- 針對現有的最適化表單[啟用 [!DNL DocuSign] ](#editafsign)。

#### 為DocuSign建立最適化表單 {#create-an-adaptive-form-for-docusign}

若要建立可啟用簽名的最適化表單：

1. 導覽至「**[!UICONTROL Adobe Experience Manager]**」>「**[!UICONTROL 「表單]**」>「**[!UICONTROL 表單與文件]**」。
1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;並選取&#x200B;**[!UICONTROL 最適化表單]**。 範本清單隨即顯示。 選取範本並選取&#x200B;**[!UICONTROL 下一步]**。
1. 在&#x200B;**[!UICONTROL 基本]**&#x200B;索引標籤中：

   1. 指定最適化表單的&#x200B;**[!UICONTROL 名稱]**&#x200B;和&#x200B;**[!UICONTROL 標題]**。

   1. 選取[整合](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms)與[時所建立的 [!DNL DocuSign] 設定容器 [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md)。

   設定容器包含為您的環境設定的[!DNL DocuSign]雲端服務。 這些服務可在最適化表單產生器中選擇。

1. 在&#x200B;**[!UICONTROL 表單模型]**&#x200B;索引標籤中，選取下列其中一個選項：

   - 如果您有自訂表格範本，而且需要以表格範本為基礎的記錄檔案，請選取&#x200B;**[!UICONTROL 關聯表格範本作為記錄檔案範本]**&#x200B;選項，並選取記錄檔案範本。 當您使用選項時，傳送以供簽署的檔案只會顯示以相關表單範本為基礎的欄位。 它不會顯示最適化表單的所有欄位。

   - 如果您沒有自訂表格範本，請選取&#x200B;**[!UICONTROL 產生記錄檔案]**&#x200B;選項。 當您使用選項時，傳送以供簽署的檔案會顯示最適化表單的所有欄位。

1. 選擇 **[!UICONTROL 建立]**。系統隨即會建立可啟用簽名的最適化表單。 您可以將[!DNL DocuSign]欄位新增至表單，並傳送以進行簽署。
1. 在編輯模式中開啟最適化表單。 在&#x200B;**[!UICONTROL 內容]**&#x200B;索引標籤中，選取&#x200B;**[!UICONTROL 表單容器]**，然後選取![設定](assets/configure-icon.svg)。

1. 在&#x200B;**[!UICONTROL 提交]**&#x200B;區段中，從&#x200B;**[!UICONTROL 提交動作]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL 使用DocuSign電子簽章提交]**。

1. 在&#x200B;**[!UICONTROL 動作組態]**&#x200B;區段中，選取&#x200B;**[!UICONTROL 新增]**&#x200B;以新增收件者並指定收件者的電子郵件地址。 再次選取&#x200B;**[!UICONTROL 新增]**&#x200B;以新增更多收件者。

1. 在&#x200B;**[!UICONTROL 電子郵件主旨]**&#x200B;欄位中指定電子郵件訊息的主旨。 選取&#x200B;**包含附件**&#x200B;以在電子郵件訊息中包含附件。

1. 選取![儲存](assets/save_icon.svg)以儲存屬性。

#### 為最適化表單啟用[!DNL DocuSign] {#editafsign}

若要在現有的最適化表單中使用[!DNL DocuSign]：

1. 導覽至「**[!UICONTROL Adobe Experience Manager]**」>「**[!UICONTROL 「表單]**」>「**[!UICONTROL 表單與文件]**」。
1. 選取最適化表單並選取&#x200B;**[!UICONTROL 屬性]**。
1. 在&#x200B;**[!UICONTROL 基本]**&#x200B;索引標籤中，選取整合[與](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms)時所建立的[!DNL DocuSign]設定容器[!DNL AEM Forms]。
1. 在&#x200B;**[!UICONTROL 表單模型]**&#x200B;索引標籤中，選取下列其中一個選項：

   - 如果您有自訂表格範本，而且需要以表格範本為基礎的記錄檔案，請選取&#x200B;**[!UICONTROL 關聯表格範本作為記錄檔案範本]**&#x200B;選項，並選取記錄檔案範本。 當您使用選項時，傳送以供簽署的檔案只會顯示以相關表單範本為基礎的欄位。 它不會顯示最適化表單的所有欄位。

   - 如果您沒有自訂表格範本，請選取&#x200B;**[!UICONTROL 產生記錄檔案]**&#x200B;選項。 當您使用選項時，傳送以供簽署的檔案會顯示最適化表單的所有欄位。

1. 選取&#x200B;**[!UICONTROL 儲存並關閉]**。 已為[!DNL DocuSign]啟用最適化表單。 現在，您可以將[!DNL DocuSign]欄位新增至表單，並傳送以進行簽署。

1. 在編輯模式中開啟最適化表單。 在&#x200B;**[!UICONTROL 內容]**&#x200B;索引標籤中，選取&#x200B;**[!UICONTROL 表單容器]**，然後選取![設定](assets/configure-icon.svg)。

1. 在&#x200B;**[!UICONTROL 提交]**&#x200B;區段中，從&#x200B;**[!UICONTROL 提交動作]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL 使用DocuSign電子簽章提交]**。

1. 在&#x200B;**[!UICONTROL 動作組態]**&#x200B;區段中，選取&#x200B;**[!UICONTROL 新增]**&#x200B;以新增收件者並指定收件者的電子郵件地址。 再次選取&#x200B;**[!UICONTROL 新增]**&#x200B;以新增更多收件者。

1. 在&#x200B;**[!UICONTROL 電子郵件主旨]**&#x200B;欄位中指定電子郵件訊息的主旨。 選取&#x200B;**包含附件**&#x200B;以在電子郵件訊息中包含附件。

1. 選取![儲存](assets/save_icon.svg)以儲存屬性。
