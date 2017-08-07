---
title: "Advanced Threat Analytics 필수 구성 요소 | Microsoft 문서"
description: "환경에서 ATA를 올바르게 배포하기 위한 요구 사항을 설명합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 8/2/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: a5f90544-1c70-4aff-8bf3-c59dd7abd687
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 0a9d92e5851f1cf64c5e4b4e1ee57d7ee4562d96
ms.sourcegitcommit: 7bc04eb4d004608764b3ded1febf32bc4ed020be
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/02/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*



# <a name="ata-prerequisites"></a>ATA 필수 구성 요소
이 문서에서는 환경에서 ATA를 올바르게 배포하기 위한 요구 사항을 설명합니다.

>[!NOTE]
> 리소스 및 용량을 계획하는 방법에 대한 자세한 내용은 [ATA 용량 계획](ata-capacity-planning.md)을 참조하세요.


ATA는 ATA 센터, ATA 게이트웨이 및/또는 ATA 경량 게이트웨이로 구성됩니다. ATA 구성 요소에 대한 자세한 내용은 [ATA 아키텍처](ata-architecture.md)를 참조하세요.

ATA 시스템은 Active Directory 포리스트 경계에서 작동하고 Windows 2003 이상에서 FFL(포리스트 기능 수준)을 지원합니다.


