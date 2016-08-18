---
title: "버전 1.6으로의 ATA 업데이트 마이그레이션 가이드 | Microsoft ATA"
description: "버전 1.6으로 ATA를 업데이트하는 절차"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: fb65eb41-b215-4530-93a2-0b8991f4e980
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: 87cb9534a45d3a8ca29d6a803ca399a33a3d3ea6


---

# 버전 1.6으로의 ATA 업데이트 마이그레이션 가이드
ATA 1.6 업데이트에서는 다음 영역에 대한 향상된 기능을 제공합니다.

-   새 검색

-   기존 검색 기능 개선

-   ATA 경량 게이트웨이

-   자동 업데이트

-   향상된 ATA 센터 성능

-   저장소 요구 사항 감소

-   IBM QRadar 지원

## 버전 1.6으로 ATA 업데이트
> [!NOTE] 
> 사용 중인 환경에 ATA가 설치되어 있지 않으면 버전 1.6이 포함된 처음 사용자용 ATA를 다운로드한 다음 [ATA 설치](/advanced-threat-analytics/deploy-use/install-ata)에서 설명하는 표준 설치 절차를 수행하세요.

ATA 버전 1.5를 이미 배포한 경우 이 절차에서는 배포를 업데이트하는 데 필요한 단계를 안내합니다.

> [!NOTE] 
> ATA 버전 1.4가 설치된 상태에서 ATA 버전 1.6을 곧바로 설치할 수 없습니다. ATA 버전 1.5를 먼저 설치해야 합니다. 실수로 ATA 1.5를 설치하지 않고 ATA 1.6을 설치하려고 하면 **최신 버전이 컴퓨터에 이미 설치되어 있습니다.** 오류가 나타납니다. ATA 버전 1.5를 설치하기 전에 컴퓨터에서 ATA 1.6의 남아 있는 항목을 제거해야 합니다(설치가 실패하더라도).

ATA 버전 1.6으로 업데이트하려면 다음 단계를 수행합니다.

1. 업그레이드 문제를 방지하려면 [ATA 버전 1.6의 새로운 기능](whats-new-version-1.6.md)에 설명된 **ATA 버전 1.6으로 업데이트할 때 마이그레이션 실패**의 8~10단계를 수행해야 합니다.
2. 업그레이드를 완료하는 데 필요한 사용 가능한 공간이 있는지 확인하세요. 준비 검사까지 설치 단계를 수행하여 사용 가능한 공간이 얼마나 필요한지 확인한 다음 필요한 디스크 공간을 할당한 후 업그레이드를 다시 시작할 수 있습니다.
1.  [업데이트 1.6 버전을 다운로드합니다.](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics)<br>
이 버전에서는 새 ATA 배포 설치와 기존 배포 업그레이드에 동일한 설치 파일(Microsoft ATA 센터 Setup.exe)이 사용됩니다.

2.  ATA 센터를 업데이트합니다.

3.  업데이트된 ATA 게이트웨이 패키지를 다운로드합니다.

4.  ATA 게이트웨이를 업데이트합니다.

    > [!IMPORTANT]
    > ATA가 정상적으로 작동하도록 하려면 모든 ATA 게이트웨이를 업데이트하세요.

### 1단계: ATA 센터 업데이트

