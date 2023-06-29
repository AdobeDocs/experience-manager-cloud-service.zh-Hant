---
title: 使用內容轉換器
description: 使用內容轉換器
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 2%

---

# 使用內容轉換器 {#using-ct}

## 使用內容轉換器的重要考量 {#imp-considerations-ct}

請依照以下章節瞭解使用內容轉換器(CT)的重要考量事項：

* 若要使用內容轉換器，您必須先在Adobe Experience Manager (AEM)環境中執行Best Practices Analyzer。
* 雖然您可以在生產環境中執行內容轉換器，但建議您在複製的生產環境中執行內容轉換器。 更重要的是，您需要確保BPA和CT在相同的環境中執行。
* 您必須是要執行內容轉換器的環境管理員。
* 任何可變更來源內容的操作（移動/移除/重新命名）預設都會在下方建立來源路徑的備份套件 `/etc/packages/content-transformation` 轉換之前。 雖然每個操作對話方塊都有一個選項可停用/啟用備份套件的建立，但嚴格建議您一律選取啟用套件的建立。
* CT中的每個頁面都設定為最多列出50個發現，因此一次最多可以轉換50個發現。 這麼做是為了在UI上提供及時回應。

## 可用性 {#availability-ct}

內容轉換器隨附於 [內容轉移工具](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md) 可從軟體發佈入口網站下載為zip檔。 您可以透過封裝管理程式，在來源AEM執行個體上安裝封裝。

>[!NOTE]
>內容轉換器可搭配「內容轉移工具v2.0.20」或更新版本使用。

## 開啟內容轉換器 {#opening-ct}

1. 以管理員身分登入來源AEM執行個體，然後前往開始頁面：https://host:port/aem/start.html。
1. 導覽至「工具>作業>內容移轉」

   ![影像](/help/journey-migration/content-transformer/assets/ct-1.png)

   >[!NOTE]
   > 請確認您之前已執行BPA報表，並使用URL http://host:port/apps/best-practices-analyzer/content/BestPracticesReport.html進行驗證

1. 按一下標題為的卡片 **BPA報告的內容轉換器**

   ![影像](/help/journey-migration/content-transformer/assets/ct-2.png)

   以下範例說明BPA報告建立成功以及發現內容相關問題後，內容轉換器概觀頁面的外觀。

   BPA報告的剩餘到期時間會顯示在側邊欄中。 建議使用最新的BPA報告執行內容轉換器，以避免遺漏任何與內容相關的發現。

   ![影像](/help/journey-migration/content-transformer/assets/ct-3.png)

1. 您可以根據以下條件篩選問題： `Pattern Code`， `Subtype`， `Importance`、和 `Source`.

   ![影像](/help/journey-migration/content-transformer/assets/ct-4.png)

1. 您可以選取所有或特定問題，然後採取移動、移除和重新命名等動作來解決這些問題。 也可以使用新增自訂路徑 **新增路徑** 按鈕。

   >[!NOTE]
   > 使用移動操作時，建議將所有路徑僅移動至一個資料夾(例如 `/etc/packages/content-transformation/paths`)，所以安裝備份套件以將執行個體恢復到原始狀態時，資料夾(`/etc/packages/content-transformation/paths`)可使用移除操作來刪除，以減少存放庫大小。

   ![影像](/help/journey-migration/content-transformer/assets/ct-5.png)
   ![影像](/help/journey-migration/content-transformer/assets/ct-6.png)

   >[!NOTE]
   > 任何可變更來源內容的操作(`move`/`remove`/`rename`)預設會建立「 」底下來源路徑的備份套件 `/etc/packages/content-transformation` 轉換之前。 雖然每個操作對話方塊都有一個選項可停用/啟用備份套件的建立，但嚴格建議您一律選取啟用套件的建立。

1. 以下顯示為路徑移動作業而建立的備份封裝範例，按一下安裝以恢復來源路徑。 請注意，安裝只會讓來源路徑回到其原始位置，而不會刪除轉換期間移動它們的路徑。 若要刪除移動位置中的路徑，請按一下 **新增路徑** 按鈕以新增位置(例如 `/etc/packages/content-transformation/paths`)，選取位置並按一下 **移除**.

   >[!CAUTION]
   > 不要刪除 `/etc/packages/content-transformation` 因為這是備份套件的存放位置。 只有在您確定不再需要這些套件時，才能刪除此位置來減少存放庫大小。

   ![影像](/help/journey-migration/content-transformer/assets/ct-7.png)
   ![影像](/help/journey-migration/content-transformer/assets/ct-8.png)
