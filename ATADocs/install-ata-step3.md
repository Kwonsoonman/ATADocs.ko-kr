---
title: "Advanced Threat Analytics 설치 - 3단계 | Microsoft 문서"
description: "ATA 설치 3단계에서는 ATA Gateway 설치 패키지를 다운로드합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 10/9/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 7fb024e6-297a-4ad9-b962-481bb75a0ba3
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: f466dddfd2c490d71a57fb27aa833c5ee3a0e5e2
ms.sourcegitcommit: e9f2bfd610b7354ea3fef749275f16819d60c186
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*



# <a name="install-ata---step-3"></a>ATA 설치 - 3단계

>[!div class="step-by-step"]
[« 2단계](install-ata-step2.md)
[4단계 »](install-ata-step4.md)

## <a name="step-3-download-the-ata-gateway-setup-package"></a>3단계. ATA Gateway 설치 패키지 다운로드
도메인 연결 설정을 구성하고 나면 ATA Gateway 설치 패키지를 다운로드할 수 있습니다. ATA 게이트웨이는 전용 서버 또는 도메인 컨트롤러에 설치할 수 있습니다. 도메인 컨트롤러에 설치하는 경우 ATA 경량 게이트웨이로 설치됩니다. ATA 경량 게이트웨이에 대한 자세한 내용은 [ATA 아키텍처](ata-architecture.md)를 참조하세요. 

페이지 맨 위에 있는 단계 목록에서 게이트웨이 설치 다운로드를 클릭하여 게이트웨이 페이지로 이동합니다.

![ATA Gateway 구성 설정](media/ATA_1.7-welcome-download-gateway.PNG)

> [!NOTE] 
> 게이트웨이 구성 화면을 나중에 확인하려면 **설정 아이콘**(오른쪽 위 모서리)을 클릭하고 **구성**을 선택한 다음 **시스템**에서 **게이트웨이**를 클릭합니다.  

1.  **게이트웨이 설치**를 클릭합니다.
  ![ATA 게이트웨이 설치 다운로드](media/download-gateway-setup.png)
2.  패키지를 로컬에 저장합니다.
3.  패키지를 전용 서버 또는 ATA 게이트웨이를 설치 중인 도메인 컨트롤러에 복사합니다. 또는 전용 서버나 도메인 컨트롤러에서 ATA 콘솔을 열어 이 단계를 건너뛸 수 있습니다.

zip 파일에는 다음 항목이 포함되어 있습니다.

-   ATA Gateway 설치 관리자

-   ATA 센터에 연결하는 데 필요한 정보가 포함된 구성 설정 파일


>[!div class="step-by-step"]
[« 2단계](install-ata-step2.md)
[4단계 »](install-ata-step4.md)


## <a name="related-videos"></a>관련 동영상
- [ATA 배포 개요](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [올바른 ATA 게이트웨이 유형 선택](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)

## <a name="see-also"></a>참고 항목
- [ATA POC 배포 가이드](http://aka.ms/atapoc)
- [ATA 크기 조정 도구](http://aka.ms/atasizingtool)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [이벤트 수집 구성](configure-event-collection.md)
- [ATA 필수 구성 요소](ata-prerequisites.md)
