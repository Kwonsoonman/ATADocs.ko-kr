---
title: "버전 1.7으로의 ATA 업데이트 마이그레이션 가이드 | Microsoft ATA"
description: "버전 1.7으로 ATA를 업데이트하는 절차"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: fb65eb41-b215-4530-93a2-0b8991f4e980
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e3b690767e5c6f5561a97a73eccfbf50ddb04148
ms.openlocfilehash: 5c20c41c3fe587f18087d64f4f84c1df65072fde


---

# 버전 1.7으로의 ATA 업데이트 마이그레이션 가이드
ATA 1.7 업데이트에서는 다음 영역에 대한 향상된 기능을 제공합니다.

-   새 검색

-   기존 검색 기능 개선
  

## 버전 1.7로 ATA 업데이트
> [!NOTE] 
> 사용 중인 환경에 ATA가 설치되어 있지 않으면 버전 1.7이 포함된 처음 사용자용 ATA를 다운로드한 다음 [ATA 설치](/advanced-threat-analytics/deploy-use/install-ata)에서 설명하는 표준 설치 절차를 수행하세요.

ATA 버전 1.6을 이미 배포한 경우 이 절차에서는 배포를 업데이트하는 데 필요한 단계를 안내합니다.

> [!NOTE] 
> ATA 버전 1.4 또는 1.5가 설치된 상태에서 ATA 버전 1.7을 곧바로 설치할 수 없습니다. ATA 버전 1.6을 먼저 설치해야 합니다. 

ATA 버전 1.7로 업데이트하려면 다음 단계를 수행합니다.

1.  [업데이트 1.7 버전을 다운로드합니다.](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics)<br>
이 버전에서는 새 ATA 배포 설치와 기존 배포 업그레이드에 동일한 설치 파일(Microsoft ATA 센터 Setup.exe)이 사용됩니다.

2.  ATA 센터를 업데이트합니다.

4.  ATA 게이트웨이를 업데이트합니다.

    > [!IMPORTANT]
    > ATA가 정상적으로 작동하도록 하려면 모든 ATA 게이트웨이를 업데이트하세요.

### 1단계: ATA 센터 업데이트

1.  원하는 경우 데이터베이스를 백업합니다.

    -   ATA 센터를 가상 컴퓨터로 실행 중이며 검사점을 가져오려는 경우 먼저 가상 컴퓨터를 종료합니다.

    -   ATA 센터를 실제 서버에서 실행 중인 경우에는 [MongoDB 백업](https://docs.mongodb.org/manual/core/backups/)을 위한 권장 절차를 수행합니다.

2.  설치 파일인 **Microsoft ATA Center Setup.exe**를 실행하고 화면의 지침에 따라 업데이트를 설치합니다.

    -  **시작** 페이지에서 언어를 선택하고 **다음**을 클릭합니다.

    -  버전 1.6에서 자동 업데이트를 사용하도록 설정하지 않은 경우에는 ATA가 최신 상태로 유지되도록 ATA에서 Microsoft Update를 사용하도록 설정하라는 메시지가 표시됩니다.  Microsoft 업데이트 페이지에서 **업데이트를 확인할 때 Microsoft 업데이트 사용(권장)**을 선택합니다.
    ![ATA를 최신 이미지로 유지](media/ata_ms_update.png) 여기에 보이는 것처럼 다른 Microsoft 제품(ATA 포함)에 대한 업데이트를 사용하도록 Windows 설정을 조정합니다. 
     ![Windows 자동 업데이트 이미지](media/ata_installupdatesautomatically.png)

    -  **데이터 마이그레이션** 화면에서 데이터 전체를 마이그레이션할지, 데이터 일부를 마이그레이션할지 선택합니다. 일부 데이터만 마이그레이션하기로 선택한 경우에는 이전에 캡처된 네트워크 트래픽 및 동작 프로파일이 마이그레이션되지 않습니다. 비정상적인 동작 검색에서 이상 활동 검색을 사용하도록 설정할 전체 프로파일이 생성되는데 3주가 걸린다는 것을 의미합니다. 3주 동안 다른 모든 ATA 검색은 제대로 작동합니다. **부분** 데이터 마이그레이션은 설치하는 데 시간이 훨씬 더 적게 걸립니다. **전체** 데이터 마이그레이션을 선택하면 설치를 완료하는 데 상당한 시간이 걸릴 수 있습니다. **데이터 마이그레이션** 화면에 나열된 예상된 시간과 필요한 디스크 공간 크기는 이전 버전의 ATA에 저장해 놓은 이전에 캡처된 네트워크 트래픽의 양에 따라 달라 집니다. **부분** 또는 **전체**를 선택하기 전에 이러한 요구 사항을 확인해야 합니다.  
    
    ![ATA 데이터 마이그레이션](media/migration data migration.png)

    -  **업데이트**를 클릭합니다. 업데이트를 클릭하면 업데이트 절차가 완료될 때까지 ATA가 오프라인으로 설정됩니다.

4.  ATA 센터 업데이트가 성공적으로 완료되면 **시작**을 클릭하고 ATA 콘솔에서 ATA 게이트웨이에 대한 **업데이트** 화면을 엽니다.
    ![업데이트 성공 화면](media/migration center success.png)

5.  **업데이트** 화면에서 이미 ATA 게이트웨이가 자동으로 업데이트 되도록 설정한 경우 이 시점에서 업데이트가 진행됩니다. 그렇지 않으면 각 ATA 게이트웨이 옆에 있는 **업데이트**를 클릭합니다.
  ![게이트웨이 업데이트 이미지](media/migration update gw.png)

  
> [!IMPORTANT] 
> ATA가 정상적으로 작동하도록 하려면 모든 ATA 게이트웨이를 업데이트하세요.
> 모든 게이트웨이에 구성된 Syslog 수신기 포트가 514로 변경됩니다.
 
    > [!NOTE] 
    > To install new ATA Gateways, go the **Gateways** screen and click **Download Gateway Setup** to get the ATA 1.7 installation package and follow the instructions for new Gateway installation as described in [Step 4. Install the ATA Gateway](/advanced-threat-analytics/deploy-use/install-ata-step4) .



## 참고 항목

- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Oct16_HO1-->


