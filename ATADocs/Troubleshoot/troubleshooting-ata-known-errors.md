---
title: "Advanced Threat Analytics 오류 로그 문제 해결 | Microsoft 문서"
description: "ATA의 일반적인 오류를 해결할 수는 방법에 대해 설명합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/14/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 0c72b14a042e473c0cd59811db63ecafc4ec02d4
ms.sourcegitcommit: f18c0841d85e54eca940c8cbf226938b3c2bc80f
translationtype: HT
---
*적용 대상: Advanced Threat Analytics 버전 1.7*



# <a name="troubleshooting-the-ata-error-log"></a>ATA 오류 로그 문제 해결

이 섹션에서는 ATA 배포 시 발생할 수 있는 오류와 이러한 문제를 해결하는 데 필요한 단계에 대해 자세히 설명합니다.

## <a name="ata-gateway-errors"></a>ATA 게이트웨이 오류

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
|System.InvalidOperationException: 지정한 범주에 'Microsoft.Tri.Gateway' 인스턴스가 없습니다.|ATA 게이트웨이에서 프로세스 이름에 PID를 사용하도록 설정되어 있습니다.|프로세스 이름에서 PID를 사용하도록 설정하지 않으려면 [KB281884](https://support.microsoft.com/en-us/kb/281884)를 사용하세요.|
|System.InvalidOperationException: 범주가 없습니다.|레지스트리에서 카운터를 사용하지 않도록 설정했을 수 있습니다.|성능 카운터를 다시 작성하려면 [KB2554336](https://support.microsoft.com/en-us/kb/2554336)를 사용하세요.|
|System.ApplicationException: ETW 세션 MMA-ETW-Livecapture-a4f595bd-f567-49a7-b963-20fa4e370329를 시작할 수 없습니다.|컴퓨터의 짧은 이름을 가리키는 HOSTS 파일에 호스트 항목이 있습니다.|C:\Windows\System32\drivers\etc\HOSTS 파일에서 호스트 항목을 제거하거나 FQDN으로 변경하세요.|
|System.IO.IOException: 원격 상대방이 전송 스트림을 닫아서 인증에 실패했습니다.|TLS 1.0이 ATA 게이트웨이에서 사용하지 않도록 설정되어 있지만 .Net은 TLS 1.2를 사용하도록 설정되어 있음|다음 옵션 중 하나를 사용합니다. </br> ATA 게이트웨이에서 TLS 1.0을 사용하도록 설정 </br>다음과 같이 LLS 및 TLS에 대한 운영 체제 기본값을 사용하도록 레지스트리 키를 설정하여 .Net에서 TLS 1.2를 사용하도록 설정합니다. `[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001` </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"`|



## <a name="ata-lightweight-gateway-errors"></a>ATA 경량 게이트웨이 오류

**오류**: VMware에 경량 게이트웨이를 사용하는 경우 포트 미러 트래픽 경고 삭제

**설명**: DC를 VMware 가상 컴퓨터에서 사용하는 경우, **삭제된 포트 미러 네트워크 트래픽**에 대한 경고를 받을 수 있습니다. VMware의 구성이 일치하지 않기 때문일 수 있습니다. 
**해결 방법**: 이러한 경고를 방지하기 위해 TsoEnable, LargeSendOffload, IPv4, TSO Offload 설정이 0 또는 사용 안 함으로 설정되어 있는지 확인하세요. IPv4 Giant TSO Offload도 사용하지 않도록 설정하는 것이 좋습니다. 자세한 내용은 VMware 설명서를 참조하세요.


## <a name="ata-iis-errors-not-applicable-for-ata-v17-and-above"></a>ATA IIS 오류(ATA v1.7 이상에는 해당되지 않음)
|오류|설명|해결 방법|
|-------------|----------|---------|
|HTTP 오류 500.19 - 내부 서버 오류|IIS URL 재작성 모듈이 제대로 설치되지 않았습니다.|IIS URL 재작성 모듈을 제거했다가 다시 설치합니다.<br>[IIS URL 재작성 모듈을 다운로드합니다.](http://go.microsoft.com/fwlink/?LinkID=615137)|

## <a name="deployment-errors"></a>배포 오류
|오류|설명|해결 방법|
|-------------|----------|---------|
|오류 0x800713ec와 함께 .NET Framework 4.6.1 설치 실패|.Net Framework 4.6.1의 필수 조건이 서버에 설치되어 있지 않습니다. |ATA를 설치하기 전에 Windows 업데이트 [KB2919442](https://www.microsoft.com/download/details.aspx?id=42135) 및 [KB2919355](https://support.microsoft.com/kb/2919355)가 서버에 설치되어 있는지 확인합니다.|

![ATA .NET 설치 오류 이미지](media/netinstallerror.png)


## <a name="see-also"></a>참고 항목
- [ATA 필수 구성 요소](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA 용량 계획](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [이벤트 수집 구성](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Windows 이벤트 전달 구성](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
