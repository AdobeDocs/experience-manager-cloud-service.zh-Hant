---
title: Repository Modernizer (CAM)
description: 瞭解如何重新建構現有的專案套件，使其與針對Adobe Experience Manager as a Cloud Service定義的專案結構相容。
feature: Migration
role: Admin
source-git-commit: 317ee65786d48d7b92d95c7c6b8782f617d6e346
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 2%

---


# Repository Modernizer (CAM) {#repo-modernizer-cam}

Repository Modernizer是專為重組現有專案套件而開發的公用程式，其將內容和程式碼分割為獨立套件，以與Adobe Experience Manager as a Cloud Service定義的專案結構相容。

## 簡介 {#introduction}

Adobe Experience Manager as a Cloud Service為您的AEM專案提供許多新功能和可能性。 不過，Adobe Experience Manager Maven專案必須進行一些變更，才能與AEM雲端服務相容。 在高層面上，AEM需要將&#x200B;**內容**&#x200B;和&#x200B;**程式碼**&#x200B;分離為離散的子套件，以遵循可變和不可變內容之間的分割。 請參閱[AEM專案結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=zh-Hant)，以取得Cloud Service新AEM專案結構的詳細資訊。

Repository Modernizer會建立下列部署結構，以建立相容的AEM Cloud Service專案結構：

- `ui.apps`套件部署至`/apps`並包含所有程式碼

- `ui.content`套件部署到執行階段可寫入的區域（例如，`/content`、`/conf`、`/home`或非`/apps`的任何專案）並包含所有內容和設定。

- `all`封裝是包含子封裝`ui.apps`和`ui.content`的容器封裝。

>[!NOTE]
>
> 專案結構是以封裝及其`pom.xml/filter.xml files`的&#x200B;_原型48_&#x200B;為基礎。 如需詳細資訊，請參閱[原型48](https://github.com/adobe/aem-project-archetype)。

Repository Modernizer現在也支援下列專案型別：

- **MULTI_PROJECT**：代表沒有共同父級POM、Dispatcher和所有模組的多模組專案。
- **SINGLE_PROJECT**：代表單一專案。
- **NESTED_PROJECT**：代表具有共同父系POM、Dispatcher和所有模組的多模組專案。
- **MONOLITHIC_PROJECT**：代表包含一或多個子專案的主專案。

## 使用Repository Modernizer {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/333057/?quality=12&learn=on)

- Repository Modernizer現在會由「重構工作」標籤下的「重構服務」自動叫用。 客戶只需要上傳其專案並觸發重構工作，不需要其他設定。

## 錯誤代碼參考

如果您在使用Repository Modernizer時遇到錯誤代碼，請參閱下表以瞭解詳細資訊和建議的動作。

