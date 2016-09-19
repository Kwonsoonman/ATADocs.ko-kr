---
title: "ATA 구성 변경 - 도메인 연결 암호 | Microsoft ATA"
description: "ATA 게이트웨이의 도메인 연결 암호를 변경하는 방법에 대해 설명합니다."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 050f1ef0b39d69b64ede53243a7fa2d33d0e4813
ms.openlocfilehash: 7cee457a8959526b25a68c50efea2976bafbef75


---

*적용 대상: Advanced Threat Analytics 버전 1.7*



# ATA 구성 변경 - 도메인 연결 암호

>[!div class="step-by-step"]
[« ATA 웹 콘솔 URL](modifying-ata-config-consoleurl.md)


## 도메인 연결 암호 변경
도메인 연결 암호를 수정하는 경우 입력한 암호가 올바른지 확인합니다. 올바르지 않으면 ATA 게이트웨이 서비스가 ATA 게이트웨이에서 더 이상 실행되지 않습니다.

이 문제가 발생한 것으로 의심되면 ATA 게이트웨이의 Microsoft.Tri.Gateway Errors.log 파일에서 다음을 확인합니다.
`The supplied credential is invalid.`

이 문제를 해결하려면 다음 절차에 따라 ATA 센터에서 도메인 연결 암호를 업데이트합니다.

1.  ATA 센터에서 ATA 콘솔을 엽니다.

2.  도구 모음에서 설정 옵션을 선택하고 **구성**을 선택합니다.

    ![ATA 구성 설정 아이콘](media/ATA-config-icon.JPG)

3.  **디렉터리 서비스**를 선택합니다.

    ![ATAA 게이트웨이 암호 변경 이미지](media/ATA-GW-change-DC-password.png)

4.  **암호**에서 암호를 변경합니다.

    ATA 센터에서 도메인에 연결할 수 있는 경우 **연결 테스트** 단추를 사용하여 자격 증명의 유효성을 검사합니다.

5.  **저장**을 클릭합니다.

6.  암호를 변경한 후 ATA 게이트웨이 서비스가 ATA 게이트웨이 서버에서 실행되 고 있는지를 수동으로 확인합니다.

>[!div class="step-by-step"]
[« ATA 웹 콘솔 URL](modifying-ata-config-consoleurl.md)

## 참고 항목
- [ATA 콘솔 작업](working-with-ata-console.md)
- [ATA 설치](install-ata.md)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Aug16_HO5-->


