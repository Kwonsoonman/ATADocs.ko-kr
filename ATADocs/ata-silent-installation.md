---
title: "Advanced Threat Analytics 자동 설치 | Microsoft 문서"
description: "ATA를 자동으로 설치하는 방법을 설명합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 3210d9153cd6781ae13a784e1f2b5927e0703009
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*


# <a name="ata-silent-installation"></a>ATA 자동 설치
이 문서에는 ATA 자동 설치에 대한 지침이 있습니다.

## <a name="prerequisites"></a>전제 조건

ATA 버전 1.8을 사용하려면 Microsoft .NET Framework 4.6.1이 설치되어 있어야 합니다. 

ATA를 설치하거나 업데이트하면 Microsoft ATA 배포의 일부로 .NET Framework 4.6.1이 자동으로 설치됩니다.

> [!Note] 
> .NET framework 4.6.1을 설치하려면 서버를 다시 부팅해야 할 수 있습니다. 도메인 컨트롤러에서 ATA 게이트웨이를 설치할 때 해당 도메인 컨트롤러에 대해 유지 관리 기간을 예약하는 것이 좋습니다.
ATA 자동 설치 방법을 사용하는 경우 설치가 끝나면 서버를 자동으로 다시 시작하도록 설치 관리자가 구성됩니다(필요한 경우). Windows Installer 버그 때문에 서버가 다시 시작되지 않도록 norestart 플래그를 안정적으로 사용할 수 없으므로 유지 관리 기간에만 자동 설치를 실행해야 합니다.

배포 진행 상태를 추적하려면 **%AppData%\Local\Temp**에 있는 ATA 설치 관리자 로그를 모니터링합니다.


## <a name="install-the-ata-center"></a>ATA 센터를 설치합니다.

다음 명령을 사용하여 ATA 센터를 설치합니다.

**구문**:

    "Microsoft ATA Center Setup.exe" [/quiet] [/Help] [--LicenseAccepted] [NetFrameworkCommandLineArguments="/q"] [InstallationPath="<InstallPath>"] [DatabaseDataPath= "<DBPath>"] [CenterIpAddress=<CenterIPAddress>] [CenterPort=<CenterPort>] [CenterCertificateThumbprint="<CertThumbprint>"] 
    [ConsoleIpAddress=<ConsoleIPAddress>] [ConsoleCertificateThumbprint="<CertThumbprint >"]
    
**설치 옵션**:

> [!div class="mx-tableFixed"]
|Name|구문|자동 설치에 필수인가요?|설명|
|-------------|----------|---------|---------|
|Quiet|/quiet|예|UI 및 프롬프트를 표시하지 않고 설치 관리자를 실행합니다.|
|도움말|/help|아니요|도움말 및 빠른 참조를 제공합니다. 모든 옵션 및 동작 목록을 포함하여 설정 명령에 대한 올바른 사용법을 보여줍니다.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|예|.Net Framework 설치를 위한 매개 변수를 지정합니다. .Net Framework 자동 설치를 적용하도록 설정해야 합니다.|
|LicenseAccepted|--LicenseAccepted|예|라이선스를 읽고 승인했는지를 나타냅니다. 자동 설치에 설정되어 있어야 합니다.|

**설치 매개 변수**:

> [!div class="mx-tableFixed"]
|Name|구문|자동 설치에 필수인가요?|설명|
|-------------|----------|---------|---------|
|InstallationPath|InstallationPath="<InstallPath>"|아니요|ATA 이진 파일을 설치할 경로를 설정합니다. 기본 경로는 C:\Program Files\Microsoft Advanced Threat Analytics\Center입니다.|
|DatabaseDataPath|DatabaseDataPath= “<DBPath>”|아니요|ATA 데이터베이스 데이터 폴더 경로를 설정합니다. 기본 경로는 C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data입니다.|
|CenterIpAddress|CenterIpAddress=<CenterIPAddress>|예|ATA 센터 서비스의 IP 주소를 설정합니다.|
|CenterPort|CenterPort=<CenterPort>|예|ATA 센터 서비스의 네트워크 포트를 설정합니다.|
|CenterCertificateThumbprint|CenterCertificateThumbprint="<CertThumbprint>"|아니요|ATA 센터 서비스에 대한 인증서 지문을 설정합니다. 이 인증서는 ATA 센터와 ATA 게이트웨이 간 보안 통신에 사용됩니다. 설정하지 않으면 설치할 때 자체 서명된 인증서가 생성됩니다.|
|ConsoleIpAddress|ConsoleIpAddress=<ConsoleIPAddress>|예|ATA 콘솔의 IP 주소를 설정합니다.|
|ConsoleCertificateThumbprint|ConsoleCertificateThumbprint="<CertThumbprint >"|아니요|ATA 콘솔용 인증서 지문을 지정합니다. 이 인증서는 ATA 콘솔 웹 사이트 ID의 유효성을 검사하는 데 사용됩니다. 지정하지 않으면 설치할 때 자체 서명된 인증서가 생성됩니다.|

