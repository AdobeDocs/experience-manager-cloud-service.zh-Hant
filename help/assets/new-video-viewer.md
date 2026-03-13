---
title: 新視訊檢視器
description: Dynamic Media的全新視訊檢視器提供更優異的視訊播放體驗
role: User
exl-id: null
source-git-commit: 0a9d4ef72a6bc5037f87c22915bc75312bbd52d7
workflow-type: tm+mt
source-wordcount: '1443'
ht-degree: 2%

---


# Dynamic Media中的新視訊檢視器 {#new-video-viewer-dynamic-media}

適用於Dynamic Media的全新視訊檢視器提供Adobe Experience Manager (AEM)現代化視訊播放體驗。 它可在編寫、預覽和Sites環境中提供一致且可擴充的檢視體驗，同時繼續搭配現有Dynamic Media工作流程使用。

Dynamic Media中的現有視訊檢視器支援核心播放需求，但針對現代分析和整合情境提供有限的擴充性和事件層級整合

新的視訊檢視器可透過以下方式解決這些限制：

* 提供更一致的播放體驗
* 允許明確的檢視器選擇
* 發出結構化播放事件以供程式化使用
* 支援與外部分析和外部系統的整合

此檢視器可作為其他選項使用，若有支援，則需要明確選取檢視器。 它不會自動取代現有的視訊檢視器。

新的視訊檢視器適用於需要增強且可擴充視訊體驗，又不會中斷現有實作的組織。

> **附註**
>
> 新的視訊檢視器是可用性受限的功能。 您可以建立[支援票證](https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html)來啟用它。


## 新視訊檢視器的運作方式 {#how-it-works}

新視訊檢視器的運作方式如下：

1. 視訊資產會擷取至與Dynamic Media同步的資料夾。
2. 可使用&#x200B;**影片（新）**，從資產詳細資訊頁面預覽影片。
3. 編寫Sites頁面時，可以在&#x200B;**Dynamic Media**&#x200B;元件中選取新的視訊檢視器。
4. 在播放期間，檢視器會向父視窗傳送結構化事件。
5. 選用的檢視器修飾元可用於控制播放行為。

## 與現有Video Viewer的主要差異 {#key-differences}

| 區域 | 說明 |
|------|-------------|
| 檢視器可用性 | 顯示為名為&#x200B;**視訊（新）**&#x200B;的新選項 |
| 檢視器選擇 | 必須明確選取 |
| 擴展性 | 發出結構化播放事件 |
| 整合 | 持續使用現有的Dynamic Media工作流程 |

## 先決條件 {#prerequisites}

在使用新的Video Viewer之前，請確定符合下列必要條件：

| 需求 | 說明 |
|------------|-------------|
| Dynamic Media同步 | 資產資料夾必須與Dynamic Media同步。 |
| 視訊設定檔 | 視訊設定檔必須套用至資料夾。 |
| 視訊資產 | 視訊必須擷取至資料夾。 |

新視訊檢視器從&#x200B;**AEM as a Cloud Service 2025.7.0**&#x200B;版開始提供。

若要啟用或停用新視訊檢視器，請聯絡Adobe客戶服務。

## 預覽新視訊檢視器 {#preview}

執行以下步驟，從資產詳細資訊頁面預覽新視訊檢視器：

1. 導覽至&#x200B;**Assets** > **檔案**，然後開啟包含視訊資產的資料夾。
2. 按一下視訊資產，開啟資產詳細資訊頁面。
3. 在左側面板中，按一下&#x200B;**檢視器**。
4. 在&#x200B;**檢視器**&#x200B;面板中，選取&#x200B;**視訊（新增）**。
5. 按一下&#x200B;**URL**以複製預覽連結。
   ![複製URL](assets/Copy-url1.jpg)

## 在網站中使用新的視訊檢視器 {#use-in-sites}

新視訊檢視器可透過AEM Sites中的現有&#x200B;**Dynamic Media**&#x200B;元件使用。

### 新增Dynamic Media元件

執行以下步驟，使用動態媒體元件新增視訊：

