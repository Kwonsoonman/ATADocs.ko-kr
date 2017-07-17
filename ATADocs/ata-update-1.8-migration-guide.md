---
title: "버전 1.8로 Advanced Threat Analytics 업데이트 마이그레이션 가이드 | Microsoft Docs"
description: "버전 1.8로 ATA를 업데이트하는 절차"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/9/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e5a9718c-b22e-41f7-a614-f00fc4997682
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: ff61d12eefaf6fb0a6b3d92568ef8c25c9d4c49b
ms.sourcegitcommit: 3177d5894413fbd363b9aca8130f3f7a369223b8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2017
---
# 버전 1.8로 ATA 업데이트
<a id="updating-ata-to-version-18" class="xliff"></a>

> [!NOTE] 
> 사용 중인 환경에 ATA가 설치되어 있지 않으면 버전 1.8이 포함된 처음 사용자용 ATA를 다운로드한 다음 [ATA 설치](install-ata-step1.md)에서 설명하는 표준 설치 절차를 수행하세요.

ATA 버전 1.7을 이미 배포한 경우 이 절차에서는 배포를 업데이트하는 데 필요한 단계를 안내합니다.

> [!NOTE] 
>  ATA 버전 1.7 업데이트 1 및 1.7 업데이트 2만 ATA 버전 1.8로 업데이트할 수 있습니다. 이전 버전의 ATA는 ATA 버전 1.8로 직접 업데이트할 수 없습니다.

ATA 버전 1.8로 업데이트하려면 다음 단계를 수행합니다.

1.  [다운로드 센터에서 ATA 1.8의 업데이트 버전을 다운로드](https://www.microsoft.com/download/details.aspx?id=55536)하거나 [평가 센터](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics)에서 전체 버전을 다운로드합니다.<br>
마이그레이션 버전의 파일은 ATA 1.7에서 업데이트하는 용도로만 사용할 수 있습니다. 평가 센터 버전에서는 새 ATA 배포 설치와 기존 배포 업그레이드에 동일한 설치 파일(Microsoft ATA 센터 Setup.exe)이 사용됩니다.

2.  ATA 센터를 업데이트합니다.

4.  ATA 게이트웨이를 업데이트합니다.

    > [!IMPORTANT]
    > ATA가 정상적으로 작동하도록 하려면 모든 ATA 게이트웨이를 업데이트하세요.

### 1단계: ATA 센터 업데이트
<a id="step-1-update-the-ata-center" class="xliff"></a>

1.  원하는 경우 데이터베이스를 백업합니다.

    -   ATA 센터를 가상 컴퓨터로 실행 중이며 검사점을 가져오려는 경우 먼저 가상 컴퓨터를 종료합니다.

    -   물리적 서버에서 ATA 센터를 실행하는 경우 데이터베이스를 백업하는 방법에 대한 자세한 내용은 [재해 복구](disaster-recovery.md) 문서를 참조하세요.

2.  설치 파일인 **Microsoft ATA Center Setup.exe**를 실행하고 화면의 지침에 따라 업데이트를 설치합니다.

    -  **시작** 페이지에서 언어를 선택하고 **다음**을 클릭합니다.

    -  버전 1.7에서 자동 업데이트를 사용하도록 설정하지 않은 경우에는 ATA가 최신 상태로 유지되도록 ATA에서 Microsoft Update를 사용하도록 설정하라는 메시지가 표시됩니다.  Microsoft 업데이트 페이지에서 **업데이트를 확인할 때 Microsoft 업데이트 사용(권장)**을 선택합니다.
    ![ATA를 최신 이미지로 유지](media/ata_ms_update.png)
     
     이렇게 하면 ATA에 대한 업데이트를 사용하도록 Windows 설정이 조정됩니다. 
    
    -  **데이터 마이그레이션** 화면에서 데이터 전체를 마이그레이션할지, 데이터 일부를 마이그레이션할지 선택합니다. 부분 데이터만 마이그레이션하도록 선택하는 경우 전체 프로필을 작성하는 데 3주가 걸리는 비정상적인 동작 검색을 제외한 모든 검색이 즉시 작동합니다.  
    
    **부분** 데이터 마이그레이션은 설치하는 데 시간이 훨씬 더 적게 걸립니다. **전체** 데이터 마이그레이션을 선택하면 설치를 완료하는 데 상당한 시간이 걸릴 수 있습니다. **데이터 마이그레이션** 화면에 나열된 예상 시간과 필요한 디스크 공간을 확인합니다. 이러한 수치는 이전 버전의 ATA에서 저장한 이전에 캡처된 네트워크 트래픽의 양에 따라 달라집니다. 예를 들어 아래 화면에서는 매우 큰 데이터베이스에서의 데이터 마이그레이션을 확인할 수 있습니다.
         
    ![ATA 데이터 마이그레이션](media/migration-data-migration.png)

    -  **업데이트**를 클릭합니다. 업데이트를 클릭하면 업데이트 절차가 완료될 때까지 ATA가 오프라인으로 설정됩니다.

4.  ATA 센터 업데이트가 성공적으로 완료되면 **시작**을 클릭하고 ATA 콘솔에서 ATA 게이트웨이에 대한 **업데이트** 화면을 엽니다.

    ![업데이트 성공 화면](media/migration-center-success.png)

5.  **업데이트** 화면에서 이미 ATA 게이트웨이가 자동으로 업데이트 되도록 설정한 경우 이 시점에서 업데이트가 진행됩니다. 그렇지 않으면 각 ATA 게이트웨이 옆에 있는 **업데이트**를 클릭합니다.
  
![게이트웨이 업데이트 이미지](media/migration-update-gw.png)

  
> [!IMPORTANT] 
> ATA가 정상적으로 작동하도록 하려면 모든 ATA 게이트웨이를 업데이트하세요.
 
> [!NOTE] 
> 새 ATA 게이트웨이를 설치하려면 **게이트웨이** 화면으로 가서 **게이트웨이 설치 다운로드**를 클릭한 후 ATA 1.8 게이트웨이 설치 패키지를 받고 [4단계. ATA 게이트웨이 설치](install-ata-step4.md)에 설명된 대로 새 게이트웨이 설치에 대한 지침을 따릅니다.


## 참고 항목
<a id="see-also" class="xliff"></a>

- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
