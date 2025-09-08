---
title: 通用編輯器如何發佈內容
description: 了解通用編輯器如何發佈其內容，其與 Sites 控制台的程序有何差異，以及開發自己的應用程式與其搭配運作時需要考量的事項。
feature: Developing
role: Admin, Architect, Developer
exl-id: 60f0bb4a-ee60-4f73-83ae-8568735474ad
source-git-commit: b967a09df7c2e0f5094a6836fcf5311008081dc0
workflow-type: ht
source-wordcount: '564'
ht-degree: 100%

---

# 通用編輯器如何發佈內容 {#publishing}

了解通用編輯器如何發佈其內容，其與 Sites 控制台的程序有何差異，以及開發自己的應用程式與其搭配運作時需要考量的事項。

>[!TIP]
>
>本文內容將詳細介紹適用於開發人員之通用編輯器發佈程序。適用於內容作者之[內容發佈程序請參閱這裡。](/help/sites-cloud/authoring/universal-editor/publishing.md)

## 與 Sites 控制台程序的相似之處 {#similarities}

對於 [AEM 頁面編輯器](/help/sites-cloud/authoring/page-editor/introduction.md)和 [Sites 控制台](/help/sites-cloud/authoring/sites-console/introduction.md)使用者來說，透過通用編輯器發佈內容的程序與您習慣的做法相同：在 AEM 中進行發佈時，內容會從作者服務複寫到發佈服務 (或者複寫到[預覽服務](/help/sites-cloud/authoring/sites-console/previewing-content.md)，若有預覽服務的話而且要視作者在發佈時的選項而定。)

## 差異 {#differences}

透過通用編輯器進行發佈的差異，不在於編輯器本身，而是通用編輯器能夠讓應用程式進行外部託管。

進行外部託管時，網頁應用程式需要確保，若是作者在編輯器中開啟應用程式，要從作者服務載入內容；若是訪客存取應用程式，則要從發佈服務載入內容。

## 偵測應用程式中的服務 {#detecting}

我們可以在應用程式內透過簡單的條件陳述式，偵測應用程式是否在編輯器中開啟來選擇適當的作者或發佈端點，便可以決定應該存取作者服務或發佈服務。

另一種選項是將應用程式部署至不同設定的兩個環境，讓一個環境從作者服務檢索其內容，另一個環境從發佈服務檢索內容。若要讓作者能夠在通用編輯器內開啟已發佈的 URL，可以建立一個小指令碼，將發佈端 URL「轉換」為作者環境中的相等 URL (例如，在網域前面加上 `author` 子網域)，作者便會自動重新導向。

## 摘要 {#summary}

Universal Editor 的目標是不強加任何特定模式，以完全低耦合的方式達成實施的目標，同時仍保持實施簡單和直接的特性。

同樣地，通用編輯器不會要求特定專案用何種方法決定要從哪一個服務傳遞內容。相反地，其支援多種可能性，讓專案能夠自行決定最符合其需求的解決方案。

## 其他資源 {#additional-resources}

若要了解更多關於通用編輯器的技術細節，請參閱這些開發人員文件。

* [通用編輯器簡介](/help/implementing/universal-editor/introduction.md) - 了解通用編輯器如何能在任何實施中編輯任何內容的任何層面，讓您可以提供卓越的體驗、提升內容速度，並提供最尖端的開發人員體驗。
* [AEM 中 Universal Editor 快速入門](/help/implementing/universal-editor/getting-started.md) - 了解如何存取 Universal Editor，以及如何開始檢測您的第一個 AEM 應用程式以使用它。
* [Universal Editor 架構](/help/implementing/universal-editor/architecture.md) - 了解 Universal Editor 的架構，以及資料如何在其服務和階層之間流動。
* [屬性和類型](/help/implementing/universal-editor/attributes-types.md) - 了解 Universal Editor 需要的資料屬性和類型。
* [Universal Editor 驗證](/help/implementing/universal-editor/authentication.md) - 了解 Universal Editor 如何進行驗證。
