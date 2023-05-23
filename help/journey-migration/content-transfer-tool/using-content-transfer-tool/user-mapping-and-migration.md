---
title: 使用者對應和主體移轉
description: 用戶映射和主遷移概述
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
source-git-commit: 91a13f8b23136298e0ccf494e51fccf94fa1e0b4
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 8%

---

# 使用者對應和主體移轉 {#user-mapping-and-principal-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="使用者對應"
>abstract="內容傳輸工具可幫助您將用戶和組從現有Adobe Experience Manager(AEM)系統移到AEMas a Cloud Service。 現有使用者需要對應到他們的 IMS ID，以避免 Cloud Service 製作執行個體上出現重複的使用者。"

>[!NOTE]
>有關用戶映射工具的早期版本，請參閱 [舊文檔](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md)。

## 簡介 {#introduction}

在向Adobe Experience Manager(AEM)as a Cloud Service過渡的過程中，必須將用戶和組從現有系統移AEM動到AEMas a Cloud Service。 此任務由內容傳輸工具完成。

AEM as a Cloud Service 最重大的變更是完全整合使用 Adobe ID 以存取作者層。此過程需要使用 [Adobe Admin Console](https://helpx.adobe.com/tw/enterprise/using/admin-console.html) 用於管理用戶和組。 用戶配置檔案資訊集中在AdobeIdentity Management系統(IMS)中，該系統在所有Adobe雲應用程式中提供單點登錄。 有關詳細資訊，請參閱 [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html#identity-management)。 由於這一更改，現有用戶必須映射到其IMS ID以避免在Cloud Service作者實例上出現重複用戶。 由於傳統的AEM組與IMS中的組有根本的不同，所以組不是映射的，但是遷移完成後必須協調這兩組組。

## 用戶映射和遷移詳細資訊 {#user-mapping-detail}

內容傳輸工具和雲加速管理器可遷移與要遷移的內容相關聯的所有用戶。 此映射是自動完成的，在啟動提取之前，可以通過切換控制是否完成。 用戶在開始提取時可以覆蓋切換的預設設定。

* 如果源系統是作者實例，則預設情況下執行映射的選擇是 _上_，因為它是推薦的流程。
* 如果源系統是發佈實例，則預設情況下執行映射的選擇是 _關_，因為用戶通常不會遷移或用於發佈實例。

## 對應和移轉使用者的重要注意事項 {#important-considerations}


### 特殊案件 {#exceptional-cases}

記錄了以下特定案例：

1. 如果用戶在 `profile/email` 他們 *jcr* 節點，可能遷移該用戶或組，但未映射。 即使電子郵件地址用作登錄的用戶名，此情況也是如此。

1. 如果用戶被禁用，則其處理方式與未禁用時相同。 它按正常方式映射和遷移，並在雲實例上保持禁用狀態。

1. 如果目標AEM Cloud Service實例上存在與源實例上的用戶之一具有相同用戶名(rep:principalName)的用戶AEM，則不遷移有關用戶。

1. 如果用戶在未通過用戶映射方式進行映射的情況下被遷移，則在目標雲系統上，他們無法使用其IMS ID登錄。 或者，如果其電子郵件地址與用於登錄IMS的電子郵件地址不匹配，則在目標雲系統上，他們也無法使用其IMS ID登錄。 他們可能能夠使用傳統方法登AEM錄，但此方法通常不是想要或期望的。


## 其他注意事項 {#additional-considerations}

* 如果設定 **在接收之前擦除雲實例上的現有內容** 設定，已傳輸的Cloud Service實例上的用戶將與整個現有儲存庫一起刪除。 此外，還會建立一個新的儲存庫，將內容放入其中。 此進程還重置所有設定，包括對目標Cloud Service實例的權限，對於添加到 **管理員** 組。 必須將管理員用戶讀入 **管理員** 組以檢索CTT的訪問令牌。
* 執行內容追加時，如果內容自上次傳輸後未更改而未傳輸，則與該內容關聯的用戶和組也不會傳輸。 即使用戶和組同時發生更改，此規則仍為真。 原因是用戶和組與其關聯的內容一起遷移。
* 如果目標AEM Cloud Service實例具有與源實例上的某個用戶具有不同用戶名但電子郵件地址相同的用戶AEM，並且啟用了「用戶映射」，則日誌會記錄錯誤消息。 此外，源用AEM戶不會被傳輸，因為目標系統上只允許一個具有給定電子郵件地址的用戶。

## 最終摘要和報告 {#final-report}

一旦提取和接收成功完成，將生成顯示主遷移詳細資訊的報告。 請參閱 [如何驗證主遷移](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/validating-content-transfers.md#how-to-validate-principal-migration) 的上界。
