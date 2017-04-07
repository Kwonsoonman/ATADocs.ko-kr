---
title: "Advanced Threat Analytics 자동 설치 | Microsoft 문서"
description: "ATA를 자동으로 설치하는 방법을 설명합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 02/19/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 5b58a8ec2f2fc1fe08e2b1099c3e9eda2f6d4c49
ms.sourcegitcommit: 49e892a82275efa5146998764e850959f20d3216
translationtype: HT
---
*적용 대상: Advanced Threat Analytics 버전 1.7*



# <a name="ata-silent-installation"></a>ATA 자동 설치
이 문서에는 ATA 자동 설치에 대한 지침이 있습니다.
## <a name="prerequisites"></a>필수 구성 요소

Microsoft ATA v1.7을 사용하려면 Microsoft .NET Framework 4.6.1이 설치되어 있어야 합니다. 

ATA를 설치하거나 업데이트하면 Microsoft ATA 배포의 일부로 .Net Framework 4.6.1이 자동으로 설치됩니다.

> [!Note] 
> .NET framework 4.6.1을 설치하려면 서버를 다시 부팅해야 할 수 있습니다. 도메인 컨트롤러에서 ATA 게이트웨이를 설치할 때 해당 도메인 컨트롤러에 대해 유지 관리 기간을 예약하는 것이 좋습니다.
ATA 자동 설치 방법을 사용하는 경우 설치가 끝나면 서버를 자동으로 다시 시작하도록 설치 관리자가 구성됩니다(필요한 경우). 설치의 일부로 서버를 다시 시작하는 것을 방지하려면 `-NoRestart` 플래그를 사용합니다. `-NoRestart` 플래그를 사용하면 설치의 일부로 다시 시작해야 하는 경우 서버가 다시 시작될 때까지 설치 관리자가 일시 중지됩니다. 배포 진행 상태를 추적하려면 **%AppData%\Local\Temp**에 있는 ATA 설치 관리자 로그를 모니터링합니다.


## <a name="install-the-ata-center"></a>ATA 센터를 설치합니다.

다음 명령을 사용하여 ATA 센터를 설치합니다.

**구문**:

    "Microsoft ATA Center Setup.exe" [/quiet] [/NoRestart] [/Help] [--LicenseAccepted] [NetFrameworkCommandLineArguments="/q"] [InstallationPath="<InstallPath>"] [DatabaseDataPath= "<DBPath>"] [CenterIpAddress=<CenterIPAddress>] [CenterPort=<CenterPort>] [CenterCertificateThumbprint="<CertThumbprint>"] 
    [ConsoleIpAddress=<ConsoleIPAddress>] [ConsoleCertificateThumbprint="<CertThumbprint >"]
    
**설치 옵션**:

|Name|구문|자동 설치에 필수인가요?|설명|
|-------------|----------|---------|---------|
|Quiet|/quiet|예|UI 및 프롬프트를 표시하지 않고 설치 관리자를 실행합니다.|
|NoRestart|/norestart|아니요|다시 시작하지 않습니다. 기본적으로 다시 시작하기 전에 UI가 표시됩니다.|
|도움말|/help|아니요|도움말 및 빠른 참조를 제공합니다. 모든 옵션 및 동작 목록을 포함하여 설정 명령에 대한 올바른 사용법을 보여줍니다.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|예|.Net Framework 설치를 위한 매개 변수를 지정합니다. .Net Framework 자동 설치를 적용하도록 설정해야 합니다.|
|LicenseAccepted|--LicenseAccepted|예|라이선스를 읽고 승인했는지를 나타냅니다. 자동 설치에 설정되어 있어야 합니다.|

**설치 매개 변수**:

|Name|구문|자동 설치에 필수인가요?|설명|
|-------------|----------|---------|---------|
|InstallationPath|InstallationPath="<InstallPath>"|아니요|ATA 이진 파일을 설치할 경로를 설정합니다. 기본 경로는 C:\Program Files\Microsoft Advanced Threat Analytics\Center입니다.|
|DatabaseDataPath|DatabaseDataPath= “<DBPath>”|아니요|ATA 데이터베이스 데이터 폴더 경로를 설정합니다. 기본 경로는 C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data입니다.|
|CenterIpAddress|CenterIpAddress=<CenterIPAddress>|예|ATA 센터 서비스의 IP 주소를 설정합니다.|
|CenterPort|CenterPort=<CenterPort>|예|ATA 센터 서비스의 네트워크 포트를 설정합니다.|
|CenterCertificateThumbprint|CenterCertificateThumbprint="<CertThumbprint>"|아니요|ATA 센터 서비스에 대한 인증서 지문을 설정합니다. 이 인증서는 ATA 센터와 ATA 게이트웨이 간 보안 통신에 사용됩니다. 설정하지 않으면 설치할 때 자체 서명된 인증서가 생성됩니다.|
|ConsoleIpAddress|ConsoleIpAddress=<ConsoleIPAddress>|예|ATA 콘솔의 IP 주소를 설정합니다.|
|ConsoleCertificateThumbprint|ConsoleCertificateThumbprint="<CertThumbprint >"|아니요|ATA 콘솔용 인증서 지문을 지정합니다. 이 인증서는 ATA 콘솔 웹 사이트의 ID를 확인하는 데 사용됩니다. 지정하지 않으면 설치할 때 자체 서명된 인증서가 생성됩니다.|