1.  원하는 경우 데이터베이스를 백업합니다.

    -   ATA 센터를 가상 컴퓨터로 실행 중이며 검사점을 가져오려는 경우 먼저 가상 컴퓨터를 종료합니다.

    -   ATA 센터를 실제 서버에서 실행 중인 경우에는 [MongoDB 백업](https://docs.mongodb.org/manual/core/backups/)을 위한 권장 절차를 수행합니다.

2.  설치 파일인 Microsoft ATA 센터 Setup.exe를 실행하고 화면의 지침에 따라 업데이트를 설치합니다.

    1.  ATA 1.6을 사용하려면 .Net Framework 4.6.1을 설치해야 합니다. 아직 설치하지 않은 경우 ATA를 설치할 때 설치의 일부로 .Net Framework 4.6.1이 설치됩니다.<br>
    > [!NOTE]
    > .NET Framework 4.6.1을 설치하려면 서버를 다시 시작해야 할 수 있습니다. ATA 설치는 서버를 다시 시작한 후에만 진행됩니다.
5.  **시작** 페이지에서 언어를 선택하고 **다음**을 클릭합니다.

    6.  최종 사용자 사용권 계약을 읽고 조건에 동의하는 경우 **다음**을 클릭합니다.

    7.  ATA에 대한 Microsoft 업데이트를 사용하여 최신 상태로 유지할 수 있습니다.  Microsoft 업데이트 페이지에서 **업데이트를 확인할 때 Microsoft 업데이트 사용(권장)**을 선택합니다.
    ![ATA를 최신 이미지로 유지](media/ata_ms_update.png) 여기에 보이는 것처럼 다른 Microsoft 제품(ATA 포함)에 대한 업데이트를 사용하도록 Windows 설정을 조정합니다. 
     ![Windows 자동 업데이트 이미지](media/ata_installupdatesautomatically.png)

    8.  설치를 시작하기 전에 ATA에서 준비 검사를 수행합니다. 검사 결과를 검토하여 필수 구성 요소가 구성되어 있고 디스크 공간이 최소 크기 이상인지 확인합니다. 
    ![ATA 준비 상태 확인 이미지](media/ata_install_readinesschecks.png)

    3.  **업데이트**를 클릭합니다. 업데이트를 클릭하면 업데이트 절차가 완료될 때까지 ATA가 오프라인으로 설정됩니다.

4.  ATA 센터를 업데이트하고 나면 ATA 게이트웨이가 오래된 상태임을 보고합니다.

    ![오래된 게이트웨이 이미지](media/ATA-center-outdated.png)

> [!IMPORTANT] 
> ATA가 정상적으로 작동하도록 하려면 모든 ATA 게이트웨이를 업데이트하세요.

### 2단계. ATA Gateway 설치 패키지 다운로드
도메인 연결 설정을 구성하고 나면 ATA Gateway 설치 패키지를 다운로드할 수 있습니다.

ATA Gateway 패키지를 다운로드하려면 다음 단계를 수행합니다.

1.  이전에 다운로드한 ATA 게이트웨이 패키지의 이전 버전을 삭제합니다.

2.  ATA 게이트웨이 컴퓨터에서 브라우저를 열고 ATA 콘솔용으로 ATA 센터에서 구성한 IP 주소를 입력합니다. ATA 콘솔이 열리면 설정 아이콘을 클릭하고 **구성**을 선택합니다.

    ![구성 설정 아이콘](media/ATA-config-icon.JPG)

3.  **ATA 게이트웨이** 탭에서 **ATA 게이트웨이 설치 파일 다운로드**를 클릭합니다.

4.  패키지를 로컬에 저장합니다.

zip 파일에는 다음 항목이 포함되어 있습니다.

-   ATA Gateway 설치 관리자

-   ATA 센터에 연결하는 데 필요한 정보가 포함된 구성 설정 파일

### 3단계: ATA 게이트웨이 업데이트

1.  각 ATA 게이트웨이에서 ATA 게이트웨이 패키지의 파일을 추출한 다음 **Microsoft ATA Gateway Setup.exe**를 실행합니다.

    > [!NOTE] 
    > 이 ATA 게이트웨이 패키지를 사용하여 새 ATA 게이트웨이를 설치할 수도 있습니다.

2.  이전 설정이 유지되기는 하지만 서비스가 다시 시작되려면 몇 분 정도 걸릴 수 있습니다.

3.  배포되어 있는 기타 모든 ATA 게이트웨이에 대해 이 단계를 반복합니다.

> [!NOTE] 
> ATA 게이트웨이를 정상적으로 업데이트하고 나면 특정 ATA 게이트웨이에 대한 오래된 버전 알림이 해결됩니다.

모든 ATA 게이트웨이가 정상적으로 동기화됨을 보고하며, 업데이트된 ATA 게이트웨이 패키지를 사용할 수 있다는 메시지가 더 이상 표시되지 않으면 모든 ATA 게이트웨이가 올바르게 업데이트된 것입니다.

![업데이트된 게이트웨이 이미지](media/ATA-gw-updated.png)


## 참고 항목

- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO4-->


