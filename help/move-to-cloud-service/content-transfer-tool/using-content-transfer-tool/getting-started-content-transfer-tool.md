---
title: 內容轉移工具快速入門
description: 內容轉移工具快速入門
exl-id: a19b8424-33ab-488a-91b3-47f0d3c8abf5
source-git-commit: 19c84c9acaf8202dcb96ff25b4d674555ebc2d92
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 32%

---

# 內容轉移工具快速入門 {#getting-started-content-transfer-tool}

## 可用性 {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="下載"
>abstract="您可以從軟體發佈入口網站下載「內容轉移工具」的ZIP檔案。 您可以透過「封裝管理程式」，在來源 Adobe Experience Manager AEM) 例項上安裝封裝。請務必下載最新版本。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html" text="發行說明"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="Software Distribution入口網站"

您可以從軟體發佈入口網站下載「內容轉移工具」的ZIP檔案。 您可以透過「封裝管理程式」，在來源 Adobe Experience Manager AEM) 例項上安裝封裝。請務必下載最新版本。 如需最新版本的詳細資訊，請參閱[發行說明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hant)。

>[!NOTE]
>從[軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)入口網站下載內容轉移工具。

## 執行「內容轉移工具」  {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="執行內容轉移工具"
>abstract="了解如何使用「內容轉移工具」將內容移轉至AEMas a Cloud Service（製作/發佈）。"
>additional-url="https://video.tv.adobe.com/v/35460/?quality=12&amp;learn=on" text=" 請參閱示範"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration" text="教學課程 — 使用內容轉移工具"

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)


請依照以下章節了解如何使用「內容轉移工具」，將內容移轉至 AEM as a Cloud Service (製作/發佈)：

1. 選取Adobe Experience Manager並導覽至工具 — > **操作** -> **內容移轉**。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt01.png)

1. 從&#x200B;**內容遷移**&#x200B;嚮導中選擇&#x200B;**內容轉移**&#x200B;選項。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt02.png)


1. 建立第一個移轉集時，會顯示下列主控台。 按一下&#x200B;**建立移轉集**&#x200B;以建立新的移轉集。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt03.png)

   >[!NOTE]
   >如果您有現有的移轉集，主控台會顯示現有移轉集清單及其目前狀態。


1. 按照下面所述，填入&#x200B;**建立移轉集**&#x200B;畫面中的欄位。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt04.png)

   1. **名稱**：輸入移轉集名稱。
      >[!NOTE]
      >移轉集名稱不允許使用特殊字元。

   1. **Cloud Service 設定**：輸入目標 AEM as a Cloud Service 製作 URL。

      >[!NOTE]
      >在內容轉移活動期間，您一次最多可以建立並維護10個移轉集。
      >此外，您還須針對每個特定環境 (*預備*、*開發*&#x200B;或&#x200B;*生產*) 分別建立移轉。

   1. **存取 Token**：輸入存取 Token。

      >[!NOTE]
      >您可以使用&#x200B;**開啟存取權杖**&#x200B;按鈕來擷取存取權杖。 您必須確保您屬於目標Cloud Service例項中的AEM管理員群組。

   1. **參數**：選取以下參數以建立移轉集：

      1. **包含版本**：視需要選取。包含版本時，會自動包含路徑`/var/audit`以遷移審核事件。

      ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt05.png)

      >[!NOTE]
      >如果您要將版本納入移轉集，並要使用`wipe=false`執行追加，則必須由於「內容轉移工具」中的目前限制而停用版本清除。 如果您偏好保持版本清除已啟用，並在遷移集中執行追加，則必須以`wipe=true`的形式執行擷取。

      1. **包含來自IMS使用者和群組的對應**:選取要包含IMS使用者和群組對應的選項。如需詳細資訊，請參閱[使用者對應工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) 。

      1. **欲包含的路徑**：使用路徑瀏覽器來選取需要移轉的路徑。路徑選擇器通過鍵入或選擇接受輸入。

         >[!IMPORTANT]
         >建立移轉集時會限制下列路徑：
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc` (在 `/etc` CTT中允許選取某些路徑)




1. 填入&#x200B;**建立移轉集**&#x200B;詳細資訊畫面中的所有欄位後，按一下「**儲存**」。

1. 您將在&#x200B;**內容轉移**&#x200B;精靈中檢視移轉集，如下圖所示。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/04-item-selection-and-quick-actions.png)

   所有現有遷移集都顯示在&#x200B;**內容轉移**&#x200B;嚮導中，並顯示其當前狀態和狀態資訊。 您可能會看到以下說明的其中一些圖示。

   * *紅色雲朵*&#x200B;表示您無法完成提取程序。
   * *green cloud*&#x200B;表示您可以完成提取程式。
   * *黃色圖示*&#x200B;表示您並未建立現有移轉集，且該特定移轉集是由相同例項中的其他使用者所建立。

1. 選擇遷移集，然後按一下&#x200B;**屬性**&#x200B;以查看或編輯遷移集屬性。 編輯屬性時，無法變更&#x200B;**移轉集名稱**&#x200B;或&#x200B;**服務URL**。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt06.png)


## 下一步 {#whats-next}

學習如何建立移轉集後，您現在就可以了解「內容轉移工具」中的提取和擷取程式。 在了解這些程式之前，您必須檢閱[處理大型內容存放庫](help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) ，以大幅加快內容轉移活動的提取和擷取階段，以將內容移至AEMas a Cloud Service。