**예**: 기본 설치 경로 및 단일 IP 주소를 사용하여 ATA 센터를 설치하려면 다음을 수행합니다.

    "Microsoft ATA Center Setup.exe" /quiet --LicenseAccepted NetFrameworkCommandLineArguments="/q" CenterIpAddress=192.168.0.10
    CenterPort=444 ConsoleIpAddress=192.168.0.10

기본 설치 경로, 두 개의 IP 주소, 사용자 정의 인증서 지문을 사용하여 ATA 센터를 설치하려면 다음을 수행합니다.

    "Microsoft ATA Center Setup.exe" /quiet --LicenseAccepted NetFrameworkCommandLineArguments ="/q" CenterIpAddress=192.168.0.10 CenterPort=443 CenterCertificateThumbprint= ‎"1E2079739F624148ABDF502BF9C799FCB8C7212F"
    ConsoleIpAddress=192.168.0.11  ConsoleCertificateThumbprint="G9530253C976BFA9342FD1A716C0EC94207BFD5A"

## <a name="update-the-ata-center"></a>ATA 센터를 업데이트합니다.

다음 명령을 사용하여 ATA 센터를 업데이트합니다.

**구문**:

    "Microsoft ATA Center Setup.exe" [/quiet] [-NoRestart] /Help] [NetFrameworkCommandLineArguments="/q"]


**설치 옵션**:

|Name|구문|자동 설치에 필수인가요?|설명|
|-------------|----------|---------|---------|
|Quiet|/quiet|예|UI 및 프롬프트를 표시하지 않고 설치 관리자를 실행합니다.|
|NoRestart|/norestart|아니요|다시 시작하지 않습니다. 기본적으로 다시 시작하기 전에 UI가 표시됩니다.|
|도움말|/help|아니요|도움말 및 빠른 참조를 제공합니다. 모든 옵션 및 동작 목록을 포함하여 설정 명령에 대한 올바른 사용법을 보여줍니다.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|예|.Net Framework 설치를 위한 매개 변수를 지정합니다. .Net Framework 자동 설치를 적용하도록 설정해야 합니다.|


ATA를 업데이트할 때 설치 관리자가 서버에 ATA가 이미 설치되어 있는지 자동으로 검색하며, 업데이트 설치 옵션은 필요하지 않습니다.

**예**: ATA 센터를 자동으로 업데이트하려면 다음을 수행합니다. 대규모 환경에서는 ATA 센터 업데이트를 완료하는 데 시간이 걸릴 수 있습니다. ATA 로그를 모니터링하여 업데이트 진행 상태를 추적합니다.

        "Microsoft ATA Center Setup.exe" /quiet NetFrameworkCommandLineArguments="/q"

## <a name="uninstall-the-ata-center-silently"></a>ATA 센터 자동 제거

ATA 센터 자동 제거를 수행하려면 다음 명령을 사용합니다. **구문**:

    Microsoft ATA Center Setup.exe [/quiet] [/Uninstall] [/NoRestart] [/Help]
     [--DeleteExistingDatabaseData]

**설치 옵션**:

|Name|구문|자동 제거에 필수입니까?|설명|
|-------------|----------|---------|---------|
|Quiet|/quiet|예|UI 및 프롬프트를 표시하지 않고 제거 프로그램을 실행합니다.|
|제거|/uninstall|예|서버에서 ATA 센터 자동 제거를 실행합니다.|
|NoRestart|/norestart|아니요|다시 시작하지 않습니다. 기본적으로 다시 시작하기 전에 UI가 표시됩니다.|
|도움말|/help|아니요|도움말 및 빠른 참조를 제공합니다. 모든 옵션 및 동작 목록을 포함하여 설정 명령에 대한 올바른 사용법을 보여줍니다.|

**설치 매개 변수**:

|Name|구문|자동 제거에 필수입니까?|설명|
|-------------|----------|---------|---------|
|DeleteExistingDatabaseData|DeleteExistingDatabaseData|아니요|기존 데이터베이스에 있는 모든 파일을 삭제합니다.|

**예**: 서버에서 ATA 센터를 자동으로 제거하기 위해 다음과 같이 기존 데이터베이스의 모든 데이터를 제거합니다.


    "Microsoft ATA Center Setup.exe" /quiet /uninstall --DeleteExistingDatabaseData

## <a name="ata-gateway-silent-installation"></a>ATA 게이트웨이 자동 설치
다음 명령을 사용하여 ATA 게이트웨이를 자동으로 설치합니다.

