---
title: 組織數位資產以使用Dynamic Media影像描述檔或視訊描述檔的最佳實務
description: 「命名、組織和管理Dynamic Media影像檔案和視訊資產檔案的秘訣與最佳實務。」
contentOwner: Rick Brough
feature: Asset Management,Image Profiles,Video Profiles
topic: Business Practitioner
role: Administrator,Business Practitioner
exl-id: 82ab5432-088c-4442-a9db-9f4e0184febf
translation-type: tm+mt
source-git-commit: 6b232ab512a6faaf075faa55c238dfb10c00b100
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# 組織數位資產以使用影像描述檔或視訊描述檔的最佳範例{#best-practices-for-organizing-your-digital-assets-for-using-profiles}

使用「Dynamic Media影像描述檔」或「視訊描述檔」的重要概念，是指派給資料夾。 描述檔中是影像或視訊的設定。 這些設定會處理資料夾的內容及其任何子檔案夾。 因此，命名檔案和檔案夾、排列子檔案夾和處理這些檔案夾中檔案的方式，會影響描述檔處理這些資產的方式。

透過使用一致且適當的檔案和資料夾命名策略，以及良好的中繼資料實務，您可以充份運用您的數位資產收集，並確保正確的檔案由正確的描述檔處理。

請參閱[關於Dynamic Media影像配置檔案和視頻配置檔案](about-image-video-profiles.md)。

以下是組織數位資產檔案的最佳實務秘訣。

* 根據您新增的中繼資料來組織檔案，而不是根據檔案所在的資料夾。 您可以新增中繼資料設定檔來完成此作業。

   * 請參閱[中繼資料描述檔](/help/assets/metadata-profiles.md)。
   * 請參閱[數位資產管理的中繼資料](/help/assets/manage-metadata.md)。

* 通常，您的數位資產收集量會不斷增加。 因此，您必須先將所有上傳資產的中繼資料使用、檔案夾結構和檔案命名正規化，這一點在稍早之前就很重要。 標準化這些功能可確保隨著數位資產庫的擴充，您可以更精確地將處理設定檔套用至資料夾，並保有一致性。
* 僅使用資料夾，為您的數位資產建立一致的儲存結構。 例如，可協助您調整要指派哪些描述檔的檔案夾結構可包含下列內容：

   * **開發資料夾** -包含您目前正在處理的數位資產。
   * **用戶端資料夾** -包含以用戶端或專案名稱為基礎的數位資產。
   * **主要來源資料夾** -包含原始的來源數位資產。
   * **轉譯資料夾** -包含原始來源數位資產的轉譯和副本。
   * **檔案大小檔案夾** -包含以小型、中型或大型檔案大小為基礎的數位資產。
   * **測試資料夾** -包含可立即在您的網站上發佈的數位資產。
   * **Mime類型資料夾** -包含MIME類型專屬的數位資產，例如影像、檔案和多媒體。
   * **封存資料夾** -包含淘汰的數位資產。
   * **日期型資料夾** -包含以建立日期或上次修改日期為基礎的數位資產。

* 建立不太可能更改的資料夾目錄，以便所有分配的配置檔案不中斷。
* 假設資產已發佈，則您會使用Adobe Experience Manager將資產移至另一個檔案夾，並從其新位置重新發佈。 原始發佈的資產位置仍可供使用，以及新重新發佈的資產。 但是，原始發佈的資產「遺失」至Experience Manager，無法解除發佈。 因此，在將資產移至其他資料夾之前，請先解除發佈資產，這是最佳作法。
