---
title: "Advanced Threat Analytics 설치 - 1단계 | Microsoft 문서"
description: "ATA를 설치하는 첫 번째 단계에는 ATA Center를 다운로드하여 선택한 서버에 설치하는 과정이 포함됩니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/23/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b28cb3a0da844b7c460c03726222bc775a9e47da
ms.openlocfilehash: 35949dfc81ed3753bf1e449a2de06bdf0403fe78


---

*적용 대상: Advanced Threat Analytics 버전 1.7*



# <a name="install-ata---step-1"></a>ATA 설치 - 1단계

>[!div class="step-by-step"]
[2단계 »](install-ata-step2.md)

이 설치 절차에서는 ATA 1.7을 새로 설치하는 데 필요한 지침을 제공합니다. 기존의 ATA 배포를 이전 버전에서 업데이트하는 방법에 대한 내용은 [ATA 버전 1.7 마이그레이션 가이드](/advanced-threat-analytics/understand-explore/ata-update-1.7-migration-guide)를 참조하세요.

> [!IMPORTANT] 
> Windows 2012 R2를 사용할 경우 설치를 시작하기 전에 ATA Center 및 ATA Gateway 서버에 KB2934520을 설치할 수 있습니다. 그렇지 않으면 ATA 설치에서 이 업데이트를 설치하므로 ATA 설치 도중에 다시 시작해야 합니다.

## <a name="step-1-download-and-install-the-ata-center"></a>1단계. ATA Center 다운로드 및 설치
서버가 요구 사항을 충족하는지 확인한 후 ATA Center 설치를 진행할 수 있습니다.

ATA Center 서버에서 다음 단계를 수행합니다.