**예**: 기본 설치 경로 및 단일 IP 주소를 사용하여 ATA 센터를 설치하려면 다음을 수행합니다.

    "Microsoft ATA Center Setup.exe" /quiet --LicenseAccepted NetFrameworkCommandLineArguments="/q" CenterIpAddress=192.168.0.10
    CenterPort=444 ConsoleIpAddress=192.168.0.10

기본 설치 경로, 두 개의 IP 주소, 사용자 정의 인증서 지문을 사용하여 ATA 센터를 설치하려면 다음을 수행합니다.

    "Microsoft ATA Center Setup.exe" /quiet --LicenseAccepted NetFrameworkCommandLineArguments ="/q" CenterIpAddress=192.168.0.10 CenterPort=443 CenterCertificateThumbprint= ‎"1E2079739F624148ABDF502BF9C799FCB8C7212F"
    ConsoleIpAddress=192.168.0.11  ConsoleCertificateThumbprint="G9530253C976BFA9342FD1A716C0EC94207BFD5A"

## <a name="update-the-ata-center"></a>ATA 센터를 업데이트합니다.

다음 명령을 사용하여 ATA 센터를 업데이트합니다.

**구문**:

    "Microsoft ATA Center Setup.exe" [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]


**설치 옵션**:

> [!div class="mx-tableFixed"]
|Name|구문|자동 설치에 필수인가요?|설명|
|-------------|----------|---------|---------|
|Quiet|/quiet|예|UI 및 프롬프트를 표시하지 않고 설치 관리자를 실행합니다.|
|도움말|/help|아니요|도움말 및 빠른 참조를 제공합니다. 모든 옵션 및 동작 목록을 포함하여 설정 명령에 대한 올바른 사용법을 보여줍니다.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|예|.Net Framework 설치를 위한 매개 변수를 지정합니다. .Net Framework 자동 설치를 적용하도록 설정해야 합니다.|


ATA를 업데이트할 때 설치 관리자가 서버에 ATA가 이미 설치되어 있는지 자동으로 검색하며, 업데이트 설치 옵션은 필요하지 않습니다.

**예**: ATA 센터를 자동으로 업데이트하려면 다음을 수행합니다. 대규모 환경에서는 ATA 센터 업데이트를 완료하는 데 시간이 걸릴 수 있습니다. ATA 로그를 모니터링하여 업데이트 진행 상태를 추적합니다.

        "Microsoft ATA Center Setup.exe" /quiet NetFrameworkCommandLineArguments="/q"

## <a name="uninstall-the-ata-center-silently"></a>ATA 센터 자동 제거

ATA 센터 자동 제거를 수행하려면 다음 명령을 사용합니다. **구문**:

    Microsoft ATA Center Setup.exe [/quiet] [/Uninstall] [/Help]
     [--DeleteExistingDatabaseData]

**설치 옵션**:

> [!div class="mx-tableFixed"]
|Name|구문|자동 제거에 필수입니까?|설명|
|-------------|----------|---------|---------|
|Quiet|/quiet|예|UI 및 프롬프트를 표시하지 않고 제거 프로그램을 실행합니다.|
|제거|/uninstall|예|서버에서 ATA 센터 자동 제거를 실행합니다.|
|도움말|/help|아니요|도움말 및 빠른 참조를 제공합니다. 모든 옵션 및 동작 목록을 포함하여 설정 명령에 대한 올바른 사용법을 보여줍니다.|

**설치 매개 변수**:

> [!div class="mx-tableFixed"]
|Name|구문|자동 제거에 필수입니까?|설명|
|-------------|----------|---------|---------|
|DeleteExistingDatabaseData|DeleteExistingDatabaseData|아니요|기존 데이터베이스에 있는 모든 파일을 삭제합니다.|

**예**: 서버에서 ATA 센터를 자동으로 제거하기 위해 다음과 같이 기존 데이터베이스의 모든 데이터를 제거합니다.


    "Microsoft ATA Center Setup.exe" /quiet /uninstall --DeleteExistingDatabaseData

## <a name="ata-gateway-silent-installation"></a>ATA 게이트웨이 자동 설치

> [!NOTE]
> System Center Configuration Manager 또는 다른 소프트웨어 배포 시스템을 통해 ATA 경량 게이트웨이를 자동으로 배포하는 경우 두 개의 배포 패키지를 만드는 것이 좋습니다.</br>- Net Framework 4.6.1(도메인 컨트롤러 다시 부팅 포함)</br>- ATA 게이트웨이. </br>ATA 게이트웨이 패키지가 .Net Framework 패키지 배포에 종속되도록 설정합니다. </br>[.Net Framework 4.6.1 오프라인 배포 패키지](https://www.microsoft.com/download/details.aspx?id=49982)를 다운로드합니다. 


다음 명령을 사용하여 ATA 게이트웨이를 자동으로 설치합니다.

**구문**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/Help] [NetFrameworkCommandLineArguments ="/q"] 
    [ConsoleAccountName="<AccountName>"] 
    [ConsoleAccountPassword="<AccountPassword>"]