| 錯誤碼 | 訊息 | 說明 | 需要使用者動作？ |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- | --------------------- |
| RM-100 | 將OSGi設定檔{0}轉換為.cfg.json格式時發生錯誤。 請先驗證現有的設定檔，然後再試一次。 | 將OSGi設定檔案轉換為.cfg.json格式期間發生問題時，會發生此錯誤。 | 是 |
| RM-101 | 嘗試複製下列來源的內容時發生錯誤： {0} | 嘗試從指定的來源複製內容時發生失敗時，就會發生此錯誤。 | 否 |
| RM-102 | 嘗試將檔案{0}從{1}移動到{2}時發生錯誤。 | 將檔案從一個位置移動到另一個位置時出現此錯誤。 | 否 |
| RM-103 | 無法將指定的路徑解析為有效的檔案： {0} | 在指定位置找不到檔案時，會發生此錯誤。 | 否 |
| RM-104 | 反複處理{0}的內容時發生錯誤。 | 周遊檔案或目錄期間發生此錯誤，表示存取或處理內容時發生問題。 | 否 |
| RM-105 | 嘗試剖析XML檔案時發生錯誤： {0}。 請先驗證XML檔案，然後再試一次。 | 剖析XML檔案失敗時，會發生此錯誤。 | 是 |
| RM-106 | 寫入XML檔案時發生錯誤： {0}。 | 當寫入XML檔案時發生問題時，就會發生這個錯誤。 | 否 |
| RM-107 | 在現有專案中找不到內容封裝： {0}。 請驗證是否已上傳正確的專案。 | 此錯誤表示在現有專案中找不到內容套件。 | 是 |
| RM-108 | 在預期的路徑找不到POM檔案： {0}。 專案或模組的POM檔案應直接位於其目錄中，做為子檔案。 | 在預期位置找不到POM檔案時，就會發生此錯誤。 | 是 |
| RM-109 | 嘗試剖析pom.xml檔案時發生錯誤： {0}。 請先驗證pom檔案，然後重試。 | 剖析pom.xml檔案時發生問題時，會發生此錯誤。 | 是 |
| RM-110 | 寫入pom.xml檔案時發生錯誤： {0}。 | 當寫入pom檔案時發生問題時，就會發生此錯誤。 | 否 |
| RM-111 | 寫入報告檔案時發生錯誤。 | 當寫入報表檔案的過程中發生失敗時，就會發生此錯誤。 | 否 |
| RM-112 | 在({1})的存放庫結構pom檔案中找不到{0} | 在AEM專案原型範本中找不到預期的設定時，就會發生此錯誤。 | 否 |
| RM-113 | 嘗試將AEM專案原型範本複製到目的地時發生錯誤。 | 將AEM專案原型範本複製到目的地時出現此錯誤。 | 否 |
| RM-115 | 嘗試連線到Azure Blob儲存體時發生錯誤。 | 當連線到Azure Blob儲存體時發生問題時，就會發生此錯誤。 | 否 |
| RM-116 | 嘗試將檔案{0}上傳到Azure Blob儲存體時發生錯誤。 | 上傳檔案至Azure Blob儲存體時發生問題時，會發生此錯誤。 | 否 |
| RM-117 | 嘗試從Azure Blob儲存體下載檔案{0}時發生錯誤。 | 當從Azure Blob儲存下載檔案時發生問題時，會發生此錯誤。 | 否 |
| RM-118 | 處理{0}時發生I/O錯誤。 | 當讀取或寫入專案檔案時發生問題時，會發生此錯誤。 | 否 |
| RM-119 | 嘗試封存上傳至Azure的結果時發生I/O錯誤。 | 當封存處理程式產生的結果時發生錯誤，就會發生此錯誤。 | 否 |
| RM-120 | 嘗試取消封存提供的專案zip時發生I/O錯誤。 請檢查提供的專案zip是否有效。 | 取消封存特定客戶專案時發生錯誤，就會發生此錯誤。 | 是 |
| RM-121 | 寫入組態檔時發生錯誤。 | 當寫入組態檔的過程中發生失敗時，就會發生此錯誤。 | 否 |
| RM-122 | 不支援的要求型別： {0}。 | 當系統不支援請求型別時，會發生此錯誤。 請檢查請求型別，然後重試。 | 否 |

## 瞭解搜尋結果報表優先順序

當您下載Repository Modernizer工具產生的結果報告時，每個結果都會被指派一個&#x200B;**優先順序**。 這些優先順序可協助您瞭解每個問題的急迫性和影響：

| 優先順序 | 說明 |
| -------- | ----------------------------------------------------------------------------------------------- |
| 關鍵 | 必須解析才能成功建置專案。 |
| 高 | 應該加以解析，以確保AEM中的功能不會損毀。 |
| 一般 | 應該解決問題，以確保現代化的整體健全性與完整性。 |
| 低 | 對於手動驗證；這些發現僅供參考，不需要立即操作。 |

>[!NOTE]
> 
>建議先處理優先順序較高的發現，以確保順利的現代化和部署程式。
