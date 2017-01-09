---
title: "ATA 설치 - 2단계 | Microsoft 문서"
description: "ATA 설치 2단계에서는 ATA Center 서버에서 도메인 연결 설정을 구성합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 85e285c5d88e5916e0bf0eb7dd327cb4cb45b4cb
ms.openlocfilehash: 4ca0f9b9c73ddb1432eaf31b75f78af4541e3e29


---

*적용 대상: Advanced Threat Analytics 버전 1.7*



# <a name="install-ata---step-2"></a>ATA 설치 - 2단계

>[!div class="step-by-step"]
[« 1단계](install-ata-step1.md)
[3단계 »](install-ata-step3.md)

## <a name="step-2-provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>2단계. Active Directory 포리스트에 연결할 사용자 이름 및 암호 제공

처음 ATA 콘솔을 열 때 다음 화면이 나타납니다.

![ATA 시작 1단계](media/ATA_1.7-welcome-provide-username.png)

1.  다음 정보를 입력하고 **저장**을 클릭합니다.

    |필드|설명|
    |---------|------------|
    |**사용자 이름**(필수)|읽기 전용 사용자 이름을 입력합니다(예: **ATAuser**).|
    |**암호**(필수)|읽기 전용 사용자에 대한 암호를 입력합니다(예: **Pencil1**).|
    |**도메인**(필수)|읽기 전용 사용자에 대한 도메인을 입력합니다(예: **contoso.com**). **참고:** 사용자가 있는 도메인의 전체 FQDN을 입력해야 합니다. 예를 들어 사용자의 계정이 corp.contoso.com 도메인에 있는 경우 contoso.com이 아니라 `corp.contoso.com`을 입력해야 합니다.|

2. 필요에 따라 **연결 테스트**를 클릭하여 도메인 연결을 테스트하고 제공된 자격 증명으로 액세스할 수 있는지 확인할 수 있습니다. 이 작업은 ATA 센터가 도메인에 연결되어 있는 경우에만 수행할 수 있습니다.   

    저장되고 나면 콘솔에서 시작 메시지가 다음과 같이 변경됩니다. ![ATA 시작 1단계가 완료됨](media/ATA_1.7-welcome-provide-username-finished.png)

3. 콘솔에서 **Download Gateway setup and install the first Gateway**(게이트웨이 설치 프로그램을 다운로드하여 첫 번째 게이트웨이 설치)를 클릭하여 계속합니다.


>[!div class="step-by-step"]
[« 1단계](install-ata-step1.md)
[3단계 »](install-ata-step3.md)


## <a name="see-also"></a>참고 항목

- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [이벤트 수집 구성](configure-event-collection.md)
- [ATA 필수 구성 요소](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=Nov16_HO2-->