1. 在&#x200B;**網站編輯器**&#x200B;中開啟頁面。
2. 將&#x200B;**Dynamic Media**&#x200B;元件拖曳至頁面上的必要位置。
3. 選取頁面上的&#x200B;**Dynamic Media**&#x200B;元件。
4. 按一下元件以開啟資產選擇器。
5. 選取視訊資產。

![拖曳動態媒體元件](assets/drag-component.jpeg)

### 設定檢視器

執行以下步驟來設定檢視器預設集：

1. 選取頁面上的&#x200B;**Dynamic Media**&#x200B;元件。
2. 按一下元件工具列中的&#x200B;**設定**。
   ![開啟Dynamic Media設定](assets/configure-asset.png)

3. 在&#x200B;**動態媒體設定對話方塊**&#x200B;中，從&#x200B;**檢視器預設集**&#x200B;下拉式清單中選取&#x200B;**視訊（新增）**。
   ![選取視訊（新）檢視器預設集](assets/viewer-preset.jpeg)

4. 在&#x200B;**檢視器修飾元**&#x200B;欄位中輸入任何必要的修飾元（例如，`autoplay=true&muted=true`）。
   ![檢視器修飾元](assets/additional-modifiers.jpeg)

5. 儲存變更。

視訊會使用新的視訊檢視器在頁面上載入。

> **注意：**&#x200B;新的視訊檢視器不會自動取代現有的視訊。 使用動態媒體元件時，使用者必須在&#x200B;**檢視器預設集**&#x200B;中手動選取&#x200B;**視訊（新）**，或更新直接URL以視需要指向新視訊檢視器。

### 使用直接URL移轉視訊

如果視訊是透過直接URL存取，而非透過動態媒體元件存取，您可以更新URL以將其切換為新的視訊檢視器。 例如：`https://s7d1.scene7.com/dmviewers/html5/VideoViewer.html?asset=<video-asset>`

## 檢視器修飾元 {#viewer-modifiers}

檢視器修飾元可讓您控制資產載入、播放行為、串流格式選擇和檢視器簡報。

| 修飾元 | 說明 |
|--------|-------------|
| `asset` | 指定視訊或自我調整視訊集的資產ID。 |
| `posterimage` | 指定播放開始前顯示的影像。 |
| `serverurl` | 指定「影像伺服」根路徑。 |
| `contenturl` | 指定內容根路徑。 |
| `videoserverurl` | 指定視訊伺服器根路徑。 |
| `sources.dash` | 指定播放的DASH資訊清單URL。 |
| `sources.hls` | 指定要播放的HLS資訊清單URL。 |
| `autoplay=true` | 載入視訊時自動開始播放。 |
| `controls=true/false` | 顯示或隱藏視訊播放控制項。 |
| `loop=true` | 在視訊結束後自動重新啟動播放。 |
| `muted=true` | 以靜音狀態開始播放。 |
| `playbackrates` | 指定可用的播放速度選項。 |
| `playback` | 指定串流格式（自動、hls、破折號或漸進式）。 |
| `progressivebitrate` | 指定漸進式播放的位元速率。 |
| `initialbitrate` | 指定最適化串流的初始位元速率。 |
| `isletterboxed=true/false` | 控制視訊是文字框還是延伸。 |
| `customcss` | 指定檢視器樣式的自訂CSS檔案。 |
| `transition` | 指定檢視器控制項的顯示或隱藏轉變行為。 |

修飾元在&#x200B;**檢視器修飾元**&#x200B;欄位中指定為查詢引數。

## 支援的事件 {#supported-events}

新的視訊檢視器在播放期間會發出下列事件：

| 事件型別 | 說明 |
|-----------|-------------|
| play | 視訊開始播放 |
| pause | 視訊已暫停 |
| 搜尋 | 使用者在視訊中搜尋 |
| 載入 | 視訊已載入 |
| 關閉 | 播放器已關閉 |
| 中繼資料 | 中繼資料，例如持續時間 |
| 里程碑 | 已達播放里程碑 |
| current_time | 定期播放位置 |
| 全螢幕 | 輸入全熒幕 |
| un_fullscreen | 退出全熒幕 |

