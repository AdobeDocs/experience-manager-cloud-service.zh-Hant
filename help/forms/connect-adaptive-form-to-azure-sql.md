---
Title: How to Connect AEM Adaptive Forms with Azure SQL Storage
Description: Learn how to configure an Azure SQL Database connection in AEM Forms and integrate it with your Adaptive Forms to store or retrieve data efficiently using JDBC.
Keywords: Azure SQL integration with AEM Forms, Connecting Adaptive Forms to Azure SQL Database, JDBC connection for Azure SQL in AEM Forms, Storing Adaptive Form data in Azure SQL
feature: Adaptive Forms, Core Components
role: User, Developer
source-git-commit: e29f70aa1a8164787c7d310a05c24d7e501803e5
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 2%

---

# 將最適化表單連線至Azure SQL儲存體

Adobe Experience Manager (AEM)中的最適化Forms可與外部資料庫整合，以儲存或擷取資料。
本文概述如何透過AEM as a Cloud Service使用JDBC將調適型表單連結至Azure SQL資料庫。

>
> 
> 本指南適用於已啟用進階網路的非沙箱AEM as a Cloud Service環境。

## 優點

將Adaptive Forms與Azure SQL整合有幾項優點：

* **即時資料互動：**&#x200B;啟用表單與Azure資料庫之間的資料即時讀取與寫入。
* **可擴充性：** Azure SQL提供適合企業級應用程式的可擴充資料庫效能。
* **集中式資料儲存：**&#x200B;將表單提交與擷取的資料安全地儲存在單一中央位置。
* **安全性法規遵循：**&#x200B;利用Azure的內建網路、防火牆和加密選項，確保安全通訊。
* **雲端原生整合：**&#x200B;適用於使用AEM as a Cloud Service的現代、雲端優先架構。

## 先決條件

* 建立[Azure SQL資料庫](https://learn.microsoft.com/en-us/azure/azure-sql/database/single-database-create-quickstart?view=azuresql&tabs=azure-portal)並確保已啟用&#x200B;**代理連線**。

  >[!NOTE]
  >
  > 瀏覽至： `Azure Portal → SQL Server → Security → Networking → Connectivity`以啟用&#x200B;**代理連線**。

  ![建立Azure Db](/help/forms/assets/create-azure-db.png)

* 啟用為已建立的Azure資料庫使用專用輸出IP[設定的](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/networking/dedicated-egress-ip-address)進階網路。

  >[!NOTE]
  >
  >    啟用專用輸出IP之後。 移至`Azure Portal → SQL Server → Security → Networking → Public Access`並將輸出IP新增至防火牆規則。

  ![輸出IP](/help/forms/assets/cretae-azure-db-egress-ip.png)

* 在雲端環境中使用下列專案設定連線埠轉送：
   * **連線埠原點**：介於`30000–30999`之間
   * **portDest**： `1433` （Azure SQL的預設連線埠）
例如： `portOrigin: 30433 → portDest: 1433`

     >
     > 
     > 您可以聯絡Adobe Cloud Manager支援以設定連線埠轉送。


## 將Adaptive Forms連線至Azure SQL的步驟

**步驟1：複製AEM as a Cloud Service Git存放庫**

1. 開啟命令列，並選擇要儲存AEM as a Cloud Service存放庫的目錄，例如`/cloud-service-repository/`。

1. 執行以下命令以複製存放庫：

   ```
   git clone https://git.cloudmanager.adobe.com/<organization-name>/<app-id>/
   ```

   **在哪裡可以找到此資訊？**

   如需尋找這些詳細資訊的逐步指示，請參閱Adobe Experience League文章&quot;[存取Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git)&quot;。

   當命令成功完成時，您會看到在本機目錄中建立的新資料夾。 此資料夾是以您的應用程式命名。

1. 在編輯器中開啟存放庫資料夾。

**步驟2：新增必要的JAR**

透過[套件將](https://central.sonatype.com/artifact/com.microsoft.sqlserver/mssql-jdbc/12.8.0.jre11?smo=true)SQL驅動程式相依性`all`包含到AEM專案：

>[!NOTE]
>
> 若要在專案中包含SQL相依性，請參閱[SQL驅動程式相依性](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool#mysql-driver-dependencies)區段。

**步驟3：新增JDBC設定**

1. 導覽至`<application folder>`中的下列目錄，其中應放置JDBC集區的OSGi設定：

   ```bash
   cd ui.config/src/jcr_root/apps/<application folder>/osgiconfig/config/
   ```

**步驟4：建立Azure SQL連線組態檔**

1. 建立檔案：

   ```bash
   com.day.commons.datasource.jdbcpool.JdbcPoolService~<application folder>-sql.cfg.json
   ```

1. 新增下列幾行程式碼：

   ```json
   {
   "datasource.name": "azuredbshr",
   "jdbc.driver.class": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
   "jdbc.username": "<azureuser>",
   "jdbc.connection.uri": "jdbc:sqlserver://$[env:AEM_PROXY_HOST;default=proxy.tunnel]:30433;database=testdb;user=<azureuser>;password=<azurepassword>;encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;",
   "jdbc.password": "******",
   "jdbc.validation.query": "SELECT 1"
       }
   ```

   >
   >
   > 以實際的Azure使用者名稱取代`jdbc.username`，並以實際的安全密碼取代`jdbc.password`。

**步驟5：認可並推送變更**

開啟終端機並執行下列命令：

```bash
git add .
git commit -m "<commit message>"
git push 
```

**步驟6：透過Cloud Manager管道部署變更**

1. 登入&#x200B;**AEM Cloud Manager**。
1. 導覽至您的專案並執行管道以部署變更。

**步驟7：建立表單資料模型(FDM)**

完成AEM和Azure設定並部署程式碼變更後：

1. 前往AEM Author例項。
1. 導覽至&#x200B;**工具** > **Forms** > **資料整合**。
1. 建立新的&#x200B;**表單資料模型**。
1. 在&#x200B;**資料來源**&#x200B;索引標籤中，選取已建立的JDBC組態。
1. 按一下[建立&#x200B;****]並驗證連線。

![建立表單資料模型](/help/forms/assets/create-azure-sql-fdm.png)

**步驟8：在最適化表單中使用已建立的FDM**

1. 在編輯模式中開啟最適化表單。
1. 選取上一步建立的FDM作為資料模型。
1. 使用[資料繫結將表單欄位連線到Azure SQL資料來源](/help/forms/work-with-form-data-model.md#add-data-model-objects-and-services)並設定提交動作。

## 最佳做法

* 使用&#x200B;**密碼管理**&#x200B;避免在組態檔中硬式編碼密碼。
* 定期輪換資料庫認證，並安全地更新設定。
* 監視JDBC連線記錄檔的失敗和延遲。
* 遵循Azure最佳實務，以保護SQL資料庫和防火牆組態的安全。
* 避免使用高許可權資料庫帳戶來存取表單。

## 相關文章

{{af-submit-action}}