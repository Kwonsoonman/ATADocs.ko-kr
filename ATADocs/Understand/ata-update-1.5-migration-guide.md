---
title: "버전 1.5로 Advanced Threat Analytics 업데이트 마이그레이션 가이드 | Microsoft 문서"
description: "버전 1.5로 ATA를 업데이트하는 절차를 설명합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: fb65eb41-b215-4530-93a2-0b8991f4e980
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b28cb3a0da844b7c460c03726222bc775a9e47da
ms.openlocfilehash: c0efec3abdec8e44c8cf5005d756f973e64312e7


---

# <a name="ata-update-to-15-migration-guide"></a>버전 1.5로의 ATA 업데이트 마이그레이션 가이드
ATA 1.5로 업데이트하는 경우 다음 영역에서 기능이 개선됩니다.

-   검색 시간 단축

-   NAT(Network Address Translation) 장치용으로 향상된 자동 검색 알고리즘 제공

-   도메인에 가입되지 않은 장치용으로 향상된 이름 확인 프로세스 제공

-   제품 업데이트 중에 데이터 마이그레이션 지원

-   수천 개의 엔터티를 사용하여 의심스러운 활동에 대한 UI 응답성 향상

-   모니터링 경고의 자동 해결 기능 개선

-   모니터링 및 문제 해결 기능 향상을 위한 추가 성능 모니터 제공

## <a name="updating-ata-to-version-15"></a>버전 1.5로 ATA 업데이트
> [!NOTE]
> 사용 중인 환경에 ATA가 설치되어 있지 않으면 버전 1.5가 포함된 처음 사용자용 ATA를 다운로드한 다음 [ATA 설치](/advanced-threat-analytics/deploy-use/install-ata)에서 설명하는 표준 설치 절차를 수행하세요.

ATA 버전 1.4를 이미 배포한 경우 이 절차에서는 설치한 버전을 업데이트하는 데 필요한 단계를 안내합니다.

ATA 버전 1.5로 업데이트하려면 다음 단계를 수행합니다.

1.  VLSC 또는 MSDN에서 ATA v1.5를 다운로드합니다.
      > [!NOTE]
         업데이트된 ATA 정식 버전을 사용하여 버전 1.5로의 업데이트를 수행할 수도 있습니다.


2.  ATA 센터를 업데이트합니다.

3.  업데이트된 ATA 게이트웨이 패키지를 다운로드합니다.

4.  ATA 게이트웨이를 업데이트합니다.

    > [!IMPORTANT]
    > ATA가 정상적으로 작동하도록 하려면 모든 ATA 게이트웨이를 업데이트하세요.

### <a name="step-1-update-the-ata-center"></a>1단계: ATA 센터 업데이트

