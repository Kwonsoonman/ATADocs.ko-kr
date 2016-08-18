---
title: "ATA 설치 - 2단계 | Microsoft ATA"
description: "ATA 설치 2단계에서는 ATA Center 서버에서 도메인 연결 설정을 구성합니다."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: 65ec5c86478e9ded096b899d64eb257257095eaf


---

# ATA 설치 - 2단계

>[!div class="step-by-step"]
[« 1단계](install-ata-step1.md)
[3단계 »](install-ata-step3.md)

## 2단계. ATA 게이트웨이 일반 설정 구성
**일반** 설정 탭의 설정은 ATA 센터에서 관리하는 모든 ATA 게이트웨이에 적용됩니다.

일반 ATA 게이트웨이 설정을 구성하려면 다음을 수행합니다.

1.  ATA 콘솔을 열고 로그인합니다. 지침은 [ATA 콘솔 작업](working-with-ata-console.md)을 참조하세요.

2.  설정 아이콘을 클릭하고 **구성**을 선택합니다.

    ![ATA Gateway 구성 설정](media/ATA-config-icon.JPG)

3.  **일반** 탭의 **ATA 게이트웨이** 아래에 다음 정보를 입력하고 **저장**을 클릭합니다.

    |필드|설명|
    |---------|------------|
    |**사용자 이름**(필수)|읽기 전용 사용자 이름을 입력합니다(예: **user1**).|
    |**암호**(필수)|읽기 전용 사용자에 대한 암호를 입력합니다(예: **Pencil1**). **참고:** 이 암호가 올바른지 확인합니다. 잘못된 암호를 저장하면 ATA Gateway 서버에서 ATA 서비스의 실행이 중지됩니다.|
    |**도메인**(필수)|읽기 전용 사용자에 대한 도메인을 입력합니다(예: **contoso.com**). **참고:** 사용자가 있는 도메인의 전체 FQDN을 입력해야 합니다. 예를 들어 사용자의 계정이 corp.contoso.com 도메인에 있는 경우 contoso.com이 아니라 `corp.contoso.com`을 입력해야 합니다.|
    |모든 ATA 게이트웨이 자동 업데이트 |이 설정을 사용하면 이후 버전 릴리스에서 ATA 센터를 업데이트할 때 모든 ATA 게이트웨이가 자동으로 업데이트됩니다.|

    ![ATA 도메인 연결 설정 이미지](media/ata-domain-connectivity-user.jpg)



>[!div class="step-by-step"]
[« 1단계](install-ata-step1.md)
[3단계 »](install-ata-step3.md)


## 참고 항목

- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [이벤트 수집 구성](configure-event-collection.md)
- [ATA 필수 구성 요소](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=Jul16_HO4-->


