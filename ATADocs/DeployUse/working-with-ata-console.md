---
title: "ATA 콘솔 작업 | Microsoft ATA"
description: "ATA 콘솔 및 콘솔의 구성 요소에 로그인하는 방법을 설명합니다."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1bf264d9-9697-44b5-9533-e1c498da4f07
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: 1eb9397b541eb64cef553f61e8517568d16b0092


---

# ATA 콘솔 작업

ATA 콘솔을 사용하여 ATA에서 검색한 의심스러운 활동을 모니터링하고 대응할 수 있습니다.

## ATA 콘솔에 대한 액세스 설정
ATA Center 서버에서 로컬 관리자 그룹의 구성원인 모든 사용자는 ATA 콘솔에 로그인하고 ATA 설정을 관리할 수 있는 권한이 있습니다.
사용자를 로컬 관리자로 지정하지 않고 ATA 콘솔에 로그인하도록 허용하려면 해당 사용자를 **Microsoft Advanced Threat Analytics Administrators** 로컬 그룹에 추가합니다.

## ATA 콘솔 로그인

1. ATA 센터 서버에서 바탕 화면에 있는 **Microsoft ATA 콘솔** 아이콘을 클릭하거나 브라우저를 열고 ATA 콘솔로 이동합니다.

    ![ATA 서버 아이콘](media/ata-server-icon.png)

>[!NOTE]
> ATA 센터나 ATA 게이트웨이에서 브라우저를 열고 ATA 센터 설치에서 ATA 콘솔에 대해 구성한 IP 주소로 이동합니다.    

2.  사용자 이름과 암호를 입력하고 **로그인**을 클릭합니다.

![ATA 로그인 화면 이미지](media/ATA-log-in-screen.jpg)

> [!NOTE]
> 로컬 관리자 그룹 또는 Microsoft Advanced Threat Analytics Administrators 그룹의 구성원인 사용자로 로그인해야 합니다.

## ATA 콘솔

ATA 콘솔은 모든 의심스러운 활동에 대한 빠른 보기를 시간순으로 제공합니다. 모든 활동의 세부 정보를 검색하고 해당 활동에 따라 작업을 수행할 수 있습니다. 또한 콘솔에는 ATA 네트워크 또는 의심스러운 것으로 간주되는 새로운 활동에 대한 문제를 강조하는 경고 및 알림도 표시됩니다.

이는 ATA 콘솔의 주요 요소입니다.


### 공격 타임라인

ATA 콘솔에 로그인하면 이 기본 시작 페이지로 이동합니다. 기본적으로 해결되지 않은 모든 의심스러운 활동이 공격 타임라인에 표시됩니다. 모두, 미해결, 해제됨 또는 해결됨 상태의 의심스러운 활동을 표시하도록 공격 타임라인을 필터링할 수 있습니다. 또한 각 활동에 할당된 심각도를 볼 수 있습니다.

![ATA 공격 타임라인 이미지](media/attack-timeline.png)

자세한 내용은 [의심스러운 활동 작업](/advanced-threat-analytics/deploy-use/working-with-suspicious-activities)을 참조하세요.

### 알림 표시줄

새로운 의심스러운 활동이 검색된 경우 오른쪽에 알림 표시줄이 자동으로 열립니다. 마지막으로 로그인한 시간 이후에 새로운 의심스러운 활동이 있는 경우에는 로그인에 성공한 후에 알림 표시줄이 열립니다. 언제든지 오른쪽에 있는 화살표를 클릭하여 알림 표시줄에 액세스할 수 있습니다.

![ATA 알림 표시줄 이미지](media/notification-bar.png)

### 필터링 패널

공격 타임라인에 표시되거나 엔터티 프로필 의심스러운 활동 탭에 표시되는 의심스러운 활동을 상태 및 심각도에 따라 필터링할 수 있습니다.

### 검색 창

최상위 메뉴에서 검색 창을 찾을 수 있습니다. ATA에서 특정 사용자, 컴퓨터 또는 그룹을 검색할 수 있습니다. 검색하려면 입력을 시작하기만 하면 됩니다.

![ATA 콘솔 검색 이미지](media/ATA-console-search.png)

### 상태 관리 센터

상태 관리 센터에서는 ATA 배포에서 제대로 작동하지 않는 요소가 있는 경우 경고를 제공합니다.

![ATA 상태 관리 센터 이미지](media/health-center.png)

시스템에서 연결 오류 또는 ATA Gateway 연결 끊김 등의 문제가 발생할 때마다 상태 관리 센터 아이콘에 빨간색 점이 표시됩니다. ![ATA 상태 관리 센터 빨간색 점 이미지](media/ATA-Health-Center-Alert-red-dot.png)

상태 관리 센터 경고는 해제하거나 해결할 수 있으며 심각도에 따라 높음, 중간 또는 낮음으로 분류할 수 있습니다. 해결한 경고를 ATA 서비스에서 여전히 활성 상태인 것으로 검색한 경우 이 경고는 자동으로 미해결 경고 목록으로 이동합니다. 시스템에서 더 이상 경고의 원인이 없는 것으로 검색한 경우(상황이 해결된 경우) 이 경고는 자동으로 해결됨 목록으로 이동합니다.

### 사용자 및 컴퓨터 프로필

ATA에서는 네트워크의 각 사용자 및 컴퓨터에 대한 프로필을 작성합니다. 사용자 프로필에는 ATA가그룹 멤버 자격, 최근 로그인 및 최근에 액세스한 리소스와 같은 일반 정보가 표시합니다.

![사용자 프로필](media/user-profile.png)

컴퓨터 프로필에는 ATA가 최근 로그인 및 최근에 액세스한 리소스와 같은 일반 정보를 표시합니다.

![컴퓨터 프로필](media/computer-profile.png)

ATA에서는 요약, 활동 및 의심스러운 활동 페이지에서 엔터티(컴퓨터, 장치, 사용자)에 대한 추가 정보를 제공합니다.

ATA에서 완전히 확인할 수 없는 프로필 옆에는 절반이 채워진 원 아이콘이 표시됩니다.


![ATA 미확인 프로필 이미지](media/ATA-Unresolved-Profile.jpg)

### 최소 프로필

콘솔의 도처에 사용자 또는 컴퓨터와 같은 단일 엔터티가 표시된 곳이 있습니다. 엔터티 위로 마우스를 가져가면 다음 정보(사용 가능한 경우)가 표시된 최소 프로필이 자동으로 열립니다.

![ATA 최소 프로필 이미지](media/ATA-mini-profile.jpg)

-   Name

-   사진

-   전자 메일

-   전화

-   심각도별 의심스러운 활동 수



## 참고 항목
[ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO4-->