1.  원하는 경우 데이터베이스를 백업합니다.

    -   ATA 센터를 가상 컴퓨터로 실행 중이며 검사점을 가져오려는 경우 먼저 가상 컴퓨터를 종료합니다.

    -   ATA 센터를 실제 서버에서 실행 중인 경우에는 [MongoDB 백업](https://docs.mongodb.org/manual/core/backups/)을 위한 권장 절차를 수행합니다.

2.  업데이트 파일인 Microsoft ATA Center Update.exe를 실행하고 화면의 지침에 따라 업데이트를 설치합니다.

    1.  **시작** 페이지에서 언어를 선택하고 **다음**을 클릭합니다.

    2.  최종 사용자 사용권 계약을 읽고 조건에 동의하면 확인란을 클릭한 후에 **다음**을 클릭합니다.

    3.  전체 마이그레이션(기본값)을 실행할지 아니면 부분 마이그레이션을 실행할지를 선택합니다.

        ![전체 마이그레이션 또는 부분 마이그레이션 선택](media/ATA-center-fullpartial.png)

        -   **부분** 마이그레이션을 선택하면 수집된 네트워크 트래픽과 ATA에서 분석하여 전달된 Windows 이벤트가 모두 삭제되며 사용자 동작 프로필을 다시 학습해야 합니다. 이 과정은 최소&3;주가 소요됩니다. 디스크 공간이 부족하다면 **부분** 마이그레이션을 실행하는 것이 적절합니다.

        -   **전체** 마이그레이션을 실행하는 경우에는 추가 디스크 공간(업그레이드 페이지에서 자동으로 계산됨)이 필요하며 네트워크 트래픽에 따라 마이그레이션 시간이 더 오래 걸릴 수 있습니다. 전체 마이그레이션에서는 이전에 수집한 모든 데이터와 사용자 동작 프로필이 유지됩니다. 따라서 ATA가 동작 프로필을 학습하는 데 시간이 추가로 소요되지 않으며, 업데이트 이후 비정상 동작을 즉시 검색할 수 있습니다.

3.  **업데이트**를 클릭합니다. 업데이트를 클릭하면 업데이트 절차가 완료될 때까지 ATA가 오프라인으로 설정됩니다.

4.  ATA 센터를 업데이트하고 나면 ATA 게이트웨이가 오래된 상태임을 보고합니다.

    ![오래된 게이트웨이 이미지](media/ATA-center-outdated.png)

> [!IMPORTANT]
> - ATA가 정상적으로 작동하도록 하려면 모든 ATA 게이트웨이를 업데이트하세요.

### <a name="step-2-download-the-ata-gateway-setup-package"></a>2단계. ATA 게이트웨이 설치 패키지 다운로드
도메인 연결 설정을 구성하고 나면 ATA Gateway 설치 패키지를 다운로드할 수 있습니다.

ATA 게이트웨이 패키지를 다운로드하려면 다음 단계를 수행합니다.

1.  이전에 다운로드한 ATA 게이트웨이 패키지의 이전 버전을 삭제합니다.

2.  ATA 게이트웨이 컴퓨터에서 브라우저를 열고 ATA 콘솔용으로 ATA 센터에서 구성한 IP 주소를 입력합니다. ATA 콘솔이 열리면 설정 아이콘을 클릭하고 **구성**을 선택합니다.

    ![구성 설정 아이콘](media/ATA-config-icon.JPG)

3.  **ATA 게이트웨이** 탭에서 **ATA 게이트웨이 설치 파일 다운로드**를 클릭합니다.

4.  패키지를 로컬에 저장합니다.

zip 파일에는 다음 항목이 포함되어 있습니다.

-   ATA Gateway 설치 관리자

-   ATA 센터에 연결하는 데 필요한 정보가 포함된 구성 설정 파일

### <a name="step-3-update-the-ata-gateways"></a>3단계: ATA 게이트웨이 업데이트

1.  각 ATA 게이트웨이에서 ATA 게이트웨이 패키지의 파일을 추출한 다음 Microsoft ATA 게이트웨이 설치 파일을 실행합니다.

    > [!NOTE]
    > 이 ATA 게이트웨이 패키지를 사용하여 새 ATA 게이트웨이를 설치할 수도 있습니다.

2.  이전 설정이 유지되기는 하지만 서비스가 다시 시작되려면 몇 분 정도 걸릴 수 있습니다.

3.  배포되어 있는 기타 모든 ATA 게이트웨이에 대해 이 단계를 반복합니다.

> [!NOTE]
> ATA 게이트웨이를 정상적으로 업데이트하고 나면 특정 ATA 게이트웨이에 대한 오래된 버전 알림이 사라집니다.

모든 ATA 게이트웨이가 정상적으로 동기화됨을 보고하며, 업데이트된 ATA 게이트웨이 패키지를 사용할 수 있다는 메시지가 더 이상 표시되지 않으면 모든 ATA 게이트웨이가 올바르게 업데이트된 것입니다.

![업데이트된 게이트웨이 이미지](media/ATA-gw-updated.png)

## <a name="see-also"></a>참고 항목

- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Feb17_HO1-->


