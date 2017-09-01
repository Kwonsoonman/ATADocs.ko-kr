---
title: "Advanced Threat Analytics 시스템 상태 및 이벤트 모니터링 | Microsoft Docs"
description: "ATA 상태 관리 센터를 사용하면 ATA 서비스의 작동 상태를 확인하고 문제 가능성에 대한 경고를 받고 이벤트 뷰어에서 시스템 이벤트를 볼 수 있습니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/28/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d6c783b2-46c5-4211-b21a-d6b17f08d03d
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: cdd046eeaca1d8aeb7ea3afa001b34b82cb468b0
ms.sourcegitcommit: 46dd0e695f16a0dd23bbfa140eba15ea6a34d7af
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*


# <a name="working-with-ata-system-health-and-events"></a>ATA 시스템 상태 및 이벤트 작업

## <a name="ata-health-center"></a>ATA 상태 관리 센터
ATA 상태 관리 센터에서는 ATA 서비스의 작동 상태를 확인하고 문제에 대한 경고를 받을 수 있습니다.

## <a name="working-with-the-ata-health-center"></a>ATA 상태 관리 센터 사용
ATA 상태 관리 센터에서는 메뉴 모음의 상태 관리 센터 아이콘 위에 경고(빨간 점)를 표시하여 문제가 있음을 알려 줍니다.

![ATA 상태 관리 센터 빨간 점 도구 모음](media/ATA-Health-Center-Alert-red-dot.png)

### <a name="managing-ata-health"></a>ATA 상태 관리
시스템의 전반적인 상태를 확인하려면 메뉴 모음에서 상태 관리 센터 아이콘을 클릭합니다. ![ATA 상태 관리 센터 아이콘](media/ATA-red-dot.png)

-   경고 모서리에 있는 세 점을 클릭하고 선택하여 시작된 경고를 **마감**, **표시 안 함** 또는 **삭제**로 설정하여 관리할 수 있습니다.

-   **시작됨**: 새로운 의심스러운 활동이 모두 이 목록에 표시됩니다.

-   **마감**: 식별, 조사 및 완화한 의심스러운 활동을 추적하는 데 사용됩니다.

    > [!NOTE]
    > 짧은 기간 내에 동일한 활동이 다시 검색된 경우 ATA는 마감된 활동을 다시 열 수 있습니다.

-   **표시 안 함**: 활동 표시 안 함은 지금은 활동을 무시하고 새 인스턴스가 있을 경우에만 다시 경고를 받는 것을 의미합니다. 이는 비슷한 경고가 있을 경우 ATA에서 다시 열지 않음을 의미합니다. 하지만 경고가 7일 동안 중지된 후 다시 표시되면 다시 경고를 받게 됩니다.

- **삭제**: 경고를 삭제하는 경우 시스템의 데이터베이스에서 삭제되며 복원할 수 없습니다. 삭제를 클릭하면 동일한 유형의 의심스러운 활동을 모두 삭제할 수 있습니다.



![ATA 상태 관리 센터 문제 이미지](media/ATA-Health-Issue.JPG)






## <a name="see-also"></a>참고 항목

- [의심스러운 활동 작업](working-with-suspicious-activities.md)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
