---
# required metadata

title: ATA 설치 - 2단계 | Microsoft Advanced Threat Analytics
description: ATA 설치 2단계에서는 ATA Center 서버에서 도메인 연결 설정을 구성합니다.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 설치 - 2단계

>[!div class="step-by-step"]
[« 1단계](install-ata-step1.md)
[3단계 »](install-ata-step3.md)

## 2단계. ATA Gateway 도메인 연결 설정 구성
도메인 연결 설정 섹션의 설정은 ATA Center에서 관리되는 모든 ATA Gateway에 적용됩니다.

도메인 연결 설정을 구성하려면 ATA Center 서버에서 다음을 수행합니다.

1.  ATA 콘솔을 열고 로그인합니다. 지침은 [ATA 콘솔 작업](/advanced-threat-analytics/understand/working-with-ata-console)을 참조하세요.

2.  ATA Center를 설치한 후 ATA 콘솔에 처음 로그인하면 ATA Gateway 구성 페이지로 자동으로 이동합니다. 나중에 설정을 수정해야 하는 경우 설정 아이콘을 클릭하고 **구성**을 선택합니다.

    ![ATA Gateway 구성 설정](media/ATA-config-icon.JPG)

3.  **게이트웨이** 페이지에서 **도메인 연결 설정**을 클릭하고 다음 정보를 입력한 후 **저장**을 클릭합니다.

    |필드|설명|
    |---------|------------|
    |**사용자 이름**(필수)|읽기 전용 사용자 이름을 입력합니다(예: **user1**).|
    |**암호**(필수)|읽기 전용 사용자에 대한 암호를 입력합니다(예: **Pencil1**). **참고:** 이 암호가 올바른지 확인합니다. 잘못된 암호를 저장하면 ATA Gateway 서버에서 ATA 서비스의 실행이 중지됩니다.|
    |**도메인**(필수)|읽기 전용 사용자에 대한 도메인을 입력합니다(예: **contoso.com**). **참고:** 사용자가 있는 도메인의 전체 FQDN을 입력해야 합니다. 예를 들어 사용자의 계정이 corp.contoso.com 도메인에 있는 경우 contoso.com이 아니라 `corp.contoso.com`을 입력해야 합니다.|
    ![ATA 도메인 연결 설정 이미지](media/ATA-Domain-Connectivity-User.JPG)


>[!div class="step-by-step"]
[« 1단계](install-ata-step1.md)
[3단계 »](install-ata-step3.md)


## 참고 항목

- [지원이 필요한 경우 포럼을 확인하세요.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [이벤트 수집 구성](/advanced-threat-analytics/plandesign/configure-event-collection)
- [ATA 필수 구성 요소](/advanced-threat-analytics/plandesign/ata-prerequisites)


<!--HONumber=Apr16_HO2-->