[시작하기 전에](#before-you-start): 이 섹션에서는 ATA 설치를 시작하기 전에 수집해야 하는 정보와 확인해야 하는 계정 및 네트워크 엔터티를 제시합니다.

[ATA 센터](#ata-center-requirements): 이 섹션에는 ATA 센터 하드웨어, 소프트웨어 요구 사항 및 ATA 센터 서버에서 구성해야 하는 설정에 대해 설명합니다.

[ATA 게이트웨이](#ata-gateway-requirements): 이 섹션에는 ATA 게이트웨이 하드웨어, 소프트웨어 요구 사항 및 ATA 게이트웨이 서버에서 구성해야 하는 설정에 대해 설명합니다.

[ATA 경량 게이트웨이](#ata-lightweight-gateway-requirements):이 섹션에는 ATA 경량 게이트웨이 하드웨어 및 소프트웨어 요구 사항이 나열되어 있습니다.

[ATA 콘솔](#ata-console): 이 섹션에서는 ATA 콘솔을 실행하기 위한 브라우저 요구 사항을 제시합니다.

![ATA 아키텍처 다이어그램](media/ATA-architecture-topology.jpg)

## <a name="before-you-start"></a>시작하기 전에
이 섹션에서는 ATA 설치를 시작하기 전에 수집해야 하는 정보와 확인해야 하는 계정 및 네트워크 엔터티를 제시합니다.


-   모니터링되는 도메인의 모든 개체에 대한 읽기 권한이 있는 사용자 계정 및 암호입니다.

    > [!NOTE]
    > 도메인의 여러 OU(조직 구성 단위)에서 사용자 지정 ACL을 설정한 경우에는 선택한 사용자에게 해당 OU에 대한 읽기 권한이 있는지 확인하세요.

-   ATA 게이트웨이 또는 경량 게이트웨이에 Microsoft Message Analyzer를 설치하지 마세요. Message Analyzer 드라이버는 ATA 게이트웨이 및 경량 게이트웨이 드라이버와 충돌합니다. ATA 게이트웨이에서 Wireshark를 실행하는 경우 Wireshark 캡처를 중지한 후 Microsoft Advanced Threat Analytics Gateway Service를 다시 시작해야 합니다. 그렇지 않으면 게이트웨이가 트래픽 캡처를 중지합니다. ATA 경량 게이트웨이에서 Wireshark를 실행해도 ATA 경량 게이트웨이에는 방해가 되지 않습니다.

-    권장: 사용자에게 삭제된 개체 컨테이너에 대한 읽기 전용 권한이 있어야 합니다. 그러면 ATA가 도메인에서 대량 개체 삭제를 검색할 수 있습니다. 삭제된 개체 컨테이너에 대해 읽기 전용 권한을 구성하는 방법에 대한 자세한 내용은 [디렉터리 개체에 대한 권한 보기 또는 설정](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx) 항목에서 **삭제된 개체 컨테이너에 대한 권한 변경** 섹션을 참조하세요.

-   선택 사항: 네트워크 활동이 없는 사용자 계정을 사용합니다. 이 계정은 ATA 허니토큰 사용자로 구성됩니다. 허니토큰 사용자를 구성하려면 사용자 이름이 아닌 사용자 계정의 SID가 필요합니다. 자세한 내용은 [ATA 검색 설정 작업](https://docs.microsoft.com/en-us/advanced-threat-analytics/deploy-use/working-with-detection-settings)을 참조하세요.

-   선택 사항: ATA는 도메인 컨트롤러에서 보내고 받는 네트워크 트래픽을 수집 및 분석할 수 있을 뿐 아니라 Windows 이벤트 4776, 4732, 4733, 4728, 4729, 4756 및 4757을 사용하여 ATA Pass-the-Hash, 무차별 암호 대입(Brute force), 중요한 그룹 수정 및 Honeytoken 검색 기능을 추가로 개선할 수 있습니다. 이러한 이벤트는 SIEM에서 수신될 수도 있고 도메인 컨트롤러에서 Windows 이벤트 전달을 설정하여 수신할 수도 있습니다. 수집된 이벤트는 도메인 컨트롤러 네트워크 트래픽을 통해서는 사용할 수 없는 추가 정보를 ATA에 제공합니다.


## <a name="ata-center-requirements"></a>ATA 센터 요구 사항
이 섹션에서는 ATA 센터의 요구 사항에 대해 설명합니다.
### <a name="general"></a>일반
ATA 센터는 Windows Server 2012 R2 또는 Windows Server 2016을 실행 중인 서버에 설치할 수 있습니다. ATA 센터는 도메인이나 작업 그룹의 구성원인 서버에 설치할 수 있습니다.

Windows Server 2012 R2를 실행 중인 ATA 센터를 설치하기 전에 [KB2919355](https://support.microsoft.com/kb/2919355/) 업데이트가 설치되었는지 확인합니다.

Windows PowerShell cmdlet `[Get-HotFix -Id kb2919355]`를 실행하여 이 업데이트가 설치되었는지를 확인할 수 있습니다.

ATA 센터를 가상 컴퓨터로 설치할 수 있습니다. 

>[!NOTE] 
> 가상 컴퓨터로 실행하는 경우 동적 메모리 또는 다른 메모리 풍선 알림 기능은 지원되지 않습니다.

ATA 센터를 가상 컴퓨터로 실행하는 경우 데이터베이스 손상 가능성을 방지하기 위해 새 검사점을 만들기 전에 서버를 종료합니다.
### <a name="server-specifications"></a>서버 사양
물리적 서버에서 작업할 때 ATA 데이터베이스를 사용하려면 BIOS에서 NUMA(Non-Uniform Memory Access)를 **사용하지 않도록 설정**해야 합니다. 시스템이 NUMA를 노드 인터리빙으로 참조할 수 있습니다. 이 경우 NUMA를 사용하지 않으려면 노드 인터리빙을 **사용하도록 설정**해야 합니다. 자세한 내용은 BIOS 설명서를 참조하세요. 이는 ATA 센터가 가상 서버에서 실행 중인 경우 관련이 없습니다.<br>
성능을 최적화하려면 ATA 센터의 **전원 옵션**을 **고성능**으로 설정합니다.<br>
모니터링 중인 도메인 컨트롤러 수와 각 도메인 컨트롤러의 로드에 따라 필요한 서버 사양이 결정됩니다. 자세한 내용은 [ATA 용량 계획](ata-capacity-planning.md)을 참조하세요.


### <a name="time-synchronization"></a>시간 동기화
ATA 센터 서버, ATA 게이트웨이 서버, 도메인 컨트롤러의 시간차가 5분 이상 나지 않도록 동기화해야 합니다.


### <a name="network-adapters"></a>네트워크 어댑터
다음이 필요합니다.
-   하나 이상의 네트워크 어댑터(VLAN 환경에서 물리적 서버를 사용할 경우 두 개의 네트워크 어댑터 사용 권장)

-   ATA 센터와 ATA 게이트웨이 간의 통신에 사용되는 IP 주소이며 포트 443에서 SSL을 사용하여 암호화됩니다. (ATA 서비스는 ATA 센터가 포트 443에 가지고 있는 모든 IP 주소에 바인딩됩니다.)

### <a name="ports"></a>포트
아래 표에는 ATA 센터가 정상적으로 작동하도록 하려면 열어야 하는 최소한의 포트가 나와 있습니다.

|프로토콜|전송|포트|끝/시작|방향|
|------------|-------------|--------|-----------|-------------|
|**SSL**(ATA 통신)|TCP|443 또는 구성 가능|ATA 게이트웨이|인바운드|
|**HTTP**(선택 사항)|TCP|80|회사 네트워크|인바운드|
|**HTTPS**|TCP|443|회사 네트워크 및 ATA 게이트웨이|인바운드|
|**SMTP**(선택 사항)|TCP|25|SMTP 서버|아웃바운드|
|**SMTPS**(선택 사항)|TCP|465|SMTP 서버|아웃바운드|
|**syslog**(선택 사항)|TCP|514|Syslog 서버|아웃바운드|
|**LDAP**|TCP 및 UDP|389|도메인 컨트롤러|아웃바운드|
|**LDAPS**(선택 사항)|TCP|636|도메인 컨트롤러|아웃바운드|
|**DNS**|TCP 및 UDP|53|DNS 서버|아웃바운드|
|**Kerberos**(도메인에 연결된 경우 선택 사항)|TCP 및 UDP|88|도메인 컨트롤러|아웃바운드|
|**Netlogon**(도메인에 연결된 경우 선택 사항)|TCP 및 UDP|445|도메인 컨트롤러|아웃바운드|
|**Windows 시간**(도메인에 연결된 경우 선택 사항)|UDP|123|도메인 컨트롤러|아웃바운드|

> [!NOTE]
> ATA 게이트웨이와 도메인 컨트롤러 간의 자격 증명을 테스트하려면 LDAP가 필요합니다. 이 테스트는 ATA 센터에서 도메인 컨트롤러로 수행되어 이러한 자격 증명의 유효성을 테스트하며, 이 테스트 이후에는 ATA 게이트웨이가 LDAP를 일반적인 통신의 일부로 사용합니다.


### <a name="certificates"></a>인증서
ATA 센터에 CRL 배포 지점 액세스 권한이 있는지 확인합니다. ATA 게이트웨이가 인터넷에 액세스할 수 없으면 [CRL을 수동으로 가져오는 절차](https://technet.microsoft.com/library/aa996972%28v=exchg.65%29.aspx)에 따라 전체 체인에 모든 CRL 배포 지점을 설치합니다.

ATA를 쉽게 설치하려면 설치하는 동안 자체 서명 인증서를 설치할 수 있습니다. 배포 후에는 자체 서명 인증서를 ATA 게이트웨이에 사용할 내부 인증 기관의 인증서로 바꿀 수 있습니다.<br>

> [!WARNING]
> - 기존 인증서의 갱신 프로세스가 지원되지 않습니다. 인증서를 갱신하는 방법은 새 인증서를 만들고 해당 인증서를 사용하도록 ATA를 구성하는 방법만이 유일합니다.


> [!NOTE]
> - 인증서의 공급자 형식은 CSP(암호화 서비스 공급자) 또는 KSP(키 저장소 공급자)일 수 있습니다.
> - ATA 센터 인증서는 갱신되지 않아야 합니다. 인증서가 만료되기 전에 인증서를 갱신하는 올바른 방법은 새 인증서를 만들고 해당 인증서를 선택하는 것입니다. 
> - 다른 컴퓨터에서 ATA 콘솔에 액세스하려는 경우 해당 컴퓨터가 ATA 센터에서 사용 중인 인증서를 신뢰하는지 확인해야 합니다. 그렇지 않으면 로그인 페이지가 표시되기 전에 웹 사이트 보안 인증서에 문제가 있다는 경고 페이지가 표시됩니다.

## <a name="ata-gateway-requirements"></a>ATA 게이트웨이 요구 사항
이 섹션에서는 ATA 게이트웨이의 요구 사항에 대해 설명합니다.
### <a name="general"></a>일반
ATA 게이트웨이는 Windows Server 2012 R2 또는 Windows Server 2016(서버 코어 포함)을 실행 중인 서버에 설치할 수 있습니다.
ATA 게이트웨이는 도메인이나 작업 그룹의 구성원인 서버에 설치할 수 있습니다.
ATA 게이트웨이를 사용하면 Windows 2003 이상의 도메인 기능 수준에서 도메인 컨트롤러를 모니터링할 수 있습니다.

Windows Server 2012 R2를 실행 중인 ATA 게이트웨이를 설치하기 전에 [KB2919355](https://support.microsoft.com/kb/2919355/) 업데이트가 설치되었는지 확인합니다.

Windows PowerShell cmdlet `[Get-HotFix -Id kb2919355]`를 실행하여 이 업데이트가 설치되었는지를 확인할 수 있습니다.


ATA 게이트웨이가 설치된 가상 컴퓨터를 사용하는 방법에 대한 자세한 내용은 [포트 미러링 구성](configure-port-mirroring.md)을 참조하세요.

> [!NOTE]
> 최소 5GB의 공간이 필요하며 10GB가 권장됩니다. 여기에는 ATA 이진 파일, [ATA 로그](troubleshooting-ata-using-logs.md) 및 [성능 로그](troubleshooting-ata-using-perf-counters.md)에 필요한 공간이 포함됩니다.

### <a name="server-specifications"></a>서버 사양
성능을 최적화하려면 ATA 게이트웨이의 **전원 옵션**을 **고성능**으로 설정합니다.<br>
도메인 컨트롤러에서 보내고 받는 네트워크 트래픽의 양에 따라 ATA 게이트웨이 하나가 여러 도메인 컨트롤러를 모니터링할 수 있습니다.

>[!NOTE] 
> 가상 컴퓨터로 실행하는 경우 동적 메모리 또는 다른 메모리 풍선 알림 기능은 지원되지 않습니다.

ATA 게이트웨이 하드웨어 요구 사항에 대한 자세한 내용은 [ATA 용량 계획](ata-capacity-planning.md)을 참조하세요.

### <a name="time-synchronization"></a>시간 동기화
ATA 센터 서버, ATA 게이트웨이 서버, 도메인 컨트롤러의 시간차가 5분 이상 나지 않도록 동기화해야 합니다.

### <a name="network-adapters"></a>네트워크 어댑터
ATA 게이트웨이를 사용하려면 관리 어댑터와 캡처 어댑터가 각각 하나 이상 필요합니다.

-   **관리 어댑터** - 회사 네트워크 통신에 사용됩니다. 다음 정보를 사용하여 이 어댑터를 구성해야 합니다.

    -   기본 게이트웨이를 포함하는 고정 IP 주소

    -   기본 설정 DNS 서버와 대체 DNS 서버

    -   **이 연결의 DNS 접미사**는 모니터링 중인 각 도메인의 도메인 DNS 이름이어야 합니다.

        ![고급 TCP/IP 설정에서 DNS 접미사 구성](media/ATA-DNS-Suffix.png)

        > [!NOTE]
        > ATA 게이트웨이가 도메인의 구성원이면 관리 어댑터는 자동으로 구성될 수 있습니다.

-   **캡처 어댑터** -도메인 컨트롤러에서 보내고 받는 트래픽을 캡처하는 데 사용됩니다.

    > [!IMPORTANT]
    > -   캡처 어댑터용 포트 미러링은 도메인 컨트롤러 네트워크 트래픽의 대상으로 구성합니다. 자세한 내용은 [포트 미러링 구성](configure-port-mirroring.md)을 참조하세요. 일반적으로는 네트워킹 또는 가상화 팀과 협의하여 포트 미러링을 구성해야 합니다.
    > -   기본 게이트웨이 및 DNS 서버 주소가 없는 라우팅 불가능 고정 IP 주소를 환경에 대해 구성합니다. 예를 들어 1.1.1.1/32와 같이 구성할 수 있습니다. 이렇게 하면 캡처 네트워크 어댑터가 트래픽을 최대한 캡처할 수 있으며, 관리 네트워크 어댑터를 사용하여 필요한 네트워크 트래픽을 보내고 받을 수 있습니다.

### <a name="ports"></a>포트
아래 표에는 관리 어댑터에 구성된 ATA 게이트웨이에 필요한 최소한의 포트가 나와 있습니다.

|프로토콜|전송|포트|끝/시작|Direction|
|------------|-------------|--------|-----------|-------------|
|LDAP|TCP 및 UDP|389|도메인 컨트롤러|아웃바운드|
|보안 LDAP(LDAPS)|TCP|636|도메인 컨트롤러|아웃바운드|
|글로벌 카탈로그에 대한 LDAP|TCP|3268|도메인 컨트롤러|아웃바운드|
|글로벌 카탈로그에 대한 LDAPS|TCP|3269|도메인 컨트롤러|아웃바운드|
|Kerberos|TCP 및 UDP|88|도메인 컨트롤러|아웃바운드|
|Netlogon|TCP 및 UDP|445|도메인 컨트롤러|아웃바운드|
|Windows 시간|UDP|123|도메인 컨트롤러|아웃바운드|
|DNS|TCP 및 UDP|53|DNS 서버|아웃바운드|
|NTLM over RPC|TCP|135|네트워크의 모든 장치|아웃바운드|
|NetBIOS|UDP|137|네트워크의 모든 장치|아웃바운드|
|SSL|TCP|443 또는 센터 서비스용으로 구성된 포트|ATA 센터:<br /><br />-   센터 서비스 IP 주소<br />-   콘솔 IP 주소|아웃바운드|
|syslog(선택 사항)|UDP|514|SIEM 서버|인바운드|

> [!NOTE]
> ATA 게이트웨이가 수행하는 확인 프로세스의 일부분으로 ATA 게이트웨이에서 네트워크의 장치에 대해 다음 포트를 인바운드로 열어야 합니다.
>
> -   NTLM over RPC(TCP 포트 135)
> -   NetBIOS(UDP 포트 137)

## <a name="ata-lightweight-gateway-requirements"></a>ATA 경량 게이트웨이 요구 사항
이 섹션에서는 ATA 경량 게이트웨이 요구 사항에 대해 설명합니다.
### <a name="general"></a>일반
ATA 경량 게이트웨이는 Windows Server 2008 R2 SP1(Server Core 제외), Windows Server 2012, Windows Server 2012 R2, Windows Server 2016(Core 포함, Nano 제외)을 실행하는 도메인 컨트롤러에 대한 설치를 지원합니다.

도메인 컨트롤러는 RODC(읽기 전용 도메인 컨트롤러)만 될 수 있습니다.

Windows Server 2012 R2를 실행하는 도메인 컨트롤러에 ATA 경량 게이트웨이를 설치하기 전에 [KB2919355](https://support.microsoft.com/kb/2919355/) 업데이트가 설치되었는지 확인합니다.

Windows PowerShell cmdlet `[Get-HotFix -Id kb2919355]`를 실행하여 이 업데이트가 설치되었는지를 확인할 수 있습니다.

Windows server 2012 R2 Server Core에 대한 설치의 경우 [KB3000850](https://support.microsoft.com/help/3000850/november-2014-update-rollup-for-windows-rt-8.1%2c-windows-8.1%2c-and-windows-server-2012-r2) 업데이트도 설치되어 있어야 합니다.

 Windows PowerShell cmdlet `[Get-HotFix -Id kb3000850]`을 실행하여 이 업데이트가 설치되었는지를 확인할 수 있습니다.


설치하는 동안 .Net Framework 4.6.1이 설치되고 도메인 컨트롤러가 다시 부팅되도록 할 수 있습니다.


> [!NOTE]
> 최소 5GB의 공간이 필요하며 10GB가 권장됩니다. 여기에는 ATA 이진 파일, [ATA 로그](troubleshooting-ata-using-logs.md) 및 [성능 로그](troubleshooting-ata-using-perf-counters.md)에 필요한 공간이 포함됩니다.

### <a name="server-specifications"></a>서버 사양

ATA 경량 게이트웨이는 도메인 컨트롤러에 최소 2개의 코어와 6GB의 RAM이 설치되어 있어야 합니다.
성능을 최적화하려면 ATA 경량 게이트웨이의 **전원 옵션**을 **고성능**으로 설정합니다.
ATA 경량 게이트웨이는 도메인 컨트롤러에서 들어오고 나가는 네트워크 트래픽 양과 해당 도메인 컨트롤러에 설치된 리소스 양에 따라 로드와 크기가 다양한 도메인 컨트롤러에 배포할 수 있습니다.

>[!NOTE] 
> 가상 컴퓨터로 실행하는 경우 동적 메모리 또는 다른 메모리 풍선 알림 기능은 지원되지 않습니다.

ATA 경량 게이트웨이 하드웨어 요구 사항에 대한 자세한 내용은 [ATA 용량 계획](ata-capacity-planning.md)을 참조하세요.

### <a name="time-synchronization"></a>시간 동기화
ATA 센터 서버, ATA 경량 게이트웨이 서버 및 도메인 컨트롤러의 시간차가 5분 이상 나지 않도록 동기화해야 합니다.
### <a name="network-adapters"></a>네트워크 어댑터
ATA 경량 게이트웨이는 모든 도메인 컨트롤러의 네트워크 어댑터에서 로컬 트래픽을 모니터링합니다. <br>
배포 후 모니터링되는 네트워크 어댑터를 수정하려면 ATA 콘솔을 사용하면 됩니다.

### <a name="ports"></a>포트
아래 표에는 ATA 경량 게이트웨이에 필요한 최소한의 포트가 나와 있습니다.

|프로토콜|전송|포트|끝/시작|방향|
|------------|-------------|--------|-----------|-------------|
|DNS|TCP 및 UDP|53|DNS 서버|아웃바운드|
|NTLM over RPC|TCP|135|네트워크의 모든 장치|아웃바운드|
|NetBIOS|UDP|137|네트워크의 모든 장치|아웃바운드|
|SSL|TCP|443 또는 센터 서비스용으로 구성된 포트|ATA 센터:<br /><br />-   센터 서비스 IP 주소<br />-   콘솔 IP 주소|아웃바운드|
|syslog(선택 사항)|UDP|514|SIEM 서버|인바운드|

> [!NOTE]
> ATA 경량 게이트웨이가 수행하는 확인 프로세스의 일부분으로 ATA 경량 게이트웨이에서 네트워크의 장치에 대해 다음 포트를 인바운드로 열어야 합니다.
>
> -   NTLM over RPC
> -   NetBIOS

## <a name="ata-console"></a>ATA 콘솔
다음과 같은 브라우저를 통해 ATA 콘솔에 액세스합니다.

-   Internet Explorer 버전 10 이상

-   Microsoft Edge

-   Google Chrome 40 이상

-   스크린 너비 해상도가 1700픽셀 이상인 브라우저

## <a name="see-also"></a>참고 항목

- [ATA 아키텍처](ata-architecture.md)
- [ATA 설치](install-ata-step1.md)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)