## 處理父視窗中的事件 {#handling-events}

新的視訊檢視器會在視訊互動期間，將與播放相關的訊息傳送至上層頁面。

若要處理這些事件，父應用程式必須先接聽瀏覽器訊息事件並驗證訊息來源，才能處理資料。

事件裝載包含事件型別、播放狀態、目前播放時間和其他中繼資料等資訊。 這些事件可用於支援分析追蹤、自訂互動或與外部系統的整合

Adobe建議驗證訊息來源，以確保系統只會處理來自受信任Dynamic Media網域的事件。

## 新視訊檢視器的視訊參與報告 {#video-engagement-report}

「視訊參與報表」提供在Dynamic Media中使用新視訊檢視器播放之視訊的分析量度。 報表會提供指定月份的彙總效能資料，並支援每月報表。

報表是根據要求而產生。 若要請求報告，請建立[支援票證](https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html)並提供下列詳細資料：

* 報告月份 — 指定需要報告的月份（例如，2026年1月）。
* 傳送電子郵件地址 — 傳送報表的群組（建議）或個人的電子郵件地址

此報表提供每個視訊的參與量度，包括檢視次數、曝光數、觀看時間、完成率和參與分數。

### 報表格式

* 報表會以CSV格式傳送。
* 每一列代表單一視訊。
* 系統會彙總所選報告期間的量度。
* 報表中會排除已刪除的資產。
* 支援`tenant_name`的篩選。

### 報告欄位

視訊參與報表包含下列欄位：

| 欄位 | 說明 | 計算 |
|-------|------------|-------------|
| `video_id` | 唯一的視訊識別碼。 | 不適用 |
| `video_name` | 視訊資產的名稱。 | 不適用 |
| `video_created_date` | 建立視訊的日期。 | 不適用 |
| `duration_in_seconds` | 視訊的持續時間（秒數）。 | 不適用 |
| `video_views` | 選定報告期間內的視訊播放事件總數。 | 不適用 |
| `video_impressions` | 視訊載入的總次數。 | 不適用 |
| `video_watched_seconds` | 在所有播放事件中觀看的總秒數。 | 所有播放事件觀看的秒數總和 |
| `play_rate` | 視訊播放相對於視訊載入的百分比。 | (`video_views` ÷ `video_impressions`) × 100 |
| `avg_time_watched_in_seconds` | 每次檢視觀看的平均秒數。 | `video_watched_seconds` ÷ `video_views` |
| `avg_completion_rate` | 達到完整視訊完成的檢視百分比。 | （已完成檢視÷`video_views`） × 100 |
| `engagement_score` | 所有播放事件的平均觀看百分比。 | （所有工作階段中檢視的視訊時間軸÷總百分比`video_views`） |
| `tenant_name` | 與資料相關聯之公司或租使用者的識別碼。 | 不適用 |

## 常見問題 {#faq-video-engagement}

+++如果視訊設為自動播放，會自動計算為檢視，還是隻計入使用者觀看了持續時間最短的一段時間？

自動播放會計為視訊檢視。 自動起始的播放會記錄為檢視。

+++

+++如果使用者只觀看部分影片（例如，10秒影片的前2秒和後2秒），是否會計為已完成的檢視？

當播放達到視訊時間軸結尾時，即使已略過視訊的某些部分，檢視仍會計為已完成。

+++

+++如果使用者向後擦除並重新觀看視訊部分，它是否會增加video_views計數、engagement_score或兩者？

重新觀看視訊的部分不會增加video_views計數。 其他播放會貢獻至engagement_score。

+++

+++如果同一使用者多次觀看相同影片而不重新載入頁面，如何計算video_views和engagement_score？

重複播放而不重新載入頁面不會增加video_views計數。 其他播放會貢獻至engagement_score。

+++

+++暫停和恢復視訊是否會影響參與追蹤或完成率的計算？

暫停和恢復播放不會影響參與追蹤或完成率計算。

+++
