---
title: "ATA의 알려진 문제 해결 | Microsoft Docs"
description: "Advanced Threat Analytics에서 알려진 문제를 해결하는 방법을 설명합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 8/20/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 2362f6bf64147b972e9c45e3b97bab4280c6eeac
ms.sourcegitcommit: 46dd0e695f16a0dd23bbfa140eba15ea6a34d7af
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*



# <a name="troubleshooting-ata-known-issues"></a>ATA의 알려진 문제 해결

이 섹션에서는 ATA 배포 시 발생할 수 있는 오류와 이러한 문제를 해결하는 데 필요한 단계에 대해 자세히 설명합니다.

## <a name="ata-gateway-and-lightweight-gateway-errors"></a>ATA 게이트웨이 및 경량 게이트웨이 오류

> [!div class="mx-tableFixed"]
|오류|설명|해결 방법|
|-------------|----------|---------|
|System.DirectoryServices.Protocols.LdapException: 로컬 오류가 발생했습니다.|ATA 게이트웨이가 도메인 컨트롤러에 대해 인증하지 못했습니다.|1. DNS 서버에서 도메인 컨트롤러의 DNS 레코드가 올바르게 구성되어 있는지 확인합니다. <br>2. ATA 게이트웨이의 시간이 도메인 컨트롤러의 시간과 동기화되어 있는지 확인합니다.|
|System.IdentityModel.Tokens.SecurityTokenValidationException: 인증서 체인이 유효한지 확인하지 못했습니다.|ATA 게이트웨이가 ATA 센터 인증서의 유효성을 검사하지 못했습니다.|1. 루트 CA 인증서가 ATA 게이트웨이의 신뢰할 수 있는 인증 기관 인증서 저장소에 설치되어 있는지 확인합니다. <br>2. CRL(인증서 해지 목록)을 사용할 수 있는지, 인증서 해지 유효성 검사를 수행할 수 있는지 확인합니다.|
|Microsoft.Common.ExtendedException: 생성된 시간을 구문 분석하지 못했습니다.|ATA 게이트웨이가 SIEM에서 전달된 syslog 메시지를 구문 분석하지 못했습니다.|SIEM이 ATA에서 지원하는 형식 중 하나로 메시지를 전달하도록 구성되어 있는지 확인합니다.|
|System.ServiceModel.FaultException: 메시지에 대한 보안을 확인하는 동안 오류가 발생했습니다.|ATA 게이트웨이가 ATA 센터에 대해 인증하지 못했습니다.|ATA 게이트웨이의 시간이 ATA 센터의 시간과 동기화되어 있는지 확인합니다.|
|System.ServiceModel.EndpointNotFoundException: net.tcp://center.ip.addr:443/IEntityReceiver에 연결할 수 없습니다.|ATA 게이트웨이가 ATA 센터에 연결을 설정하지 못했습니다.|네트워크 설정이 정확한지, ATA 게이트웨이와 ATA 센터 간의 네트워크 연결이 활성 상태인지 확인합니다.|
|System.DirectoryServices.Protocols.LdapException: LDAP 서버를 사용할 수 없습니다.|ATA 게이트웨이가 LDAP 프로토콜을 사용하여 도메인 컨트롤러를 쿼리하지 못했습니다.|1. ATA에서 Active Directory 도메인에 연결하는 데 사용한 사용자 계정이 Active Directory 트리의 모든 개체에 대해 읽기 권한을 갖는지 확인합니다. <br>2. 도메인 컨트롤러가 ATA에서 사용하는 사용자 계정의 LDAP 쿼리를 방지하도록 확정되지 않았는지 확인합니다.|
|Microsoft.Tri.Infrastructure.ContractException: 계약 예외|ATA 게이트웨이가 ATA 센터에서 구성을 동기화하지 못했습니다.|ATA 콘솔에서 ATA 게이트웨이의 구성을 완료합니다.|
|System.Reflection.ReflectionTypeLoadException: 요청된 형식 중 하나 이상을 로드할 수 없습니다. 자세한 내용은 LoaderExceptions 속성을 검색하세요.|Message Analyzer는 ATA 게이트웨이에 설치됩니다.| Message Analyzer를 제거하세요.|
|오류 [레이아웃] System.OutOfMemoryException: 'System.OutOfMemoryException' 유형의 예외가 발생했습니다.|ATA 게이트웨이의 메모리가 부족합니다.|도메인 컨트롤러의 메모리 양을 늘리세요.|
|라이브 소비자 시작 실패  ---> Microsoft.Opn.Runtime.Monitoring.MessageSessionException: PEFNDIS 이벤트 공급자가 준비되지 않았습니다.|PEF(Message Analyzer)가 올바르게 설치되지 않았습니다.|그렇지 않고 Hyper-V를 사용하여 Hyper-V 통합 서비스를 업그레이드하려면 지원 서비스에 해결 방법을 문의하세요.|
|오류 0x80070652가 발생하여 설치가 실패했습니다.|컴퓨터에서 보류 중인 다른 설치가 있습니다.|다른 설치가 완료될 때까지 기다리고 필요한 경우 컴퓨터를 다시 시작하세요.|
|System.InvalidOperationException: 지정한 범주에 'Microsoft.Tri.Gateway' 인스턴스가 없습니다.|ATA 게이트웨이에서 프로세스 이름에 PID를 사용하도록 설정되어 있습니다.|프로세스 이름에서 PID를 사용하도록 설정하지 않으려면 [KB281884](https://support.microsoft.com/kb/281884)를 사용하세요.|
|System.InvalidOperationException: 범주가 없습니다.|레지스트리에서 카운터를 사용하지 않도록 설정했을 수 있습니다.|성능 카운터를 다시 작성하려면 [KB2554336](https://support.microsoft.com/kb/2554336)를 사용하세요.|
|System.ApplicationException: ETW 세션 MMA-ETW-Livecapture-a4f595bd-f567-49a7-b963-20fa4e370329를 시작할 수 없습니다.|컴퓨터의 짧은 이름을 가리키는 HOSTS 파일에 호스트 항목이 있습니다.|C:\Windows\System32\drivers\etc\HOSTS 파일에서 호스트 항목을 제거하거나 FQDN으로 변경하세요.|
|System.IO.IOException: 원격 상대방이 전송 스트림을 닫아서 인증에 실패했습니다.|TLS 1.0이 ATA 게이트웨이에서 사용하지 않도록 설정되어 있지만 .Net은 TLS 1.2를 사용하도록 설정되어 있음|다음 옵션 중 하나를 사용합니다. </br> ATA 게이트웨이에서 TLS 1.0을 사용하도록 설정 </br>다음과 같이 SSL 및 TLS에 대한 운영 체제 기본값을 사용하도록 레지스트리 키를 설정하여 .Net에서 TLS 1.2를 사용하도록 설정합니다. </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001` </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`</br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SchUseStrongCrypto"=dword:00000001 `</br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] " SchUseStrongCrypto"=dword:00000001`|
|System.TypeLoadException: 'Microsoft.Opn.Runtime, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' 어셈블리에서 'Microsoft.Opn.Runtime.Values.BinaryValueBufferManager' 형식을 로드할 수 없습니다.|ATA 게이트웨이가 필요한 구문 분석 파일을 로드하지 못했습니다.|Microsoft Message Analyzer가 현재 설치되어 있는지 확인합니다. Message Analyzer는 ATA 게이트웨이/경량 게이트웨이와 함께 설치할 수 없습니다. Message Analyzer를 제거하고 게이트웨이 서비스를 다시 시작합니다.|
|VMware에서 경량 게이트웨이를 사용하는 경우 삭제된 포트 미러 트래픽 경고|VMware 가상 컴퓨터에서 DC를 사용하는 경우, **삭제된 포트 미러 네트워크 트래픽**에 대한 경고를 받을 수 있습니다. VMware의 구성이 일치하지 않기 때문일 수 있습니다. |이러한 경고를 방지하기 위해 다음 설정이 0 또는 사용 안 함으로 설정되어 있는지 확인하세요.: TsoEnable, LargeSendOffload, IPv4, TSO Offload IPv4 Giant TSO Offload도 사용하지 않도록 설정하는 것이 좋습니다. 자세한 내용은 VMware 설명서를 참조하세요.|
|System.Net.WebException: 원격 서버에서 오류가 반환되었습니다. (407) 프록시 인증이 필요합니다.|ATA 센터와 ATA 게이트웨이 통신이 프록시 서버에 의해 중단됩니다.|ATA 게이트웨이 컴퓨터에서 프록시를 사용하지 않도록 설정합니다. <br></br>프록시 설정을 계정별로 지정될 수 있습니다.|
|System.IO.DirectoryNotFoundException: 지정된 경로를 찾을 수 없습니다. (HRESULT의 예외: 0x80070003)|ATA를 작동하는 데 필요한 하나 이상의 서비스가 시작되지 않았습니다.|다음 서비스를 시작합니다. <br></br>성능 로그 및 경고(PLA), 작업 스케줄러(일정)|
|System.Net.WebException: 원격 서버에서 오류가 반환되었습니다. (403) 사용 권한 없음|ATA 센터를 신뢰할 수 없기 때문에 ATA 게이트웨이 또는 경량 게이트웨이가 HTTP 연결을 설정하는 것이 금지되었을 수 있습니다.|ATA 센터의 NetBIOS 이름과 FQDN을 신뢰할 수 있는 웹 사이트 목록에 추가하고 Internet Explorer에서 캐시(또는 구성된 이름이 해당 NetBIOS/FQDN과 다른 경우에는 구성에 지정된 ATA 센터의 이름)를 지웁니다.|
|System.Net.Http.HttpRequestException: PostAsync 실패 [requestTypeName=StopNetEventSessionRequest]|ATA 게이트웨이 또는 ATA 경량 게이트웨이는 WMI 문제로 인해 네트워크 트래픽을 수집하는 ETW 세션을 멈추고 시작할 수 없습니다.|[WMI: WMI 리포지토리 다시 작성](https://blogs.technet.microsoft.com/askperf/2009/04/13/wmi-rebuilding-the-wmi-repository/)의 지침에 따라 WMI 문제를 해결합니다.|

 
## <a name="deployment-errors"></a>배포 오류
> [!div class="mx-tableFixed"]
|오류|설명|해결 방법|
|-------------|----------|---------|
|오류 0x800713ec와 함께 .NET Framework 4.6.1 설치 실패|.Net Framework 4.6.1의 필수 조건이 서버에 설치되어 있지 않습니다. |ATA를 설치하기 전에 Windows 업데이트 [KB2919442](https://www.microsoft.com/download/details.aspx?id=42135) 및 [KB2919355](https://support.microsoft.com/kb/2919355)가 서버에 설치되어 있는지 확인합니다.|
|System.Threading.Tasks.TaskCanceledException: 작업이 취소되었습니다.|ATA 센터에 연결할 수 없어 배포 프로세스 시간이 초과되었습니다.|1.    IP 주소로 이동하여 ATA 센터에 대한 네트워크 연결을 확인합니다. <br></br>2.    프록시 또는 방화벽 구성을 확인합니다.|
|System.Net.Http.HttpRequestException: 요청을 보내는 동안 오류가 발생했습니다. ---> System.Net.WebException: 원격 서버에서 오류가 반환되었습니다. (407) 프록시 인증이 필요합니다.|잘못된 프록시 구성 때문에 ATA 센터에 연결할 수 없어 배포 프로세스 시간이 초과되었습니다.|배포하기 전에 프록시 구성을 사용하지 않도록 설정한 다음 프록시 구성을 다시 사용하도록 설정합니다. 또는 프록시에서 예외를 구성할 수 있습니다.|
|System.Net.Sockets.SocketException: 원격 호스트에 의해 기존 연결이 강제로 종료되었습니다.||다음 옵션 중 하나를 사용합니다. </br>ATA 게이트웨이에서 TLS 1.0을 사용하도록 설정 </br>다음과 같이 SSL 및 TLS에 대한 운영 체제 기본값을 사용하도록 레지스트리 키를 설정하여 .Net에서 TLS 1.2를 사용하도록 설정합니다.</br> `[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`</br> `[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`</br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SchUseStrongCrypto"=dword:00000001` </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] " SchUseStrongCrypto"=dword:00000001`|
|오류 [\[]DeploymentModel[\]] 실패한 관리 인증 [\[]CurrentlyLoggedOnUser=<domain>\<username>상태=FailedAuthentication 예외=[\]]|ATA 게이트웨이 또는 ATA 경량 게이트웨이의 배포 프로세스를 ATA 센터에 대해 성공적으로 인증할 수 없습니다.|배포 프로세스가 실패한 컴퓨터에서 브라우저를 열고 ATA 콘솔에 연결할 수 있는지 확인합니다. </br>연결할 수 없는 경우 문제 해결을 시작하여 ATA 센터에 대해 브라우저를 인증할 수 없는 이유를 확인합니다. </br>확인할 사항:</br>프록시 구성</br>네트워킹 문제</br>ATA 센터와 다른 컴퓨터에서 인증을 위한 그룹 정책 설정입니다.|





## <a name="ata-gateway-and-lightweight-gateway-issues"></a>ATA 게이트웨이 및 경량 게이트웨이 문제

> [!div class="mx-tableFixed"]
|문제|설명|해결 방법|
|-------------|----------|---------|
|도메인 컨트롤러에서 받은 트래픽이 없지만 모니터링 경고가 관찰됨|    ATA 게이트웨이를 통해 포트 미러링을 사용하는 도메인 컨트롤러에서 받은 트래픽이 없음|ATA 게이트웨이 캡처 NIC의 **고급 설정**에서 다음 기능을 사용하지 않도록 설정합니다.<br></br>수신 세그먼트 병합(IPv4)<br></br>수신 세그먼트 병합(IPv6)|
|이 모니터링 경고가 표시됨: **일부 네트워크 트래픽이 분석되고 있지 않음**|VMware 가상 컴퓨터에 ATA 게이트웨이나 경량 게이트웨이가 있는 경우 이 모니터링 경고가 표시될 수 있습니다. VMware에 구성 불일치가 있어 이 경고가 발생합니다.|가상 컴퓨터 NIC 구성에서 다음 설정을 **0** 또는 **사용 안 함**으로 설정: TsoEnable, LargeSendOffload, TSO Offload, Giant TSO Offload|TLS 1.0이 ATA 게이트웨이에서 사용하지 않도록 설정되어 있지만 .Net은 TLS 1.2를 사용하도록 설정되어 있음|




## <a name="see-also"></a>참고 항목
- [ATA 필수 구성 요소](ata-prerequisites.md)
- [ATA 용량 계획](ata-capacity-planning.md)
- [이벤트 수집 구성](configure-event-collection.md)
- [Windows 이벤트 전달 구성](configure-event-collection.md#configuring-windows-event-forwarding)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