1.  [Microsoft 볼륨 라이선스 서비스 센터](https://www.microsoft.com/Licensing/servicecenter/default.aspx) 또는 [TechNet 평가 센터](http://www.microsoft.com/evalcenter/) 또는 [MSDN](https://msdn.microsoft.com/subscriptions/downloads)에서 ATA를 다운로드합니다.

2.  ATA 센터를 설치할 컴퓨터에 로컬 관리자 그룹의 구성원인 사용자로 로그인합니다.

3.  **Microsoft ATA 센터 Setup.EXE**를 실행하고 설치 마법사를 따릅니다.

> [!NOTE]   
> 설치 과정에서 다시 부팅해야 하는 경우 문제를 방지하려면 탑재된 ISO 파일이 아니라 로컬 드라이브에서 설치 파일을 실행해야 합니다.   

4.  설치를 시작할 때 Microsoft .Net Framework가 설치되지 않은 경우 설치하라는 메시지가 표시됩니다. .NET Framework를 설치하고 나면 다시 부팅하라는 메시지가 표시될 수 있습니다.
5.  **시작** 페이지에서 ATA 설치 화면에 사용할 언어를 선택하고 **다음**을 클릭합니다.

6.  Microsoft 소프트웨어 사용 조건을 읽고 동의하면 확인란을 클릭한 후 **다음**을 클릭합니다.

7.  ATA를 자동으로 업데이트하도록 설정하는 것이 좋습니다. 컴퓨터에서 Windows를 자동으로 업데이트하도록 설정하지 않은 경우 **Microsoft 업데이트를 사용하여 컴퓨터의 보안 및 최신 상태 유지** 화면이 표시됩니다. 
    ![ATA를 최신 이미지로 유지](media/ata_ms_update.png)

8. **업데이트를 확인할 때 Microsoft 업데이트 사용(권장)**을 선택합니다. 다음 그림과 같이 다른 Microsoft 제품(ATA 포함)에 업데이트를 사용하도록 Windows 설정을 조정합니다. 
    ![Windows 자동 업데이트 이미지](media/ata_installupdatesautomatically.png)

8.  **ATA 센터 구성** 페이지에서 사용자 환경에 따라 다음 정보를 입력합니다.

    |필드|설명|설명|
    |---------|---------------|------------|
    |설치 경로|ATA Center를 설치할 위치입니다. 기본적으로 %programfiles%\Microsoft Advanced Threat Analytics\Center입니다.|기본값을 그대로 둡니다.|
    |데이터베이스 데이터 경로|MongoDB 데이터베이스 파일이 있는 위치입니다. 기본적으로 %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data입니다.|크기 조정에 따라 증가할 여유가 있는 곳으로 위치를 변경합니다. **참고:** <ul><li>프로덕션 환경에서는 용량 계획에 따라 충분한 공간이 있는 드라이브를 사용해야 합니다.</li><li>대규모 배포의 경우 데이터베이스는 별도의 물리적 디스크에 있어야 합니다.</li></ul>크기 조정에 대한 자세한 내용은 [ATA 용량 계획](/advanced-threat-analytics/plan-design/ata-capacity-planning)을 참조하세요.|
    |센터 서비스 IP 주소: 포트|ATA Center 서비스가 ATA Gateway 통신을 위해 수신 대기할 IP 주소입니다.<br /><br />**기본 포트:** 443|ATA Center 서비스에서 사용할 IP 주소를 선택하려면 아래쪽 화살표를 클릭합니다.<br /><br />ATA Center 서비스의 IP 주소 및 포트는 ATA 콘솔의 IP 주소 및 포트와 같을 수 없습니다. ATA 콘솔의 포트를 변경해야 합니다.|
    |센터 서비스 SSL 인증서|ATA 콘솔 및 ATA 센터 서비스에서 사용할 인증서입니다.|열쇠 아이콘을 클릭하여 설치된 인증서를 선택하거나, 랩 환경에 배포하는 경우 자체 서명된 인증서를 선택합니다.|
    |콘솔 IP 주소|ATA 콘솔에서 사용할 IP 주소입니다.|ATA 콘솔에서 사용하는 IP 주소를 선택하려면 아래쪽 화살표를 클릭합니다. **참고:** ATA Gateway에서 ATA 콘솔에 보다 쉽게 액세스하려면 이 IP 주소를 적어 두세요.|
    
    ![ATA Center 구성 이미지](media/ATA-Center-Configuration.png)

10.  **설치**를 클릭하여 ATA 센터 및 해당 구성 요소를 설치합니다.
    ATA Center 설치 중에 다음 구성 요소가 설치되고 구성됩니다.

    -   ATA 센터 서비스

    -   MongoDB

    -   사용자 지정 성능 모니터 데이터 컬렉션 집합

    -   자체 서명된 인증서(설치 중에 선택한 경우)

11.  설치가 완료되면 **시작**을 클릭하여 ATA 콘솔에 연결합니다.
이때 **일반** 설정 페이지로 자동으로 이동됩니다. 여기에서 ATA Gateway 구성 및 배포를 계속할 수 있습니다.
IP 주소를 사용하여 사이트에 로그인하기 때문에 인증서와 관련된 경고 메시지가 표시되는데, 이는 정상이며 **이 웹 사이트를 계속 탐색**을 클릭해야 합니다.

### <a name="validate-installation"></a>설치 유효성 검사

1.  **Microsoft Advanced Threat Analytics Center** 서비스가 실행 중인지 확인합니다.
2.  바탕 화면에서 **Microsoft Advanced Threat Analytics** 바로 가기를 클릭하여 ATA 콘솔에 연결합니다. ATA Center를 설치하는 데 사용한 것과 동일한 사용자 자격 증명으로 로그인합니다.



>[!div class="step-by-step"]
[« 설치 전](configure-port-mirroring.md)
[2단계 »](install-ata-step2.md)

## <a name="see-also"></a>참고 항목

- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [이벤트 수집 구성](configure-event-collection.md)
- [ATA 필수 구성 요소](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Feb17_HO1-->


