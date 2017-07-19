---
title: "ATA 보고서 작업 | Microsoft Docs"
description: "ATA에서 보고서를 생성하여 네트워크를 모니터링할 수 있는 방법을 설명합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/12/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 38ea49b5-cd5e-43e5-bc39-5071f759633b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 4f29dfcc8b18ff755f6c0dcdaa08eaa807b08072
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/30/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*


# <a name="ata-reports"></a>ATA 보고서

콘솔의 ATA 보고서 섹션에서는 시스템 상태, 사용자 환경에서 검색된 의심스러운 활동 보고서 등 시스템 상태 정보를 제공하는 보고서를 생성할 수 있습니다.

보고서 페이지에 액세스하려면 메뉴 모음에서 보고서 아이콘을 클릭합니다. ![보고서 아이콘](./media/ata-report-icon.png).
사용할 수 있는 보고서는 다음과 같습니다. 
- 요약 보고서: 요약 보고서는 시스템 상태 대시보드를 제공합니다. 세 개의 탭을 볼 수 있습니다. **요약** 탭에는 네트워크에서 검색된 항목의 요약이 표시되고, **시작된 의심스러운 활동** 탭에는 주의해야 하는 의심스러운 활동 목록이 표시되고, **시작된 상태 문제** 탭에는 주의해야 하는 ATA 시스템 상태 문제 목록이 표시됩니다. 나열된 의심스러운 활동은 상태 문제와 마찬가지로 유형별로 분류되어 있습니다. 
- 중요한 그룹 수정: 이 보고서에는 중요한 그룹(예: 관리자)이 수정될 때마다 해당 항목이 표시됩니다.

보고서를 생성하는 방법에는 두 가지가 있으며, 요청 시 또는 보고서가 정기적으로 메일로 전송되도록 예약하는 것입니다.

요청 시 보고서를 생성하려면

1. ATA 콘솔 메뉴 모음에서 메뉴 모음의 보고서 아이콘을 클릭합니다. ![보고서 아이콘](./media/ata-report-icon.png).
2. **요약** 또는 **중요한 그룹 수정**에서 **시작** 및 **종료** 날짜를 설정하고 **다운로드**를 클릭합니다. 
![보고서](./media/reports.png)

예약된 보고서를 설정하려면
 
1. **보고서** 페이지에서 **예약된 보고서 설정**을 클릭하거나 ATA 콘솔 구성 페이지의 알림 및 보고서에서 **예약된 보고서**를 클릭합니다.

   ![보고서 예약](./media/ata-sched-reports.png)

2. **요약** 또는 **중요한 그룹 수정** 옆에 있는 **일정**을 클릭하여 보고서 배달 빈도 및 메일 주소를 설정하고 메일 주소 옆에 있는 더하기 기호를 클릭하여 메일 주소를 추가하고 **저장**을 클릭합니다.

   ![보고서 빈도 및 메일 예약](./media/sched-report1.png)


> [!NOTE]
> 예약된 보고서는 메일을 통해 배달되며, **구성**에서 메일 서버를 이미 구성했으며 알림 및 보고서에서 **메일 서버**를 선택하는 경우에만 보낼 수 있습니다.


## <a name="see-also"></a>참고 항목
- [ATA 필수 구성 요소](ata-prerequisites.md)
- [ATA 용량 계획](ata-capacity-planning.md)
- [이벤트 수집 구성](configure-event-collection.md)
- [Windows 이벤트 전달 구성](configure-event-collection.md#configuring-windows-event-forwarding)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
