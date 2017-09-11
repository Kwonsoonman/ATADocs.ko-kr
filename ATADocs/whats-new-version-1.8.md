---
title: "ATA 버전 1.8의 새로운 기능 | Microsoft Docs"
description: "알려진 문제와 함께 ATA 버전 1.8의 새로운 기능을 나열합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 9/03/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 9592d413-df0e-4cec-8e03-be1ae00ba5dc
ms.reviewer: 
ms.suite: ems
ms.openlocfilehash: 2793a602a0cd0fb9902197acd45dd5bdd4612ea4
ms.sourcegitcommit: 654500928025e3cb127e095c17cc1d6444defd3a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/03/2017
---
# <a name="whats-new-in-ata-version-18"></a>ATA 버전 1.8의 새로운 기능

ATA의 최신 업데이트 버전은 [다운로드 센터에서 다운로드](https://www.microsoft.com/download/details.aspx?id=55536)할 수 있으며 전체 버전은 [Eval 센터](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics)에서 다운로드할 수 있습니다.

이 릴리스 정보에서는 이 Advanced Threat Analytics 버전의 업데이트, 새로운 기능, 버그 수정 및 알려진 문제에 대한 정보를 제공합니다.



## <a name="new--updated-detections"></a>새롭거나 업데이트된 검색 기능

- 비정상적인 프로토콜 구현이 WannaCry 맬웨어를 검색하도록 향상되었습니다.

- 새 기능! **중요한 그룹의 비정상적인 수정** – 권한 상승 단계의 일부로 공격자가 중요한 리소스에 대한 액세스 권한을 얻기 위해 높은 권한을 가진 그룹을 수정합니다. 이제 ATA가 관리자 권한 그룹에 비정상적인 변경이 있을 경우 이를 검색합니다.
- 새 기능! **의심스러운 인증 실패**(동작 무차별 암호 대입(Brute force)) – 공격자가 자격 증명에 무차별 암호 대입(Brute force)을 사용하여 계정을 손상하려고 합니다. 이제 비정상적인 인증 실패 동작이 검색되면 ATA에서 경고가 발생합니다.   

- **원격 실행 시도 - WMI 실행** - 공격자는 도메인 컨트롤러에서 원격으로 코드를 실행하여 네트워크를 제어하려고 시도할 수 있습니다. ATA에서 원격으로 코드를 실행하는 WMI 메서드 검색을 포함하도록 원격 실행 검색 기능이 향상되었습니다.

- 디렉터리 서비스 쿼리를 사용한 정찰 – 이 검색은 하나의 중요한 엔터티에 대한 쿼리를 catch하고 이전 버전에서 생성된 거짓 긍정 수를 줄일 수 있도록 향상되었습니다. 버전 1.7에서 이 기능을 사용하지 않도록 설정한 경우 버전 1.8을 설치하면 이제 자동으로 사용됩니다.

- Kerberos 골든 티켓 활동 - ATA 1.8에는 골든 티켓 공격을 검색하는 추가 기술이 포함되어 있습니다.
    - 이제 ATA가 골든 티켓 수명이 만료된 의심스러운 활동을 검색합니다. Kerberos 티켓이 허용된 수명보다 오래 사용되면 ATA는 골든 티켓이 생성되었을 가능성이 있는 의심스러운 활동으로 검색합니다.
- 알려진 거짓 긍정을 제거하기 위해 다음 검색이 향상되었습니다.  
    - 권한 상승 검색(위조된 PAC) 
    - 암호화 다운그레이드 활동(스켈레톤 키)
    - 비정상적인 프로토콜 구현
    - 손상된 신뢰

## <a name="improved-triage-of-suspicious-activities"></a>의심스러운 활동의 향상된 심사

-   새 기능! ATA 1.8에서는 심사 프로세스 중 의심스러운 활동에 대해 다음과 같은 작업을 실행할 수 있습니다. 
    - **엔터티 제외** - ATA에서 원격 코드를 실행하는 관리자, 보안 스캐너 검색 등 무해한 참 긍정을 검색할 때 경고하지 않도록 향후 의심스러운 활동 발생에서 엔터티를 제외합니다.
    - **반복 표시 안 함** - 의심스러운 활동에 대한 경고가 반복해서 표시되지 않도록 합니다.
    - **의심스러운 활동 삭제** - 공격 타임라인에서 의심스러운 활동을 삭제합니다.
-   이제 의심스러운 활동 경고에 대한 후속 작업 프로세스가 더 효율적입니다. 의심스러운 활동 타임라인이 다시 설계되었습니다. ATA 1.8에서는 단일 화면에 더 많은 의심스러운 활동을 표시하고, 심사 및 조사를 위해 더 나은 정보를 포함할 수 있습니다. 

## <a name="new-reports-to-help-you-investigate"></a>조사에 도움이 되는 새로운 보고서 
-   새 기능! 의심스러운 활동, 상태 문제 등을 포함하여 ATA에서 요약된 모든 데이터를 볼 수 있도록 **요약 보고서**가 추가되었습니다. 반복해서 자동으로 생성되는 사용자 지정 보고서를 정의할 수도 있습니다.
-   새 기능! 특정 기간 동안 중요한 그룹에서 변경된 모든 내용을 볼 수 있도록 **중요한 그룹 보고서**가 추가되었습니다.


## <a name="infrastructure-improvements"></a>인프라 향상

-   ATA 센터 성능이 향상되었습니다. ATA 1.8에서는 ATA 센터가 초당 1M 이상의 패킷을 처리할 수 있습니다.
-   이제 ATA 경량 게이트웨이가 이벤트 전달을 구성하지 않고도 로컬에서 이벤트를 읽을 수 있습니다.
-   이제 모니터링 경고 및 의심스러운 활동에 대해 별도로 메일을 구성할 수 있습니다.

## <a name="security-improvements"></a>향상된 보안 기능

-   새 기능! **ATA 관리에 대한 Single Sign-On**. ATA는 Windows 인증과 통합된 Single Sign-On을 지원합니다. 컴퓨터에 이미 로그온되어 있으면 ATA는 해당 토큰을 사용하여 ATA 콘솔에 로그인합니다. 스마트 카드를 사용하여 로그인할 수도 있습니다. ATA 게이트웨이 및 ATA 경량 게이트웨이에 대한 자동 설치 스크립트에서 이제 자격 증명을 제공할 필요 없이 로그온한 사용자의 컨텍스트를 사용합니다.
-   로컬 시스템 권한이 ATA 게이트웨이 프로세스에서 제거되었으므로 이제 가상 계정(독립 실행형 ATA 게이트웨이에서만 사용 가능), 관리 서비스 계정 및 그룹 관리 서비스 계정을 사용하여 ATA 게이트웨이 프로세스를 실행할 수 있습니다.   
-   ATA 센터 및 게이트웨이에 대한 감사 로그가 추가되었으며, 이제 모든 작업이 Windows 이벤트 로그에 기록됩니다.
-   ATA 센터에 대한 KSP 인증서 지원이 추가되었습니다.

## <a name="additional-changes"></a>추가 변경 사항

- 설명 추가 옵션이 의심스러운 활동에서 제거되었습니다.
- 의심스러운 활동 완화에 대한 권장 사항이 의심스러운 활동 타임라인에서 제거되었습니다.
- ATA 버전 1.8부터는 ATA 게이트웨이 및 경량 게이트웨이가 자체 인증서를 관리하고 이를 관리하기 위해 관리자 상호 작용이 필요하지 않습니다.

## <a name="known-issues"></a>알려진 문제

> [!WARNING]
> 이러한 알려진 문제를 방지하려면 1.8 업데이트 1을 사용하여 배포하거나 업데이트하세요.

### <a name="ata-gateway-on-windows-server-core"></a>Windows Server Core의 ATA 게이트웨이

**증상**: .Net framework 4.7이 포함된 Windows Server 2012R2에서 ATA 게이트웨이를 1.8로 업그레이드하면 실패하고 *Microsoft Advanced Threat Analytics Gateway has stopped working*\(Microsoft Advanced Threat Analytics 게이트웨이의 작동이 중지되었습니다.\) 오류가 표시됩니다. 

![게이트웨이 코어 오류](./media/gateway-core-error.png)

Windows Server 2016 Core에서는 오류가 표시되지 않을 수 있지만 설치할 때 프로세스가 실패하고 1000 및 1001(프로세스 크래시) 이벤트가 서버의 응용 프로그램 이벤트 로그에 기록됩니다.

**설명**: .NET framework 4.7에서는 WPF 기술(예: ATA)을 사용하는 응용 프로그램이 로드되지 않는 문제가 발생합니다. 자세한 내용은 [KB 4034015를 참조](https://support.microsoft.com/help/4034015/wpf-window-can-t-be-loaded-after-you-install-the-net-framework-4-7-on)하세요. 

**해결 방법**: .Net 4.7 제거. [KB 3186497을 참조](https://support.microsoft.com/help/3186497/the-net-framework-4-7-offline-installer-for-windows)하여 .NET 버전을 .NET 4.6.2로 되돌린 다음 ATA 게이트웨이를 1.8 버전으로 업데이트합니다. ATA를 업그레이드한 후 .NET 4.7을 다시 설치할 수 있습니다.  향후 릴리스에서는 이 문제를 해결하는 업데이트가 제공됩니다.

### <a name="lightweight-gateway-event-log-permissions"></a>경량 게이트웨이 이벤트 로그 사용 권한

**증상**: ATA 버전 1.8로 업그레이드하는 경우 이전에 보안 이벤트 로그에 액세스할 수 있는 권한이 부여된 앱 또는 서비스의 권한이 손실될 수 있습니다. 

**설명**: ATA를 더 쉽게 배포할 수 있도록 ATA 1.8에서는 보안 이벤트 로그에 직접 액세스하므로 Windows 이벤트 전달을 구성할 필요가 없습니다. 동시에 ATA는 낮은 권한의 로컬 서비스로 실행되어 더욱 강화된 보안을 유지합니다. ATA가 이벤트를 읽을 수 있는 액세스 권한을 제공하기 위해 ATA 서비스는 자신에게 보안 이벤트 로그에 대한 사용 권한을 부여합니다. 이 경우 다른 서비스에 대해 이전에 설정된 사용 권한을 사용할 수 없게 될 수 있습니다.

**해결 방법**: 다음 Windows PowerShell 스크립트를 실행합니다. 그러면 잘못 추가된 사용 권한이 ATA의 레지스트리에서 제거되고 다른 API를 통해 추가됩니다. 따라서 다른 앱의 사용 권한이 복원될 수 있습니다. 복원되지 않으면 수동으로 복원해야 합니다. 향후 릴리스에서는 이 문제를 해결하는 업데이트가 제공됩니다. 

       $ATADaclEntry = "(A;;0x1;;;S-1-5-80-1717699148-1527177629-2874996750-2971184233-2178472682)"
        try {
        $SecurityDescriptor = Get-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\Eventlog\Security -Name CustomSD
        $ATASddl = "O:BAG:SYD:" + $ATADaclEntry 
        if($SecurityDescriptor.CustomSD -eq $ATASddl) {
        Remove-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\Eventlog\Security -Name CustomSD
        }
    }
    catch
    {
    # registry key does not exist
    }

    $EventLogConfiguration = New-Object -TypeName System.Diagnostics.Eventing.Reader.EventLogConfiguration("Security")
    $EventLogConfiguration.SecurityDescriptor = $EventLogConfiguration.SecurityDescriptor + $ATADaclEntry

### <a name="proxy-interference"></a>프록시 간섭

**증상**: ATA 1.8로 업그레이드한 후 ATA 게이트웨이 서비스가 시작되지 않을 수 있습니다. ATA 오류 로그에 *System.Net.Http.HttpRequestException: 요청을 보내는 동안 오류가 발생했습니다. ---> System.Net.WebException: 원격 서버에 오류가 반환되었습니다. (407) 프록시 인증이 필요합니다.*라는 예외가 표시될 수 있습니다.

**설명**: ATA 1.8부터 ATA 게이트웨이는 HTTP 프로토콜을 사용하여 ATA 센터와 통신합니다. ATA 게이트웨이를 설치한 컴퓨터가 프록시 서버를 사용하여 ATA 센터에 연결된 경우 이 통신이 중단될 수 있습니다. 

**해결 방법**: ATA 게이트웨이 서비스 계정에서 프록시 서버를 사용하지 않도록 설정합니다. 향후 릴리스에서는 이 문제를 해결하는 업데이트가 제공됩니다.

### <a name="report-settings-reset"></a>보고서 설정 다시 설정

**증상**: 1.8 업데이트 1로 업데이트하면 예약된 보고서에 대한 모든 설정이 지워집니다.

**설명**: 1.8에서 1.8 업데이트 1로 업데이트하면 보고서 일정 설정이 다시 설정됩니다.

**해결 방법**: 1.8 업데이트 1로 업데이트하기 전에 보고서 설정의 복사본을 만들어 다시 입력합니다. 이는 스크립트를 통해 수행할 수도 있습니다. 자세한 내용은 [ATA 구성 내보내기 및 가져오기](ata-configuration-file.md)를 참조하세요.


## <a name="see-also"></a>참고 항목
[ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[버전 1.8로 ATA 업데이트 - 마이그레이션 가이드](ata-update-1.8-migration-guide.md)