**구문**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/NoRestart] [/Help] [NetFrameworkCommandLineArguments ="/q"] 
    [GatewayCertificateThumbprint="<CertThumbprint >"] [ConsoleAccountName="<AccountName>"] 
    [ConsoleAccountPassword="<AccountPassword>"]

**설치 옵션**:

|Name|구문|자동 설치에 필수인가요?|설명|
|-------------|----------|---------|---------|
|Quiet|/quiet|예|UI 및 프롬프트를 표시하지 않고 설치 관리자를 실행합니다.|
|NoRestart|/norestart|아니요|다시 시작하지 않습니다. 기본적으로 다시 시작하기 전에 UI가 표시됩니다.|
|도움말|/help|아니요|도움말 및 빠른 참조를 제공합니다. 모든 옵션 및 동작 목록을 포함하여 설정 명령에 대한 올바른 사용법을 보여줍니다.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|예|.Net Framework 설치를 위한 매개 변수를 지정합니다. .Net Framework 자동 설치를 적용하도록 설정해야 합니다.|

**설치 매개 변수**:

|Name|구문|자동 설치에 필수인가요?|설명|
|-------------|----------|---------|---------|
|GatewayCertificateThumbprint|GatewayCertificateThumbprint="<CertThumbprint >"|아니요|ATA 센터 서비스에 대한 인증서 지문을 설정합니다. 이 인증서는 ATA 센터와 ATA 게이트웨이 간 보안 통신에 사용됩니다. 설정하지 않으면 설치할 때 자체 서명된 인증서가 생성됩니다.|
|ConsoleAccountName|ConsoleAccountName="<AccountName>"|예|ATA 센터에 ATA 게이트웨이를 등록하는 데 사용되는 사용자 계정(user@domain.com)의 이름을 설정합니다.|
|ConsoleAccountPassword|ConsoleAccountPassword="<AccountPassword>"|예|ATA 센터에 ATA 게이트웨이를 등록하는 데 사용되는 사용자 계정(user@domain.com)의 암호를 설정합니다.|

**예**: 자동으로 ATA 게이트웨이를 설치하고 지정된 자격 증명을 사용하여 ATA 센터에 등록하려면 다음을 수행합니다.

    "Microsoft ATA Gateway Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" 
    ConsoleAccountName="user@contoso.com" ConsoleAccountPassword="userpwd"
    

## <a name="update-the-ata-gateway"></a>ATA 게이트웨이 업데이트

다음 명령을 사용하여 ATA 게이트웨이를 자동으로 업데이트합니다.

**구문**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/NoRestart] /Help] [NetFrameworkCommandLineArguments="/q"]


**설치 옵션**:

|Name|구문|자동 설치에 필수인가요?|설명|
|-------------|----------|---------|---------|
|Quiet|/quiet|예|UI 및 프롬프트를 표시하지 않고 설치 관리자를 실행합니다.|
|NoRestart|/norestart|아니요|다시 시작하지 않습니다. 기본적으로 다시 시작하기 전에 UI가 표시됩니다.|
|도움말|/help|아니요|도움말 및 빠른 참조를 제공합니다. 모든 옵션 및 동작 목록을 포함하여 설정 명령에 대한 올바른 사용법을 보여줍니다.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|예|.Net Framework 설치를 위한 매개 변수를 지정합니다. .Net Framework 자동 설치를 적용하도록 설정해야 합니다.|


**예**: ATA 게이트웨이를 자동으로 업데이트하려면 다음을 수행합니다.

        Microsoft ATA Gateway Setup.exe /quiet NetFrameworkCommandLineArguments="/q"

## <a name="uninstall-the-ata-gateway-silently"></a>ATA 게이트웨이 자동 제거

ATA 게이트웨이 자동 제거를 수행하려면 다음 명령을 사용합니다. **구문**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/Uninstall] [/NoRestart] [/Help]
    
**설치 옵션**:

|Name|구문|자동 제거에 필수입니까?|설명|
|-------------|----------|---------|---------|
|Quiet|/quiet|예|UI 및 프롬프트를 표시하지 않고 제거 프로그램을 실행합니다.|
|제거|/uninstall|예|서버에서 ATA 게이트웨이 자동 제거를 실행합니다.|
|NoRestart|/norestart|아니요|다시 시작하지 않습니다. 기본적으로 다시 시작하기 전에 UI가 표시됩니다.|
|도움말|/help|아니요|도움말 및 빠른 참조를 제공합니다. 모든 옵션 및 동작 목록을 포함하여 설정 명령에 대한 올바른 사용법을 보여줍니다.|

**예**: 서버에서 ATA 게이트웨이를 자동으로 제거하려면 다음을 수행합니다.


    Microsoft ATA Gateway Setup.exe /quiet /uninstall
    









## <a name="see-also"></a>참고 항목

- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [이벤트 수집 구성](configure-event-collection.md)
- [ATA 필수 구성 요소](/advanced-threat-analytics/plan-design/ata-prerequisites)