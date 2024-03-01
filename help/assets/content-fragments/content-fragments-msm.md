---
title: 使用MSM和即時副本重複使用內容片段
description: 瞭解如何使用MSM的即時副本功能，以便在多個位置使用相同或類似的內容片段內容，同時與來源內容同步。
source-git-commit: 3ce1a982055c2f9c900edbd88e079deb6d3a036a
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 10%

---

# 使用MSM重複使用內容片段 {#reuse-content-fragments-using-msm}

多站點管理員(MSM)和即時副本功能可讓您在多個位置使用相同的內容，同時與來源內容同步。

* 使用MSM即時副本，您可以：
   * 建立內容一次，然後
   * 在相同或其他網站或應用程式的其他區域重複使用此內容。
* 然後，MSM 維護您的來源內容與其 Live Copy 之間的即時關係，以便：
   * 當您變更來源內容時，來源和即時副本會同步。
   * 您可以透過斷開各個子頁面和/或元件的即時關係，僅對 Live Copy 的內容進行調整。

如需MSM概念的詳細概觀，請參閱 [重複使用內容：多網站管理員和即時副本](/help/sites-cloud/administering/msm/overview.md).

>[!NOTE]
>
>[多站點管理員(MSM)](/help/sites-cloud/administering/msm/overview.md) Adobe Experience Manager中的功能可讓使用者重複使用製作一次並在多個網站位置重複使用的內容。

使用MSM處理內容片段您可以：

* 建立內容片段一次，然後製作（連結）這些片段的復本，以便在網站或應用程式的其他區域重複使用。
* 更新來源復本一次，然後將變更推送至（即時）復本，保持多個復本同步。
* 暫時或永久地暫停父片段與子片段之間的連結（完全或針對其變數或欄位），以進行本機變更。

內容片段的MSM結合內容片段編輯器中的功能，可讓您中斷並恢復欄位層級的繼承。

>[!CAUTION]
>
>內容片段的MSM僅適用於透過使用內容片段時 **資產** 主控台。
>
>MSM功能為 *非* 使用時可用 **內容片段** 主控台。

## 操作說明 {#how-to}

請參閱下列檔案，以取得有關使用MSM處理內容片段（也適用於資產）的詳細資訊：

* 使用方式 [內容片段（和資產）的MSM](/help/assets/reuse-assets-using-msm.md)

* [建立即時副本](/help/assets/reuse-assets-using-msm.md)

  >[!CAUTION]
  >
  >如果您想使用MSM建立內容片段副本)，則任何 **獨特** 應從個別專案中使用的任何資料型別中移除限制 [內容片段模型](/help/assets/content-fragments/content-fragments-models.md).

* [檢視來源和即時副本的屬性和狀態](/help/assets/reuse-assets-using-msm.md#properties)
* [將修改從來源傳播到即時副本](/help/assets/reuse-assets-using-msm.md#rollout-sync)
* 取消並恢復下列專案的繼承：
   * 中的欄位和變數 [內容片段編輯器](/help/assets/content-fragments/content-fragments-variations.md#inheritance)
   * [相關資產的中繼資料](/help/assets/content-fragments/content-fragments-variations.md#canceling-reenabling-inheritance-individual-items)
* [暫停並繼續關係](/help/assets/reuse-assets-using-msm.md#suspend-resume)
* [移除即時關係](/help/assets/reuse-assets-using-msm.md#detach)
* [比較內容片段（和資產）的MSM與網站的MSM](/help/assets/reuse-assets-using-msm.md#comparison)

## 限制 {#limitations}

* 內容片段不存在修改時觸發程式及相關轉出設定。