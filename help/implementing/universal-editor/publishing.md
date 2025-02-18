---
title: 通用編輯器如何發佈內容
description: 瞭解Universal Editor如何發佈其內容、它與Sites Console中的程式有何不同，以及開發您自己的應用程式以搭配使用時的注意事項。
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 0ee6689460ac0ecc5c025fb6a940d69a16699c85
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 25%

---


# 通用編輯器如何發佈內容 {#publishing}

瞭解Universal Editor如何發佈其內容、它與Sites Console中的程式有何不同，以及開發您自己的應用程式以搭配使用時的注意事項。

>[!TIP]
>
>本文涵蓋開發人員通用編輯器發佈程式的詳細資訊。 對於內容作者，[此處說明發佈內容的程式。](/help/sites-cloud/authoring/universal-editor/publishing.md)

## 與Sites主控台程式的相似性 {#similarities}

對於[AEM Page Editor](/help/sites-cloud/authoring/page-editor/introduction.md)和[Sites Console的使用者，](/help/sites-cloud/authoring/sites-console/introduction.md)使用Universal Editor發佈內容的程式會依照您慣用的方式運作：在AEM中發佈時，內容會從作者服務復寫到發佈服務(或是[預覽服務](/help/sites-cloud/authoring/sites-console/previewing-content.md) （如果可用，且取決於作者在發佈時選擇的選項）。

## 差異 {#differences}

是什麼讓使用通用編輯器發佈有些不同，與其說在於編輯器本身，不如說在於外部託管應用程式，讓通用編輯器成為可能。

在外部託管時，Web應用程式需確保內容會在作者在編輯器中開啟應用程式時從作者服務載入，並在訪客存取應用程式時從發佈服務載入。

## 在應用程式中偵測服務 {#detecting}

偵測到作者或發佈服務在編輯器中開啟時，可透過應用程式中的簡單條件陳述式選擇適當的作者或發佈端點，以判斷是否應存取作者或發佈服務。

另一個選項是將應用程式部署至兩個設定方式不同的環境，以便其中一個從作者服務擷取其內容，另一個從發佈服務擷取內容。 若要讓作者在通用編輯器中開啟已發佈的URL，可以建立一個小型指令碼，將發佈端URL「轉換」成作者環境中的同等專案（例如，藉由在前`author`個子網域的方式），以便自動重新導向作者。

## 摘要 {#summary}

Universal Editor 的目標是不強加任何特定模式，以完全低耦合的方式達成實施的目標，同時仍保持實施簡單和直接的特性。

同樣地，Universal Editor對於任何特定專案應該如何決定從哪個服務傳送內容也沒有任何要求。 相反地，它提供了多種可能性，並允許專案決定最適合自身需求的解決方案。

## 其他資源 {#additional-resources}

若要深入瞭解通用編輯器的技術細節，請參閱這些開發人員檔案。

* [Universal Editor 簡介](/help/implementing/universal-editor/introduction.md) - 了解 Universal Editor 如何在任意實作中編輯任何方面的內容，以便提供卓越的體驗、提高內容速度並提供最先進的開發人員體驗。
* [AEM 中 Universal Editor 快速入門](/help/implementing/universal-editor/getting-started.md) - 了解如何存取 Universal Editor，以及如何開始檢測您的第一個 AEM 應用程式以使用它。
* [Universal Editor 架構](/help/implementing/universal-editor/architecture.md) - 了解 Universal Editor 的架構，以及資料如何在其服務和階層之間流動。
* [屬性和類型](/help/implementing/universal-editor/attributes-types.md) - 了解 Universal Editor 需要的資料屬性和類型。
* [Universal Editor 驗證](/help/implementing/universal-editor/authentication.md) - 了解 Universal Editor 如何進行驗證。
