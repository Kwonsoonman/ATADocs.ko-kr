---
title: "로그를 사용하여 Advanced Threat Analytics 문제 해결 | Microsoft 문서"
description: "ATA 로그를 사용하여 문제를 해결하는 방법을 설명합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 5a65285c-d1de-4025-9bb4-ef9c20b13cfa
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 125376b1e3530481a3b9f62c4661dd10dce13f22
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*



# <a name="troubleshooting-ata-center-service-startup"></a>ATA 센터 서비스 시작 문제 해결

ATA 센터가 시작되지 않는 경우 다음과 같은 문제 해결 절차를 수행합니다.

1.  다음 Windows PowerShell 명령을 실행합니다. `Get-Service Pla | Select Status` 명령을 실행하여 성능 카운터 서비스가 실행되고 있는지 확인합니다. 실행되지 않는다면 플랫폼 문제이며, 이 서비스가 다시 실행되도록 해야 합니다.
2.  실행되고 있으면 다시 시작하여 문제가 해결되는지 확인합니다. `Restart-Service Pla`
3.  새 데이터 수집기를 수동으로 만들려고 시도합니다(어떤 수집기여도 상관없으며, 예를 들어 컴퓨터 CPU만 수집해도 됨).
시작할 수 있다면 플랫폼이 정상일 수 있습니다. 그렇지 않으면 여전히 플랫폼 문제입니다.

4.  관리자 권한의 프롬프트에서 다음 명령을 실행하여 ATA 데이터 수집기를 수동으로 다시 작성합니다.

        sc stop ATACenter
        logman stop "Microsoft ATA Center"
        logman export "Microsoft ATA Center" -xml c:\center.xml
        logman delete "Microsoft ATA Center"
        logman import "Microsoft ATA Center" -xml c:\center.xml
        logman start "Microsoft ATA Center"
        sc start ATACenter



## <a name="see-also"></a>참고 항목
- [ATA 필수 구성 요소](ata-prerequisites.md)
- [ATA 용량 계획](ata-capacity-planning.md)
- [이벤트 수집 구성](configure-event-collection.md)
- [Windows 이벤트 전달 구성](configure-event-collection.md#configuring-windows-event-forwarding)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
