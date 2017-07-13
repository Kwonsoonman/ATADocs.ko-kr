---
title: "Advanced Threat Analytics에서 의심스러운 활동 작업 | Microsoft 문서"
description: "ATA에서 식별된 의심스러운 활동을 검토하는 방법을 설명합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 44d7c899-816c-4f7f-91d3-84a09d291a24
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1ff15a323f461cf8436e1ff7e15738a49bf3973c
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/30/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*



# 의심스러운 활동 작업
<a id="working-with-suspicious-activities" class="xliff"></a>
이 항목에서는 Advanced Threat Analytics를 사용하는 방법에 대한 기본 사항을 설명합니다.

## 공격 타임라인에서 의심스러운 활동 검토
<a id="review-suspicious-activities-on-the-attack-time-line" class="xliff"></a>
ATA 콘솔에 로그인하면 **의심스러운 활동 타임라인**이 자동으로 열립니다. 의심스러운 활동은 최신 활동이 타임라인의 맨 위에 오도록 시간 순으로 나열됩니다.
각 의심스러운 활동에는 다음과 같은 정보가 있습니다.

-   관련된 엔터티(사용자, 컴퓨터, 서버, 도메인 컨트롤러 및 리소스 포함)

-   의심스러운 활동의 시간 및 기간

-   의심스러운 활동의 심각도(높음, 중간 또는 낮음)

-   상태: 시작됨, 마감 또는 표시 안 함

-   기능:

    -   메일을 통해 조직의 다른 사람과 의심스러운 활동을 공유합니다.

    -   의심스러운 활동을 Excel로 내보냅니다.

    -   의심스러운 활동에 메모를 추가합니다.

    -   의심스러운 활동에 대한 입력을 제공합니다.

-   의심스러운 활동에 대응하는 방법에 대한 권장 사항을 제공합니다.

> [!NOTE]
> -   사용자 또는 컴퓨터 위로 마우스를 가져가면 엔터티에 대한 추가 정보를 제공하고 엔터티에 연결된 의심스러운 활동 수를 포함하는 엔터티 최소 프로필이 표시됩니다.
> -   엔터티를 클릭하면 사용자 또는 컴퓨터의 엔터티 프로필로 이동합니다.

![ATA 의심스러운 활동 타임라인 이미지](media/ATA-Suspicious-Activity-Timeline.JPG)

## 의심스러운 활동 목록 필터링
<a id="filter-suspicious-activities-list" class="xliff"></a>
의심스러운 활동 목록을 필터링하려면

1.  화면의 왼쪽의 **필터링 기준** 창에서 **모두**, **미해결**, **해결됨** 또는 **해제됨**을 선택합니다.

2.  목록을 추가로 필터링하려면 **높음**, **중간** 또는 **낮음**을 선택합니다.

**의심스러운 활동 심각도**

-   **낮음**

    악의적인 사용자 또는 소프트웨어가 조직 데이터에 대한 액세스 권한을 얻도록 설계된 공격으로 이어질 수 있는 의심스러운 활동을 나타냅니다.

-   **중간**

    특정 ID를 ID 도용 또는 권한 상승을 초래하는 보다 심각한 공격의 위험에 노출시킬 수 있는 의심스러운 활동을 나타냅니다.

-   **높음**

    ID 도용, 권한 상승 또는 기타 강력한 공격으로 이어질 수 있는 의심스러운 활동을 나타냅니다.




## 의심스러운 활동 해결
<a id="remediating-suspicious-activities" class="xliff"></a>
의심스러운 활동의 현재 상태를 클릭하고 **시작됨**, **표시 안 함**, **마감** 또는 **삭제됨**을 선택하여 의심스러운 활동의 상태를 변경할 수 있습니다.
이렇게 하려면 특정 의심스러운 활동의 오른쪽 위에 있는 세 점을 클릭하여 사용 가능한 작업 목록을 표시합니다.

![의심스러운 활동에 대한 ATA 작업](./media/sa-actions.png)

**의심스러운 활동 상태**

-   **시작됨**: 새로운 의심스러운 활동이 모두 이 목록에 표시됩니다.

-   **마감**: 식별, 조사 및 완화한 의심스러운 활동을 추적하는 데 사용됩니다.

    > [!NOTE]
    > 짧은 기간 내에 동일한 활동이 다시 검색된 경우 ATA는 해결된 활동을 다시 열 수 있습니다.

-   **표시 안 함**: 활동 표시 안 함은 지금은 활동을 무시하고 새 인스턴스가 있을 경우에만 다시 경고를 받는 것을 의미합니다. 이는 비슷한 경고가 있을 경우 ATA에서 다시 열지 않음을 의미합니다. 하지만 경고가 7일 동안 중지된 후 다시 표시되면 다시 경고를 받게 됩니다.

- **삭제**: 경고를 삭제하는 경우 시스템의 데이터베이스에서 삭제되며 복원할 수 없습니다. 삭제를 클릭하면 동일한 유형의 의심스러운 활동을 모두 삭제할 수 있습니다.

- **제외**: 특정 유형의 경고가 더 이상 발생하지 않도록 엔터티를 제외하는 기능입니다. 예를 들어 원격 코드를 실행하는 특정 관리자 또는 DNS 정찰을 수행하는 보안 스캐너와 같은 특정 유형의 의심스러운 활동에 대해 다시 경고가 표시되지 않게 특정 엔터티(사용자 또는 컴퓨터)를 제외하도록 ATA를 설정할 수 있습니다. 타임라인에서 검색 시 의심스러운 활동에 직접 제외를 추가할 수 있을 뿐 아니라 구성 페이지의 **제외**로 이동한 다음 각 의심스러운 활동(예: Pass-the-Ticket)에 대해 제외된 엔터티 또는 서브넷을 수동으로 추가하고 제거할 수 있습니다. 
> [!NOTE]
> ATA 관리자만 구성 페이지를 수정할 수 있습니다.


## 참고 항목
<a id="see-also" class="xliff"></a>
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [ATA 검색 설정 작업](working-with-detection-settings.md)
- [ATA 구성 수정](modifying-ata-center-configuration.md)
