---
title: "ATA 의심스러운 활동 가이드 | Microsoft Docs"
description: "이 문서에서는 ATA가 검색할 수 있는 의심스러운 활동 목록 및 해결 단계를 제공합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/3/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1fe5fd6f-1b79-4a25-8051-2f94ff6c71c1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 8a230f47f0bf0e886ba46c964e2c2121e9ee44a4
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*


# <a name="introduction"></a>소개

ATA는 지능형 공격의 여러 단계(정찰, 자격 증명 손상, 측면 확대, 권한 상승, 도메인 우위 등)에 대한 검색을 제공합니다.

이러한 적극 대처(kill-chain) 단계에서 ATA는 현재 검색 기능을 제공하며, 이 단계에 대한 설명은 아래 이미지와 같습니다.

![공격에 대한 적극 대처(kill-chain)에서 측면 활동에 대한 ATA 포커스](media/attack-kill-chain-small.jpg)

이 문서에서는 단계별 각 의심스러운 활동에 대한 세부 정보를 제공합니다.


## <a name="reconnaissance-using-account-enumeration"></a>계정 열거를 사용하여 정찰

| 설명|조사|권장 사항|심각도|
|------|----|------|----------|
| 계정 열거 공격은 공격자가 Kerberos 인증 시도를 통해 다른 계정 이름을 추측하여 사용자가 네트워크에 있는지 검색하는 데 사용하는 기술입니다. 성공적으로 추측된 계정은 공격의 이후 단계에서 사용될 수 있습니다. | 해당 컴퓨터를 살펴보고 많은 Kerberos 인증 프로세스를 시작하는 정당한 이유가 있는지 확인합니다. 이는 사용자가 없기 때문에 여러 계정을 알아보려고 시도했으나 실패한 프로세스(Client_Principal_Unknown 오류)와 성공한 하나 이상의 액세스 시도입니다. <br></br>**예외:** 이 검색은 단일 컴퓨터에서 존재하지 않는 여러 계정을 찾고 인증을 시도합니다. 사용자가 사용자 이름 또는 도메인을 수동으로 입력하는 동안 오류가 발생할 경우 인증 시도는 존재하지 않는 계정에 대한 로그온 시도로 표시됩니다. 많은 사용자가 로그인해야 하는 터미널 서버에서도 정당한 이유로 잘못된 로그인 시도가 많이 발생할 수 있습니다. |이러한 요청을 생성하는 프로세스를 조사합니다.  원본 포트에 따라 프로세스를 식별하는 방법에 대한 도움말은 [특정 패킷을 네트워크로 보내는 Windows 프로세스를 확인하려고 한 적이 있나요?](https://blogs.technet.microsoft.com/nettracer/2010/08/02/have-you-ever-wanted-to-see-which-windows-process-sends-a-certain-packet-out-to-network/)를 참조하세요.|중형|

## <a name="reconnaissance-using-directory-services-enumeration-sam-r"></a>디렉터리 서비스 열거를 사용한 정찰(SAM-R)

| 설명|조사|권장 사항|심각도|
|------|----|------|----------|
| 디렉터리 서비스 정찰은 공격자가 디렉터리 구조를 매핑하고 공격의 이후 단계를 위해 권한 있는 계정을 대상으로 지정하는 데 사용되는 기술입니다. 보안 계정 관리자 원격(SAM-R) 프로토콜은 디렉터리 쿼리에 사용하는 방법 중 하나입니다. | 해당 컴퓨터에서 보안 계정 관리자 - 원격(MS-SAMR)을 수행하는 이유를 파악합니다. 이 작업은 중요한 엔터티 쿼리 등의 비정상적인 방법으로 수행됩니다. <br></br>**예외:** 이 검색은 SAM-R 쿼리를 수행하는 사용자의 정상적인 동작을 프로파일링하고 비정상적인 쿼리가 관찰되면 경고합니다. 정상적인 작업 프로세스의 일부인 경우에도 소유하지 않은 컴퓨터에 로그인하는 중요한 사용자가 비정상으로 검색되는 SAM-R 쿼리를 트리거할 수 있습니다. 이 문제는 일반적으로 IT 팀의 구성원에게 발생할 수 있습니다. 의심스러운 것으로 플래그가 지정되었지만 정상적인 사용의 결과인 경우 해당 동작이 이전에 ATA에서 관찰되지 않았기 때문입니다. | 이 경우 Active Directory 포리스트별로 도메인에서 학습 기간을 늘리고 ATA 적용 범위를 확대하는 것이 좋습니다.<br></br>["SAMRi10" 도구를 다운로드 및 실행합니다](https://gallery.technet.microsoft.com/SAMRi10-Hardening-Remote-48d94b5b). SAMRi10은 ATA 팀에서 릴리스되었으며, SAM-R 쿼리에 대해 사용자 환경의 보안을 강화합니다. | 중형|

## <a name="reconnaissance-using-dns"></a>DNS를 사용하여 정찰


| 설명|조사|권장 사항|심각도|
|------|----|------|----------|
| DNS 서버에는 네트워크의 모든 컴퓨터, IP 주소 및 서비스 맵이 포함되어 있습니다. 이 정보는 공격자가 네트워크 구조를 매핑하고 공격의 이후 단계를 위해 적절한 컴퓨터를 대상으로 지정하는 데 사용됩니다. | 해당 컴퓨터에서 DNS 도메인의 모든 레코드를 가져오기 위해 전체 전송 영역(AXFR) 쿼리를 수행하는 이유를 파악합니다. <br></br>**예외:** 이 검색은 DNS 영역 전송 요청을 실행하는 비 DNS 서버를 식별합니다. DNS 서버에 이러한 종류의 요청을 실행하는 것으로 알려진 여러 가지 보안 스캐너 솔루션이 있습니다. <br></br>또한 ATA가 거짓 긍정 시나리오를 방지하기 위해 포트 53을 통해 ATA 게이트웨이에서 DNS 서버로 통신할 수 있는지 확인합니다.| 요청할 수 있는 호스트를 신중하게 선택하여 영역 전송을 제한합니다. 자세한 내용은 [DNS 보안](https://technet.microsoft.com/library/cc770474(v=ws.11).aspx) 및 [검사 목록: DNS 서버 보안](https://technet.microsoft.com/library/cc770432(v=ws.11).aspx)을 참조하세요. |중형|

## <a name="reconnaissance-using-smb-session-enumeration"></a>SMB 세션 열거를 사용한 정찰


| 설명|조사|권장 사항|심각도|
|------|----|------|----------|
| SMB(서버 메시지 블록) 열거를 통해 공격자는 네트워크의 사용자가 최근에 로그온한 IP 주소에 대한 정보를 얻을 수 있습니다. 공격자는 이 정보를 얻은 후 특정 계정을 대상으로 지정하고 네트워크에서 측면으로 이동하는 데 사용할 수 있습니다. | 해당 컴퓨터에서 SMB 세션 열거를 수행하는 이유를 파악합니다.<br></br>**예외:** 이 검색은 SMB 세션 열거가 엔터프라이즈 네트워크에서 정당하게 사용될 이유가 없다고 가정하지만 일부 보안 스캐너 솔루션(예: Websense)은 이러한 요청을 실행합니다. | [net cease 도구를 통해 사용자 환경의 보안 강화](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b) | 중형   |

## <a name="brute-force-ldap-kerberos-ntlm"></a>무차별 암호 대입(brute force)(LDAP, Kerberos, NTLM)


| 설명|조사|권장 사항|심각도|
|------|----|------|----------|
| 무차별 암호 대입 공격(brute force attack)에서는 공격자가 최종적으로 올바르게 추측하기를 바라며 많은 암호를 시도합니다. 공격자는 올바른 암호를 찾을 때까지 가능한 모든 암호(또는 가능한 암호의 큰 집합)를 체계적으로 확인합니다. 공격자는 올바른 암호를 추측한 후 해당 사용자인 것처럼 네트워크에 로그인할 수 있습니다. 현재 ATA는 Kerberos 또는 NTLM 프로토콜을 사용한 수평(여러 계정) 무차별 암호 대입(brute force) 및 LDAP 단순 바인딩을 사용한 수평 및 수직(단일 계정, 여러 암호 시도) 무차별 암호 대입(brute force)을 지원합니다. | 해당 컴퓨터에서 여러 사용자 계정을 인증하지 못한 이유(여러 사용자에 대해 대략 동일한 인증 시도 횟수 사용) 또는 단일 사용자에 대해 다수의 인증 오류가 발생한 이유를 파악합니다. <br></br>**예외:** 이 검색은 다른 리소스에 인증하는 계정의 정상적인 동작을 프로파일링하며, 비정상적인 패턴이 관찰되면 경고가 트리거됩니다. 이 패턴은 자동으로 인증하는 스크립트에서 흔히 나타나지만, 만료된 자격 증명(즉, 잘못된 암호 또는 사용자 이름)을 사용할 수 있습니다. | 복잡하고 긴 암호는 무차별 암호 대입 공격(brute force attack)에 필요한 첫 번째 수준의 보안을 제공합니다. | 중형   |

## <a name="sensitive-account-exposed-in-plain-text-authentication-and-service-exposing-accounts-in-plain-text-authentication"></a>일반 텍스트 인증으로 공개된 중요한 계정 및 일반 텍스트 인증으로 계정을 공개하는 서비스


| 설명|조사|권장 사항|심각도|
|------|----|------|----------|
| 컴퓨터의 일부 서비스는 중요한 계정에 대해서도 계정 자격 증명을 일반 텍스트로 보냅니다. 트래픽을 모니터링하는 공격자가 악의적인 목적으로 이러한 자격 증명을 훔칠 수 있습니다. 중요한 계정의 일반 텍스트 암호는 경고를 트리거합니다. | 위반하는 컴퓨터를 찾은 후 LDAP 단순 바인딩을 사용하는 이유를 파악합니다. | 원본 컴퓨터의 구성을 확인하고 LDAP 단순 바인딩을 사용하지 않도록 합니다. LDAP 단순 바인딩 대신 LDAP SALS 또는 LDAPS를 사용합니다. 보안 계층 프레임워크를 따르고 권한 상승을 방지하기 위해 계층 전체의 액세스를 제한합니다. | 공개하는 서비스의 경우 낮음, 중요한 계정의 경우 보통 |

## <a name="honey-token-account-suspicious-activities"></a>허니토큰 계정 의심스러운 활동


| 설명|조사|권장 사항|심각도|
|------|----|------|----------|
| Honeytoken 계정은 네트워크에서 해당 계정과 관련된 악의적인 활동을 트래핑, 식별 및 추적하도록 설정된 유인용 계정입니다. 네트워크에서 사용되지 않는 유휴 계정이며, Honeytoken 계정에서 갑자기 활동이 있을 경우 악의적인 사용자가 이 계정을 사용하려고 시도 중임을 나타낼 수 있습니다. | 이 컴퓨터에서 Honeytoken 계정이 인증되는 이유를 파악합니다. | 환경 내 다른 중요한(권한 있는) 계정의 ATA 프로필 페이지에서 잠재적으로 의심스러운 활동이 있는지 확인합니다. | 중형   |

## <a name="unusual-protocol-implementation"></a>비정상적인 프로토콜 구현


| 설명|조사|권장 사항|심각도|
|------|----|------|----------|
| 공격자는 네트워크에 대한 기능을 얻을 수 있는 특정 방식으로 SMB/Kerberos 프로토콜을 구현하는 도구를 사용할 수 있습니다. 이는 Over-Pass-the-Hash 또는 무차별 암호 대입 공격(brute force attack)에 사용되는 악의적인 기술을 나타냅니다. | 해당 컴퓨터에서 인증 프로토콜 또는 SMB를 비정상적인 방식으로 사용하는 이유를 파악합니다. <br></br>**예외:** 드물지만 비표준 방식으로 프로토콜을 구현하는 정당한 도구를 사용하는 경우에 이 검색이 트리거될 수 있습니다. 일부 펜 테스트 응용 프로그램이 이러한 경우로 알려져 있습니다. | 네트워크 트래픽을 캡처하고 비정상적인 프로토콜 구현으로 트래픽을 생성하는 프로세스를 식별합니다.<br></br>WannaCry 공격인지 확인하려면 다음 작업을 수행합니다.<br></br> 1.   의심스러운 활동의 Excel 내보내기를 다운로드합니다.<br></br>
2.  네트워크 활동 탭을 열고 "Json" 필드로 이동하여 관련된 Smb1SessionSetup & Ntlm JSON을 복사합니다.<br></br>
3.  Smb1SessionSetup.OperatingSystem이 "Windows 2000 2195"이고 Smb1SessionSetup.IsEmbeddedNtlm이 "true"이며 Ntlm.SourceAccountId가 "null"이면 WannaCry입니다.
| 보통   |

## <a name="malicious-data-protection-private-information-request"></a>악성 데이터 보호 개인 정보 요청


| 설명|조사|권장 사항|심각도|
|------|----|------|----------|
| DPAPI(데이터 보호 API)는 Windows의 여러 구성 요소에서 암호, 암호화 키 및 기타 중요한 데이터를 안전하게 저장하는 데 사용됩니다. 도메인 컨트롤러는 도메인에 연결된 Windows 컴퓨터에서 DPAPI로 암호화된 모든 암호를 해독하는 데 사용할 수 있는 백업 마스터 키를 보유합니다. 공격자는 DPAPI 도메인 백업 마스터 키를 사용하여 도메인에 연결된 모든 컴퓨터(브라우저 암호, 암호화된 파일 등)의 모든 암호를 해독할 수 있습니다. | 컴퓨터에서 DPAPI의 마스터 키에 대해 이 문서화되지 않은 API 호출을 사용하여 요청을 수행하는 이유를 파악합니다. | DPAPI에 대한 자세한 내용은 [Windows 데이터 보호](https://msdn.microsoft.com/library/ms995355.aspx)를 참조하세요. | 높은     |

## <a name="suspicion-of-identity-theft-based-on-abnormal-behavior"></a>비정상적인 동작에 따른 ID 도용 의심


| 설명|조사|권장 사항|심각도|
|------|----|------|----------|
| 동작 모델을 작성하면(동작 모델을 작성하려면 3주 동안 50개 이상의 활성 계정이 필요함) 모든 비정상적인 동작은 경고를 트리거합니다. 특정 사용자 계정에 대해 작성된 모델과 일치하지 않는 동작은 ID 도용을 가리킬 수 있습니다. | 해당 사용자가 다르게 동작할 수 있는 이유를 파악합니다. <br></br>**예외:** ATA에 부분적인 적용 범위만 있는 경우(일부 도메인 컨트롤러는 ATA 게이트웨이로 라우팅되지 않음) 부분적인 활동만 특정 사용자에 대해 학습됩니다. 3주 이상 후에 갑자기 ATA에서 모든 트래픽의 처리를 시작할 경우 사용자의 전체 활동이 경고를 트리거할 수 있습니다. | 모든 도메인 컨트롤러에 ATA가 배포되어 있는지 확인합니다. <br></br>1.  조직에서 사용자의 직위가 새로 지정되었는지 확인합니다.<br></br>2.  사용자가 계절 작업자인지 확인합니다.<br></br>3.  긴 부재 후에 사용자가 방금 돌아왔는지 확인합니다.| 모든 사용자의 경우 보통, 중요한 사용자의 경우 높음 |


## <a name="pass-the-ticket"></a>Pass-the-Ticket


| 설명|조사|권장 사항|심각도|
|------|----|------|----------|
| Pass-the-Ticket 공격은 공격자가 하나의 컴퓨터에서 Kerberos 티켓을 도용하여 네트워크의 엔터티로 가장해 다른 컴퓨터에 대한 액세스 권한을 얻는 측면 이동 기법입니다. | 이 검색은 둘 이상의 서로 다른 컴퓨터에서 동일한 Kerberos 티켓을 사용합니다. 경우에 따라 IP 주소가 빠르게 변경되면 ATA는 다른 IP 주소가 동일한 컴퓨터 또는 다른 컴퓨터에서 사용되는지 확인하지 못할 수도 있습니다. 이는 소형 DHCP 풀(VPN, WiFi 등)과 공유 IP 주소(NAT 장치)의 일반적인 문제입니다. | 보안 계층 프레임워크를 따르고 권한 상승을 방지하기 위해 계층 전체의 액세스를 제한합니다. | 높은     |

## <a name="pass-the-hash"></a>Pass-the-Hash


| 설명|조사|권장 사항|심각도|
|------|----|------|----------|
| Pass-the-Hash 공격에서 공격자는 일반적인 경우처럼 연결된 일반 텍스트 암호 대신 사용자 암호의 기본 NTLM 해시를 사용하여 원격 서버 또는 서비스에 인증합니다. | 계정이 이 경고 주위 기간에 비정상적인 활동을 수행했는지 확인합니다. | [Pass-the-Hash](http://aka.ms/PtH)에 설명된 권장 사항을 구현합니다. 보안 계층 프레임워크를 따르고 권한 상승을 방지하기 위해 계층 전체의 액세스를 제한합니다. | 높은|

## <a name="over-pass-the-hash"></a>Over-Pass The Hash


| 설명|조사|권장 사항|심각도|
|------|----|------|----------|
| Over-Pass-the-Hash 공격은 Kerberos 인증 프로토콜의 구현 취약성을 악용합니다. 이 프로토콜에서는 NTLM 해시를 통해 Kerberos 티켓을 만들기 때문에 공격자가 사용자 암호 없이 네트워크의 서비스에 인증할 수 있습니다. | 암호화 다운그레이드: 해당 계정이 AES 사용 방법을 학습한 후 Kerberos에서 RC4를 사용하는 이유를 파악합니다. <br></br>**예외:** 이 검색은 도메인에 사용된 암호화 방법을 프로파일링하고 비정상적이고 더 약한 방법이 관찰될 경우 경고합니다. 경우에 따라 더 약한 암호화 방법이 사용되며, ATA는 정상적인(드물긴 하지만) 작업 프로세스의 일부일 수도 있지만 이를 비정상적인 것으로 검색합니다. 이 문제는 이러한 동작이 ATA에서 이전에 관찰된 적이 없는 경우에 발생할 수 있습니다. 도메인에서 ATA의 적용 범위를 확대하면 도움이 됩니다. | [Pass-the-Hash](http://aka.ms/PtH)에 설명된 권장 사항을 구현합니다. 보안 계층 프레임워크를 따르고 권한 상승을 방지하기 위해 계층 전체의 액세스를 제한합니다. | 높은     |

## <a name="privilege-escalation-using-forged-authorization-data-ms14-068-exploit-forged-pac--ms11-013-exploit-silver-pac"></a>위조된 권한 부여 데이터를 사용한 권한 상승 공격(MS14-068 익스플로잇(위조된 PAC)/MS11-013 익스플로잇(실버 PAC))


| 설명|조사|권장 사항|심각도|
|------|----|------|----------|
| 이전 버전의 Windows Server에서 알려진 취약성으로 인해 공격자는 사용자의 권한 부여 데이터가 포함된 Kerberos 티켓의 필드인 PAC(Privileged Attribute Certificate)(Active Directory에서는 그룹 멤버 자격임)를 조작하여 공격자에게 추가 권한을 부여할 수 있습니다. | PAC 이외의 권한 부여 방법을 사용할 수 있는 특수 서비스가 영향을 받는 컴퓨터에서 실행되고 있는지 확인합니다. <br></br>**예외:** 일부 특정 시나리오에서는 리소스가 자체 권한 부여 메커니즘을 구현하며 ATA에서 경고를 트리거할 수 있습니다. | Windows Server 2012 R2까지의 운영 체제를 사용하는 모든 도메인 컨트롤러에 [KB3011780](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privilege)이 설치되어 있고 2012 R2까지 모든 구성원 서버 및 도메인 컨트롤러가 KB2496930으로 최신 상태인지 확인합니다. 자세한 내용은 [실버 PAC](https://technet.microsoft.com/library/security/ms11-013.aspx) 및 [위조된 PAC](https://technet.microsoft.com/library/security/ms14-068.aspx)를 참조하세요. | 높은     |

## <a name="abnormal-sensitive-group-modification"></a>비정상적인 중요한 그룹 수정


| 설명|조사|권장 사항|심각도|
|------|----|------|----------|
| 이전 버전의 Windows Server에서 알려진 취약성으로 인해 공격자는 사용자의 권한 부여 데이터가 포함된 Kerberos 티켓의 필드인 PAC(Privileged Attribute Certificate)(Active Directory에서는 그룹 멤버 자격임)를 조작하여 공격자에게 추가 권한을 부여할 수 있습니다. | 그룹 변경이 정당한지 확인합니다. <br></br>**예외:** 이 검색은 중요한 그룹을 수정하는 사용자의 정상적인 동작을 프로파일링하고 비정상적인 변경이 관찰되면 경고합니다. 이러한 동작이 ATA에서 이전에 관찰된 적이 없는 경우 정당한 변경이 경고를 트리거할 수 있습니다. 도메인에서 학습 기간을 늘리고 ATA 적용 범위를 확대하면 도움이 됩니다. | 중요한 그룹을 수정할 수 있는 권한이 있는 사용자 그룹을 최소화해야 합니다. 가능하면 Just-I- Time 권한을 사용합니다. | 중형   |

## <a name="encryption-downgrade---skeleton-key-malware"></a>암호화 다운그레이드 - 스켈레톤 키 맬웨어


| 설명|조사|권장 사항|심각도|
|------|----|------|----------|
| 스켈레톤 키는 도메인 컨트롤러에서 실행되며 해당 암호를 몰라도 모든 계정으로 도메인에 인증할 수 있는 맬웨어입니다. 대체로 이 맬웨어는 더 약한 암호화 알고리즘을 사용하여 도메인 컨트롤러의 사용자 암호를 암호화합니다. | 암호화 다운그레이드: 해당 계정이 AES 사용 방법을 학습한 후 Kerberos에서 RC4를 사용하는 이유를 파악합니다. <br></br>**예외:** 이 검색은 도메인에 사용된 암호화 방법을 프로파일링합니다. 경우에 따라 더 약한 암호화 방법이 사용되며, ATA는 정상적인(드물긴 하지만) 작업 프로세스의 일부일 수도 있지만 이를 비정상적인 것으로 검색합니다. | [ATA 팀이 작성한 스캐너](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73)를 사용하여 스켈레톤 키가 도메인 컨트롤러의 영향을 받았는지 확인할 수 있습니다. | 높은 |

## <a name="golden-ticket"></a>골든 티켓


| 설명|조사|권장 사항|심각도|
|------|----|------|----------|
| 공격자에게 도메인 관리자 권한이 있으면 네트워크의 모든 리소스에 대한 권한 부여를 제공하고 티켓 만료 시간을 원하는 대로 설정하는 Kerberos TGT(허용 티켓)를 만들 수 있습니다. 이렇게 하면 공격자가 네트워크에서 지속성을 얻을 수 있습니다. | 암호화 다운그레이드: 해당 계정이 AES 사용 방법을 학습한 후 Kerberos에서 RC4를 사용하는 이유를 파악합니다. <br></br>**예외:** 이 검색은 도메인에 사용된 암호화 방법을 프로파일링하고 비정상적이고 더 약한 방법이 관찰될 경우 경고를 보냅니다. 경우에 따라 더 약한 암호화 방법이 사용되며, ATA는 정상적인(드물긴 하지만) 작업 프로세스의 일부일 수도 있지만 이를 비정상적인 것으로 검색합니다. 이 문제는 이러한 동작이 ATA에서 이전에 관찰된 적이 없는 경우에 발생할 수 있습니다. ATA 적용 범위가 도메인 전체인지 확인합니다. | 다음과 같은 방법으로 마스터 키 KRBTGT(Kerberos 허용 티켓)를 최대한 안전하게 유지합니다.<br></br>1.  물리적 보안<br></br>2.  가상 컴퓨터에 대한 물리적 보안<br></br>3. 도메인 컨트롤러 보안 강화 수행<br></br>4.  LSA(로컬 보안 기관) 격리/Credential Guard<br></br>골든 티켓이 검색되면 더 세부적인 조사를 수행하여 전술적 복구가 필요한지 여부를 평가해야 합니다.<br></br>[Microsoft 블로그, KRBTGT Account Password Reset Scripts now available for customers](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/)(현재 KRBTGT 계정 암호 다시 설정 스크립트가 고객에게 제공됨)의 지침에 따라 [krbtgt 계정 암호/키 도구 다시 설정](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51)을 사용하여 KRBTGT(Kerberos 허용 티켓)를 정기적으로 두 번 변경합니다. <br></br>이러한 [Pass-the-Hash 권장 사항](http://aka.ms/PtH)을 구현합니다. | 중형   |



## <a name="remote-execution"></a>원격 실행


| 설명|조사|권장 사항|심각도|
|------|----|------|----------|
| 관리자 자격 증명을 손상시킨 공격자는 도메인 컨트롤러에서 원격 명령을 실행할 수 있습니다. 지속성 유지, 정보 수집, DoS(서비스 거부) 공격 등의 이유로 사용될 수 있습니다. | 해당 계정이 도메인 컨트롤러에 대해 이 원격 실행을 수행할 수 있는지 확인합니다. <br></br>**예외:** 정상적인 관리 프로세스의 일부인 경우에도 때때로 도메인 컨트롤러에서 명령을 실행하는 정당한 사용자가 이 경고를 트리거할 수 있습니다. 도메인 컨트롤러에 대해 관리 작업을 수행하는 IT 팀 구성원 또는 서비스 계정에 가장 일반적입니다. | 비계층 0 컴퓨터에서 도메인 컨트롤러에 대한 원격 액세스를 제한합니다. 의심스럽고 필수가 아닌 부실 파일 및 폴더를 모두 삭제합니다. 강력한 UAC(사용자 계정 컨트롤) 정책을 구현합니다. 보안이 강화된 컴퓨터만 관리를 위해 도메인 컨트롤러에 연결할 수 있도록 [PAW](https://technet.microsoft.com/en-us/windows-server-docs/security/securing-privileged-access/securing-privileged-access)를 구현합니다. | 낮음      |

## <a name="malicious-replication-requests"></a>악의적인 복제 요청


| 설명|조사|권장 사항|심각도|
|------|----|------|----------|
| Active Directory 복제는 한 도메인 컨트롤러에서 변경된 내용을 동일한 데이터의 복사본을 저장하는 도메인 또는 포리스트의 다른 모든 도메인 컨트롤러와 동기화하는 프로세스입니다. 적절한 사용 권한이 제공될 경우 공격자가 도메인 컨트롤러를 가장해서 복제 요청을 시작하여 암호 해시를 비롯한, Active Directory에 저장된 데이터를 검색할 수 있습니다. | 컴퓨터에서 도메인 컨트롤러 복제 API를 사용하는 이유를 파악합니다. 이 검색에서 ATA는 디렉터리 포리스트의 구성 파티션을 사용하여 컴퓨터가 도메인 컨트롤러인지 파악합니다. <br></br>**예외:** Azure AD Dir Sync에서 이 경고가 트리거될 수 있습니다. | 다음 사용 권한을 확인합니다. - 디렉터리 변경 내용 복제 <br></br>- 디렉터리 변경 내용 모두 복제<br></br>자세한 내용은 [SharePoint Server 2013에서 Active Directory 도메인 서비스에 프로필 동기화 권한 부여](https://technet.microsoft.com/library/hh296982.aspx)를 참조하세요.<br></br>[AD ACL 스캐너](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/)를 활용하거나 PowerShell 스크립트를 만들어 이러한 사용 권한을 가진 도메인 사용자를 확인할 수 있습니다. | 중형   |



## <a name="broken-trust-between-domain-and-computers"></a>도메인 및 컴퓨터 간의 손상된 신뢰


| 설명|조사|권장 사항|심각도|
|------|----|------|----------|
| 손상된 신뢰는 Active Directory 보안 요구 사항이 적용되지 않을 수 있음을 의미합니다. 종종 기본 보안 및 규정 준수 오류와 공격자를 위한 소프트 대상으로 간주됩니다. 이 경우 24시간 동안 하나의 컴퓨터 계정에서 연속으로 발생한 Kerberos 인증 오류가 5회를 초과하면 ATA에서 경고가 트리거됩니다. 컴퓨터가 도메인 컨트롤러와 통신하지 않으므로 (1) 업데이트된 그룹 정책이 없고 (2) 로그인이 캐시된 자격 증명으로 제한됩니다. | 이벤트 로그를 확인하여 도메인과의 컴퓨터 신뢰가 정상인지 확인합니다. | 필요한 경우 컴퓨터를 도메인에 다시 연결하거나 컴퓨터 암호를 다시 설정합니다. | 낮음      |

## <a name="massive-object-deletion"></a>대규모 개체 삭제


| 설명|조사|권장 사항|심각도|
|------|----|------|----------|
| 모든 계정의 5% 이상이 삭제되면 ATA에서 이 경고가 발생합니다. 이 경우 삭제된 항목 컨테이너에 대한 읽기 권한이 필요합니다. | 모든 계정의 5%가 갑자기 삭제된 이유를 파악합니다. | Active Directory에서 계정을 삭제할 수 있는 사용자에 대한 권한을 제거합니다. 자세한 내용은 [디렉터리 개체에 대한 사용 권한 보기 또는 설정](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx)을 참조하세요. | 낮음 |

## <a name="see-also"></a>참고 항목
- [의심스러운 활동 작업](working-with-suspicious-activities.md)
- [위조된 PAC 공격 조사](use-case-forged-pac.md)
- [ATA의 알려진 오류 문제 해결](troubleshooting-ata-known-errors.md)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