> [!NOTE]
> 도메인에 연결된 컴퓨터에서 작업 중이며 ATA 관리자 사용자 이름 및 암호를 사용하여 로그인한 경우에는 여기서 자격 증명을 제공할 필요가 없습니다.


**설치 옵션**:

> [!div class="mx-tableFixed"]
|Name|구문|자동 설치에 필수인가요?|설명|
|-------------|----------|---------|---------|
|Quiet|/quiet|예|UI 및 프롬프트를 표시하지 않고 설치 관리자를 실행합니다.|
|도움말|/help|아니요|도움말 및 빠른 참조를 제공합니다. 모든 옵션 및 동작 목록을 포함하여 설정 명령에 대한 올바른 사용법을 보여줍니다.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|예|.Net Framework 설치를 위한 매개 변수를 지정합니다. .Net Framework 자동 설치를 적용하도록 설정해야 합니다.|

**설치 매개 변수**:

> [!div class="mx-tableFixed"]
|Name|구문|자동 설치에 필수인가요?|설명|
|-------------|----------|---------|---------|
|ConsoleAccountName|ConsoleAccountName="<AccountName>"|예|ATA 센터에 ATA 게이트웨이를 등록하는 데 사용되는 사용자 계정(user@domain.com)의 이름을 설정합니다.|
|ConsoleAccountPassword|ConsoleAccountPassword="<AccountPassword>"|예|ATA 센터에 ATA 게이트웨이를 등록하는 데 사용되는 사용자 계정(user@domain.com)의 암호를 설정합니다.|

**예제**: ATA 게이트웨이를 자동으로 설치하려면 ATA 관리자 자격 증명을 사용하여 도메인에 연결된 컴퓨터에 로그인합니다. 그렇게 하면 설치의 일부로 자격 증명을 지정할 필요가 없습니다. 그렇지 않으면 지정된 자격 증명을 사용하여 ATA 센터에 등록합니다.

    "Microsoft ATA Gateway Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" 
    ConsoleAccountName="user@contoso.com" ConsoleAccountPassword="userpwd"
    

## <a name="update-the-ata-gateway"></a>ATA 게이트웨이 업데이트

다음 명령을 사용하여 ATA 게이트웨이를 자동으로 업데이트합니다.

**구문**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]


**설치 옵션**:

> [!div class="mx-tableFixed"]
|Name|구문|자동 설치에 필수인가요?|설명|
|-------------|----------|---------|---------|
|Quiet|/quiet|예|UI 및 프롬프트를 표시하지 않고 설치 관리자를 실행합니다.|
|도움말|/help|아니요|도움말 및 빠른 참조를 제공합니다. 모든 옵션 및 동작 목록을 포함하여 설정 명령에 대한 올바른 사용법을 보여줍니다.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|예|.Net Framework 설치를 위한 매개 변수를 지정합니다. .Net Framework 자동 설치를 적용하도록 설정해야 합니다.|


**예**: ATA 게이트웨이를 자동으로 업데이트하려면 다음을 수행합니다.

        Microsoft ATA Gateway Setup.exe /quiet NetFrameworkCommandLineArguments="/q"

## <a name="uninstall-the-ata-gateway-silently"></a>ATA 게이트웨이 자동 제거

ATA 게이트웨이 자동 제거를 수행하려면 다음 명령을 사용합니다. **구문**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/Uninstall] [/Help]
    
**설치 옵션**:

> [!div class="mx-tableFixed"]
|Name|구문|자동 제거에 필수입니까?|설명|
|-------------|----------|---------|---------|
|Quiet|/quiet|예|UI 및 프롬프트를 표시하지 않고 제거 프로그램을 실행합니다.|
|제거|/uninstall|예|서버에서 ATA 게이트웨이 자동 제거를 실행합니다.|
|도움말|/help|아니요|도움말 및 빠른 참조를 제공합니다. 모든 옵션 및 동작 목록을 포함하여 설정 명령에 대한 올바른 사용법을 보여줍니다.|

**예**: 서버에서 ATA 게이트웨이를 자동으로 제거하려면 다음을 수행합니다.


    Microsoft ATA Gateway Setup.exe /quiet /uninstall
    









## <a name="see-also"></a>참고 항목

- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [이벤트 수집 구성](configure-event-collection.md)
- [ATA 필수 구성 요소](ata-prerequisites.md)