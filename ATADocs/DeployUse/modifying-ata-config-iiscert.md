---
title: "ATA 구성 변경 - IIS 인증서 | Microsoft ATA"
description: "IIS에서 ATA 센터에 대해 사용하는 인증서를 변경하는 방법에 대해 설명합니다."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e58a0390-57ef-4c68-a987-2e75e5f3d6b3
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: 18d3dfdc2262765d71d82f395273e2972118cbfb


---

# ATA 구성 - IIS 인증서

>[!div class="step-by-step"]
[« ATA 콘솔 IP 주소](modifying-ata-config-consoleip.md)
[도메인 연결 암호 »](modifying-ata-config-dcpassword.md)

## IIS 인증서 변경
콘솔에서 ATA 센터 서비스에 대한 인증서를 선택한 후 변경할 수 있지만 IIS에서 사용되는 인증서는 변경할 수 없습니다.

이 인증서를 변경하려면 다음 절차를 따르세요.

> [!NOTE]
> IIS 인증서를 수정한 후 새 데이터 게이트웨이 설치하기 전에 ATA 게이트웨이 설치 패키지를 다운로드해야 합니다.

ATA 센터에 대해 IIS에서 사용되는 인증서를 수정해야 하는 경우 ATA 센터 서버에서 다음 단계를 수행합니다.

1.  ATA 센터 서버에서 새 인증서를 설치합니다.

2.  IIS(인터넷 정보 서비스) 관리자를 엽니다.

3.  서버 이름을 확장하고 **사이트**를 확장합니다.

4.  Microsoft ATA 콘솔 사이트를 선택하고 **작업** 창에서 **바인딩**을 클릭합니다.

    ![ATA 콘솔 바인딩 작업](media/ATA-console-change-IP-bindings.jpg)

5.  **HTTPS**를 선택하고 **편집**을 클릭합니다.

6.  **SSL 인증서** 아래에서 새 인증서를 선택합니다.

7.  새 ATA 게이트웨이를 설치하기 전에 ATA 게이트웨이 설치 패키지를 다운로드합니다.

>[!div class="step-by-step"]
[« ATA 콘솔 IP 주소](modifying-ata-config-consoleip.md)
[도메인 연결 암호 »](modifying-ata-config-dcpassword.md)

## 참고 항목
- [ATA 콘솔 작업](working-with-ata-console.md)
- [ATA 설치](install-ata.md)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO4-->


