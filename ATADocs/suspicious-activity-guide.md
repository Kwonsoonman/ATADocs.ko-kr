---
title: "ATA 의심스러운 활동 가이드 | Microsoft Docs"
d|Description: This article provides a list of the suspicious activities ATA can detect and steps for remediation.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 09/6/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1fe5fd6f-1b79-4a25-8051-2f94ff6c71c1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 05550e56479de0390d7f2d990ffae4b319dec9f9
ms.sourcegitcommit: 74cce0c1d52086fdf10ea70f590b306c1c7e8b14
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*


# <a name="advanced-threat-analytics-suspicious-activity-guide"></a>Advanced Threat Analytics 의심스러운 활동 가이드

적절한 조사에 따르면 의심스러운 활동을 다음과 같이 분류할 수 있습니다.

-   **참 긍정**: ATA에서 검색한 악의적인 동작입니다.

-   **무해한 참 긍정**: ATA에서 검색하고 침투 테스트와 같이 실재하지만 악의적이지 않은 동작입니다.

-   **거짓 긍정**: 발생하지 않은 동작을 의미하는 거짓 경보입니다.

ATA 경고를 사용하는 방법에 대한 자세한 내용은 [의심스러운 활동 작업](working-with-suspicious-activities.md)을 참조하세요.

질문이나 의견이 있으시면 [ATAEval@microsoft.com](mailto:ATAEval@microsoft.com)에 문의하세요.

## <a name="abnormal-sensitive-group-modification"></a>비정상적인 중요한 그룹 수정


**설명**

공격자는 높은 권한이 있는 가진 그룹에 사용자를 추가합니다. 더 많은 리소스에 액세스하고 지속성을 얻기 위해 그렇게 합니다. 검색에서 사용자의 그룹 수정 활동을 프로파일링하고, 중요한 그룹에 비정상적인 추가가 표시될 때 경고합니다. 프로파일링은 ATA에서 지속적으로 수행됩니다. 경고를 트리거할 수 있기 전의 최소 기간은 각 도메인 컨트롤러마다 1개월입니다.

ATA의 중요한 그룹에 대한 정의는 [ATA 콘솔 작업](working-with-ata-console.md#sensitive-groups)을 참조하세요.


검색은 [도메인 컨트롤러에서 감사된 이벤트](https://docs.microsoft.com/advanced-threat-analytics/configure-event-collection)를 기반으로 합니다.
[ATA 감사(AuditPol, 고급 감사 설정 적용, 경량 게이트웨이 서비스 검색)](https://aka.ms/ataauditingblog)에서 참조된 도구를 사용하여 도메인 컨트롤러에 필요한 이벤트를 감사하는지 확인합니다.

**조사**

1. 그룹 수정이 합법적인가요? </br>거의 발생하지 않는 합법적인 그룹 수정은 "정상"으로 학습되지 않아 경고가 발생할 수 있으며, 이는 무해한 참 긍정으로 간주됩니다.

2. 추가된 개체가 사용자 계정인 경우 관리자 그룹에 추가된 후 해당 사용자 계정에서 수행한 작업을 확인합니다. 더 많은 컨텍스트를 얻으려면 ATA의 사용자 페이지로 이동합니다. 추가 전후에 계정과 관련된 다른 의심스러운 활동이 있었나요? **중요한 그룹 수정** 보고서를 다운로드하여 같은 기간 동안 다른 수정 사항과 수정한 사용자를 확인합니다.

**수정**

중요한 그룹을 수정할 권한이 있는 사용자 수를 최소화합니다.

해당하는 경우 [Active Directory 도메인 서비스에 대한 Privileged Access Management](https://docs.microsoft.com/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services)를 설정합니다.

## <a name="broken-trust-between-computers-and-domain"></a>컴퓨터 및 도메인 간 손상된 신뢰

**설명**

손상된 신뢰는 Active Directory 보안 요구 사항이 의심스러운 컴퓨터에 적용되지 않을 수 있음을 의미합니다. 종종 기본 보안 및 규정 준수 오류와 공격자를 위한 소프트 대상으로 간주됩니다. 이 검색에서 24시간 동안 컴퓨터 계정에서 Kerberos 인증 오류가 6개 이상 표시되면 경고가 트리거됩니다.

**조사**

의심스러운 컴퓨터에서 도메인 사용자의 로그온을 허용하고 있나요? 
- 그러한 경우 수정 단계에서 이 컴퓨터를 무시할 수 있습니다.

**수정**

필요한 경우 컴퓨터를 도메인에 다시 연결하거나 컴퓨터 암호를 다시 설정합니다.

## <a name="brute-force-attack-using-ldap-simple-bind"></a>LDAP 단순 바인딩을 사용한 무차별 대입 공격

**설명**

>[!NOTE]
> **의심스러운 인증 실패**와 이 검색 사이의 주요 차이점은 이 검색의 경우 ATA에서 서로 다른 암호를 사용하고 있었는지 여부를 결정할 수 있다는 것입니다.

무차별 대입 공격의 경우 공격자가 하나 이상의 계정에 대해 올바른 암호를 찾을 때까지 다른 계정에 대해 여러 다른 암호로 인증을 시도합니다. 일단 찾았으면 공격자가 해당 계정을 사용하여 로그인할 수 있습니다.

이 검색에서는 ATA에서 여러 다른 암호를 사용하고 있음을 검색하면 경고가 트리거됩니다. 암호를 사용하는 유형은 여러 사용자 간에 작은 암호 집합을 사용하는 *가로로*이거나 소수의 사용자만 큰 암호 집합을 사용하는 *세로로*이며, 이 두 가지 옵션을 조합하여 사용할 수도 있습니다.

**조사**

1. 관련된 계정이 많은 경우 **세부 정보 다운로드**를 클릭하여 Excel 스프레드시트의 목록을 봅니다.

2. 경고를 클릭하여 해당 전용 페이지로 이동합니다. 로그인 시도가 성공적인 인증으로 완료되었는지 확인합니다. 이러한 시도는 인포그래픽의 오른쪽에 **추측된 계정**으로 표시됩니다. 그러한 경우 **추측된 계정**이 원본 컴퓨터에서 일반적으로 사용되는 계정인가요? 그렇다면 의심스러운 활동을 **표시하지 않습니다**.

3. **추측된 계정**이 없으면 원본 컴퓨터에서 일반적으로 사용되는 **공격받은 계정**인가요? 그렇다면 의심스러운 활동을 **표시하지 않습니다**.

**수정**

[복잡하고 긴 암호](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy)는 무차별 암호 대입 공격에 대한 첫 번째 수준의 보안을 제공합니다.

## <a name="encryption-downgrade-activity"></a>암호화 다운그레이드 활동

**설명**

다양한 공격 메서드는 약한 Kerberos 암호화 암호를 사용합니다. 이 검색에서 ATA는 컴퓨터 및 사용자가 사용하는 Kerberos 암호화 종류를 학습하고 약한 암호가 사용될 때 (1) 원본 컴퓨터 및/또는 사용자에 대해 비정상적입니다. 및 (2) 알려진 공격 기술과 일치합니다.라는 경고가 표시됩니다.

세 가지 검색 유형이 있습니다.

1.  스켈레톤 키 - 도메인 컨트롤러에서 실행되며 해당 암호를 모른 채 모든 계정으로 도메인에 인증할 수 있는 맬웨어입니다. 이 맬웨어는 종종 더 약한 암호화 알고리즘을 사용하여 도메인 컨트롤러에서 사용자의 암호를 암호화합니다. 이 검색에서 원본 컴퓨터의 KRB_ERR 메시지 암호화 방법은 이전에 확인된 동작과 비교하여 다운그레이드되었습니다.

2.  골든 티켓 - [골든 티켓](#golden-ticket) 경고에서 원본 컴퓨터의 TGS_REQ(서비스 요청) 메시지의 TGT 필드에 대한 암호화 방법이 이전에 확인된 동작과 비교하여 다운그레이드되었습니다. 이는 다른 Golden Ticket 검색에서와 같이 시간 이상을 기반으로 하지 않음에 유의하세요. 또한 ATA에서 검색한 위의 서비스 요청과 관련된 Kerberos 인증 요청도 없었습니다.

3.  Overpass-the-Hash - 원본 컴퓨터의 AS_REQ 메시지 암호화 종류가 이전에 확인된 동작과 비교하여 다운그레이드되었습니다. 즉 컴퓨터에서 AES를 사용했습니다.

**조사**

먼저 경고에 대한 설명을 확인하여 처리 중인 유형이 위의 세 가지 유형 중에서 어떤 유형인지 확인합니다.

1.  스켈레톤 키 - [ATA 팀이 작성한 스캐너](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73)를 사용하여 스켈레톤 키가 도메인 컨트롤러에 영향을 주었는지 확인할 수 있습니다.
    스캐너에서 하나 이상의 도메인 컨트롤러로부터 맬웨어를 검색하면 참 긍정입니다.

2.  골든 티켓 - 거의 사용되지 않는 사용자 지정 응용 프로그램에서 낮은 암호화 암호를 사용하여 인증하는 경우가 있습니다. 원본 컴퓨터에 이러한 사용자 지정 앱이 있는지 확인합니다. 그러한 경우 무해한 참 긍정일 수 있으며 표시되지 않을 수 있습니다.

3.  Overpass-the-Hash - 스마트 카드로 구성된 사용자가 대화형 로그인에 필요하고, 이 설정을 해제한 다음 사용하도록 설정한 경우 이 경고가 트리거되는 경우가 있습니다. 관련된 계정에 대해 이와 같은 변경 내용이 있었는지 확인합니다. 그러한 경우 이는 무해한 참 긍정일 수 있으며 표시되지 않을 수 있습니다.

**수정**

1.  스켈레톤 키 - 맬웨어를 제거합니다. 자세한 내용은 SecureWorks의 [스켈레톤 키 맬웨어 분석(영문)](https://www.secureworks.com/research/skeleton-key-malware-analysis)을 참조하세요.

2.  Golden Ticket - 의심스러운 [골든 티켓](#golden-ticket) 활동의 지침을 따릅니다.   
    또한 골든 티켓을 만들려면 도메인 관리자 권한이 필요하므로 [Pass-the-Hash 권장 사항(영문)](http://aka.ms/PtH)을 구현합니다.

3.  Overpass-the-Hash - 관련된 계정이 중요하지 않으면 해당 계정의 암호를 다시 설정합니다. 이렇게 하면 공격자가 암호 해시에서 새 Kerberos 티켓을 만들지 못하게 하지만, 기존 티켓은 만료될 때까지 계속 사용할 수 있습니다. 중요한 계정인 경우 의심스러운 골든 티켓 활동과 마찬가지로 KRBTGT 계정을 두 번 다시 설정해야 합니다. KRBTGT를 두 번 다시 설정하면 이 도메인의 모든 Kerberos 티켓이 무효화되므로 그렇게 되기 전에 계획을 세웁니다. [고객을 위해 사용할 수 있는 KRBTGT 계정 암호 재설정 스크립트(영문)](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/)의 지침을 참조하세요. 또한 [KRBTGT 계정 암호/키 도구 재설정(영문)](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51)도 참조하세요. 이는 측면 확대 기술이므로 [Pass-the-Hash 권장 사항(영문)](http://aka.ms/PtH)의 모범 사례를 따릅니다.

## 골든 티켓<a name="golden-ticket"></a>

**설명**

도메인 관리자 권한이 있는 공격자는 [KRBTGT 계정](https://technet.microsoft.com/library/dn745899(v=ws.11).aspx#Sec_KRBTGT)을 손상시킬 수 있습니다. KRBTGT 계정을 사용하면 모든 리소스에 대한 권한 부여를 제공하고 티켓 만료를 임의의 시간으로 설정하는 Kerberos TGT(허용 티켓)을 만들 수 있습니다. 이 가짜 TGT는 "골든 티켓"이라고 불리며 공격자가 네트워크에서 지속성을 달성할 수 있도록 허용합니다.

이 검색에서 Kerberos 허용 티켓이 [사용자 계정에 대한 최대 수명](https://technet.microsoft.com/library/jj852169(v=ws.11).aspx) 보안 정책에 지정된 허용 시간보다 더 오랫동안 사용되면 경고가 트리거됩니다.

**조사**

1. 최근에(최근 몇 시간 내에) 그룹 정책에서 **사용자 티켓 최대 수명** 설정을 변경했나요? 그러한 경우 경고를 **닫습니다**(거짓 긍정인 경우).

2. 이 경고와 관련된 ATA 게이트웨이가 가상 컴퓨터인가요? 그러한 경우 최근에 저장된 상태에서 다시 시작했나요? 그러한 경우 이 경고를 **닫습니다**.

3. 위 질문에 대한 대답이 '아니요'인 경우 악의적이라고 가정합니다.

**수정**

[KRBTGT 계정 암호/키 도구 재설정(영문)](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51)을 사용하여 [고객을 위해 사용할 수 있는 KRBTGT 계정 암호 재설정 스크립트(영문)](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/)의 지침에 따라 KRBTGT(Kerberos 허용 티켓) 암호를 두 번 변경합니다. KRBTGT를 두 번 다시 설정하면 이 도메인의 모든 Kerberos 티켓이 무효화되므로 그렇게 되기 전에 계획을 세웁니다.  
또한 골든 티켓을 만들려면 도메인 관리자 권한이 필요하므로 [Pass-the-Hash 권장 사항(영문)](http://aka.ms/PtH)을 구현합니다.

## <a name="honeytoken-activity"></a>허니 토큰 활동


**설명**

허니 토큰 계정은 이러한 계정과 관련된 악의적인 활동을 식별 및 추적하도록 설정된 유인용 계정입니다. 허니 토큰 계정은 공격자를 유혹하기 위해 매력적인 이름(예: SQL-Admin)을 사용하지만 사용하지 않은 상태로 그대로 두어야 합니다. 이러한 계정의 활동은 악의적인 동작을 나타낼 수 있습니다.

허니 토큰 계정에 대한 자세한 내용은 [ATA 설치 - 7단계](install-ata-step7.md)를 참조하세요.

**조사**

1.  의심스러운 활동 페이지(예: Kerberos, LDAP, NTLM)에서 설명하는 메서드를 사용하여 원본 컴퓨터의 소유자가 허니 토큰 계정으로 인증했는지 확인합니다.

2.  원본 컴퓨터 프로필 페이지로 이동하여 이러한 소유자가 다른 계정으로 인증받았는지 확인합니다. 허니 토큰 계정을 사용한 경우 해당 계정의 소유자와 비교하여 확인합니다.

3.  이 활동은 비대화형 로그인일 수 있으므로 원본 컴퓨터에서 실행 중인 응용 프로그램이나 스크립트를 확인해야 합니다.

1~3 단계를 수행한 후 무해 사용의 증거가 없으면 악의적이라고 가정합니다.

**수정**

허니 토큰 계정이 의도된 용도로만 사용되는지 확인합니다. 그렇지 않으면 많은 경고가 생성될 수 있습니다.

## <a name="identity-theft-using-pass-the-hash-attack"></a>Pass-the-Hash 공격을 통한 ID 도용

**설명**

Pass-the-Hash는 공격자가 한 컴퓨터에서 사용자의 NTLM 해시를 도용하여 다른 컴퓨터에 액세스하는 데 사용하는 측면 확대 기술입니다. 

**조사**

대상 사용자가 소유하거나 정기적으로 사용하는 컴퓨터에서 해시를 사용했나요? 그러한 경우 거짓 긍정입니다. 그렇지 않은 경우 참 긍정일 것입니다.

**수정**

1. 관련된 계정이 중요하지 않으면 해당 계정의 암호를 다시 설정합니다. 이렇게 하면 공격자가 암호 해시에서 새 Kerberos 티켓을 만들지 못하게 하지만, 기존 티켓은 만료될 때까지 계속 사용할 수 있습니다. 

2. 중요한 계정인 경우 의심스러운 골든 티켓 활동과 마찬가지로 KRBTGT 계정을 두 번 다시 설정해야 합니다. KRBTGT를 두 번 다시 설정하면 이 도메인의 모든 Kerberos 티켓이 무효화되므로 그렇게 되기 전에 계획을 세웁니다. [고객을 위해 사용할 수 있는 KRBTGT 계정 암호 재설정 스크립트(영문)](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/)의 지침을 참조하고, [KRBTGT 계정 암호/키 도구 재설정(영문)](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51) 사용도 참조하세요. 이는 측면 확대 기술이므로 [Pass-the-Hash 권장 사항(영문)](http://aka.ms/PtH)의 모범 사례를 따릅니다.

## <a name="identity-theft-using-pass-the-ticket-attack"></a>Pass-the-Ticket 공격을 통한 ID 도용

**설명**

Pass-the-Ticket 공격은 공격자가 한 컴퓨터에서 Kerberos 티켓을 도용하고 이 티켓을 다시 사용하여 다른 컴퓨터에 액세스하는 데 사용하는 측면 확대 기술입니다. 이 검색에서 Kerberos 티켓이 둘 이상의 컴퓨터에서 사용되는 것으로 표시됩니다.

**조사**

1. **세부 정보 다운로드**를 클릭하여 관련된 IP 주소의 전체 목록을 봅니다. 하나 또는 두 컴퓨터의 IP 주소가 크기가 작은 DHCP 풀(예: VPN 또는 WiFi)에서 할당된 서브넷에 속해 있나요? IP 주소가 공유되어 있나요? 예를 들어 NAT 장치에서? 이러한 질문들 중 하나에 대한 대답이 '예'이면 거짓 긍정입니다.

2. 사용자를 대신하여 티켓을 전달하는 사용자 지정 응용 프로그램이 있나요? 그러한 경우 무해한 참 긍정입니다.

**수정**

1. 관련된 계정이 중요하지 않으면 해당 계정의 암호를 다시 설정합니다. 이렇게 하면 공격자가 암호 해시에서 새 Kerberos 티켓을 만들지 못하게 하지만, 기존 티켓은 만료될 때까지 계속 사용할 수 있습니다.  

2. 중요한 계정인 경우 의심스러운 골든 티켓 활동과 마찬가지로 KRBTGT 계정을 두 번 다시 설정해야 합니다. KRBTGT를 두 번 다시 설정하면 이 도메인의 모든 Kerberos 티켓이 무효화되므로 그렇게 되기 전에 계획을 세웁니다. [고객을 위해 사용할 수 있는 KRBTGT 계정 암호 재설정 스크립트(영문)](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/)의 지침을 참조하고, [KRBTGT 계정 암호/키 도구 재설정(영문)](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51) 사용도 참조하세요.  이는 측면 확대 기술이므로 [Pass-the-Hash 권장 사항(영문)](http://aka.ms/PtH)의 모범 사례를 따릅니다.

## <a name="malicious-data-protection-private-information-request"></a>악성 데이터 보호 개인 정보 요청

**설명**

DPAPI(데이터 보호 API)는 Windows에서 브라우저, 암호화된 파일 및 기타 중요한 데이터에서 저장된 암호를 안전하게 보호하기 위해 사용됩니다. 도메인 컨트롤러에는 도메인에 가입된 Windows 컴퓨터에서 DPAPI로 암호화된 모든 비밀을 해독하는 데 사용할 수 있는 백업 마스터 키가 있습니다. 공격자는 이 마스터 키를 사용하여 도메인에 가입된 모든 컴퓨터에서 DPAPI로 보호되는 모든 비밀을 해독할 수 있습니다.
이 검색에서 DPAPI를 사용하여 백업 마스터 키를 검색하면 경고가 트리거됩니다.

**조사**

1. 원본 컴퓨터에서 Active Directory에 대해 조직에서 승인한 고급 보안 스캐너를 실행하고 있나요?

2. 그렇게 하고 항상 실행하는 경우 의심스러운 활동을 **닫고 제외합니다**.

3. 그렇게 하고 항상 실행하지 않는 경우 의심스러운 활동을 **닫습니다**.

**수정**

DPAPI를 사용하려면 공격자에 도메인 관리자 권한이 필요합니다. [Pass-the-Hash 권장 사항(영문)](http://aka.ms/PtH)을 구현합니다.

## <a name="malicious-replication-requests"></a>악의적인 복제 요청


**설명**

Active Directory 복제는 한 도메인 컨트롤러에서 변경된 내용을 다른 모든 도메인 컨트롤러와 동기화하는 프로세스입니다. 필요한 권한이 부여되면 공격자가 암호 해시를 포함하여 Active Directory에 저장된 데이터를 검색할 수 있도록 복제 요청을 시작할 수 있습니다.

이 검색에서 도메인 컨트롤러가 아닌 컴퓨터에서 복제 요청을 시작하면 경고가 트리거됩니다.

**조사**

1. 의심스러운 컴퓨터가 도메인 컨트롤러인가요? 예를 들어 복제 문제가 있는 새로 승격된 도메인 컨트롤러가 있습니다. 그러한 경우 의심스러운 활동을 **닫고 제외합니다**.  

2. 의심스러운 컴퓨터가 Active Directory에서 데이터를 복제할 수 있나요? 예를 들어 Azure AD Connect가 있습니다. 그러한 경우 의심스러운 활동을 **닫고 제외합니다**.

**수정**

다음 사용 권한을 확인합니다. 

- 디렉터리 변경 내용 복제   

- 모든 디렉터리 변경 내용 복제  

자세한 내용은 [SharePoint Server 2013에서 프로필 동기화에 대한 Active Directory Domain Services 사용 권한 부여](https://technet.microsoft.com/library/hh296982.aspx)를 참조하세요.
[AD ACL 스캐너](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/)를 활용하거나 PowerShell 스크립트를 만들어 이러한 사용 권한을 가진 도메인 사용자를 확인할 수 있습니다.

## <a name="massive-object-deletion"></a>대규모 개체 삭제

**설명**

일부 시나리오에서는 공격자가 정보를 도용하는 대신 DoS(서비스 거부) 공격을 수행합니다. 많은 수의 계정을 삭제하는 것이 하나의 DoS 기술입니다.

이 검색에서 모든 계정의 5% 이상이 삭제되면 경고가 트리거됩니다. 검색하려면 삭제된 개체 컨테이너에 대한 읽기 권한이 필요합니다.  
삭제된 개체 컨테이너에 대해 읽기 전용 권한을 구성하는 방법에 대한 자세한 내용은 [디렉터리 개체에 대한 사용 권한 보기 또는 설정(영문)](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx)에서 **삭제된 개체 컨테이너에 대한 사용 권한 변경**을 참조하세요.

**조사**

삭제된 계정 목록을 검토하고 이러한 대규모 삭제를 정당화할 수 있는 패턴 또는 비즈니스 이유가 있는지 알아봅니다.

**수정**

Active Directory에서 계정을 삭제할 수 있는 사용자에 대한 권한을 제거합니다. 자세한 내용은 [디렉터리 개체에 대한 사용 권한 보기 또는 설정(영문)](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx)을 참조하세요.

## <a name="privilege-escalation-using-forged-authorization-data"></a>위조된 권한 부여 데이터를 통한 권한 상승

**설명**

이전 버전의 Windows Server에서 알려진 취약성으로 인해 공격자가 사용자 권한 부여 데이터가 포함된 Kerberos 티켓의 필드인 PAC(Privileged Attribute Certificate)(Active Directory에서는 그룹 멤버 자격임)를 조작하여 공격자에게 추가 권한을 부여할 수 있습니다.

**조사**

1. 해당 경고를 클릭하여 세부 정보 페이지로 이동합니다.

2. 대상 컴퓨터(**액세스됨** 열 아래)에 MS14-068(도메인 컨트롤러) 또는 MS11-013(서버)이 패치되어 있나요? 그러한 경우 의심스러운 활동을 **닫습니다**(거짓 긍정).

3. 그렇지 않은 경우 원본 컴퓨터(**FROM** 열 아래)에서 PAC를 수정하는 것으로 알려진 OS/응용 프로그램을 실행하나요? 그러한 경우 의심스러운 활동을 **표시하지 않습니다**(무해한 참 긍정).

4. 위의 두 질문에 대한 대답이 '아니요'인 경우 악의적이라고 가정합니다.

**수정**

Windows Server 2012 R2까지의 운영 체제를 사용하는 모든 도메인 컨트롤러에 [KB3011780](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privilege)이 설치되어 있고 2012 R2까지 모든 구성원 서버 및 도메인 컨트롤러가 KB2496930으로 최신 상태인지 확인합니다. 자세한 내용은 [실버 PAC](https://technet.microsoft.com/library/security/ms11-013.aspx) 및 [위조된 PAC](https://technet.microsoft.com/library/security/ms14-068.aspx)를 참조하세요.

## <a name="reconnaissance-using-directory-services-queries"></a>디렉터리 서비스 쿼리를 사용한 정찰

**설명**

디렉터리 서비스 정찰은 공격자가 디렉터리 구조를 매핑하고 공격 이후의 단계를 위해 권한 있는 계정을 대상으로 지정하는 데 사용됩니다. SAM-R(보안 계정 관리자 원격) 프로토콜은 이러한 매핑을 수행하기 위해 디렉터리 쿼리에 사용되는 방법 중 하나입니다.

이 검색에서는 ATA가 배포된 후 첫 번째 달에 경고가 표시되지 않습니다. 학습 기간 동안 SAM-R에서 쿼리하는 컴퓨터의 ATA 프로필은 중요한 계정의 열거형 쿼리와 개별 쿼리 모두를 통해 만들어집니다.

**조사**

1. 해당 경고를 클릭하여 세부 정보 페이지로 이동합니다. 수행된 쿼리(예: 엔터프라이즈 관리자 또는 관리자)와 성공했는지 여부를 확인합니다.

2. 이러한 쿼리는 의심스러운 원본 컴퓨터에서 만들 수 있나요?

3. 그렇게 하고 경고가 업데이트되는 경우 의심스러운 활동을 **표시하지 않습니다**.

4. 그렇게 하고 더 이상 업데이트되지 않는 경우 의심스러운 활동을 **닫습니다**.

5. 관련된 계정에 대한 정보가 있는 경우 해당 계정에서 이러한 쿼리를 만들 수 있나요? 아니면 해당 계정에서 원본 컴퓨터에 정상적으로 로그인하나요?

 - 그렇게 하고 경고가 업데이트되는 경우 의심스러운 활동을 **표시하지 않습니다**.

 - 그렇게 하고 더 이상 업데이트되지 않는 경우 의심스러운 활동을 **닫습니다**.

 - 위의 모든 질문에 대한 대답이 '아니요'인 경우 악의적이라고 가정합니다.

**수정**

[SAMRi10 도구](https://gallery.technet.microsoft.com/SAMRi10-Hardening-Remote-48d94b5b)를 사용하여 이 기술에 대한 환경을 강화합니다.

## <a name="reconnaissance-using-dns"></a>DNS를 사용하여 정찰

**설명**

DNS 서버에는 네트워크의 모든 컴퓨터, IP 주소 및 서비스로 구성된 맵이 포함되어 있습니다. 이 정보는 공격자가 네트워크 구조를 매핑하고 공격의 이후 단계를 위해 적절한 컴퓨터를 대상으로 지정하는 데 사용됩니다.

DNS 프로토콜에는 여러 가지 쿼리 유형이 있습니다. ATA는 DNS가 아닌 서버에서 시작하는 AXFR(전송) 요청을 검색합니다.

**조사**

1. 원본 컴퓨터(**...에서 시작**)가 DNS 서버인가요? 그러한 경우 거짓 긍정일 것입니다. 확인하려면 해당 경고를 클릭하여 세부 정보 페이지로 이동합니다. 테이블의 **쿼리** 아래에서 쿼리된 도메인을 확인합니다. 기존 도메인인가요? 그러한 경우 의심스러운 활동을 **닫습니다**(거짓 긍정). 또한 향후의 거짓 긍정을 방지하기 위해 ATA 게이트웨이와 원본 컴퓨터 사이에 53 UDP 포트가 열려 있는지 확인합니다.

2. 원본 컴퓨터에서 보안 스캐너를 실행하고 있나요? 그러한 경우 ATA에서 **닫기 및 제외**를 직접 사용하거나 **제외** 페이지(ATA 관리자가 사용할 수 있는 **구성** 아래)를 통해 **엔터티를 제외합니다**.

3. 위의 모든 질문에 대한 대답이 '아니요'인 경우 악의적이라고 가정합니다.

**수정**

영역 전송을 사용하지 않도록 설정하거나 지정된 IP 주소로만 제한하여 DNS를 사용한 정찰이 발생하지 않도록 내부 DNS 서버의 보안을 설정할 수 있습니다. 영역 전송 제한에 대한 자세한 내용은 [영역 전송 제한(영문)](https://technet.microsoft.com/library/ee649273(v=ws.10).aspx)을 참조하세요.
영역 전송 수정은 [내부 및 외부의 모든 공격으로부터 DNS 서버를 보호](https://technet.microsoft.com/library/cc770432(v=ws.11).aspx)하기 위해 처리해야 하는 검사 목록의 작업 중 하나입니다.

## <a name="reconnaissance-using-smb-session-enumeration"></a>SMB 세션 열거를 사용한 정찰


**설명**

SMB(서버 메시지 블록) 열거를 통해 공격자는 사용자가 최근에 로그온한 위치에 대한 정보를 얻을 수 있습니다. 공격자가 이 정보를 갖게 되면 네트워크에서 가로로 이동하여 중요한 특정 계정으로 이동할 수 있습니다.

이러한 활동은 발생되지 않아야 하므로 이 검색에서 도메인 컨트롤러에 대해 SMB 세션 열거를 수행하면 경고가 트리거됩니다.

**조사**

1. 해당 경고를 클릭하여 세부 정보 페이지로 이동합니다. 있는 경우 작업을 수행한 계정과 노출된 계정을 확인합니다.

 - 원본 컴퓨터에서 실행 중인 보안 스캐너가 있나요? 그러한 경우 의심스러운 활동을 **닫고 제외합니다**.

2. 관련된 사용자가 작업을 수행했는지 확인합니다. 이러한 사용자가 원본 컴퓨터에 정상적으로 로그인하나요? 아니면 그러한 작업을 수행해야 하는 관리자인가요?  

3. 그렇게 하고 경고가 업데이트되는 경우 의심스러운 활동을 **표시하지 않습니다**.  

4. 그렇게 하고 더 이상 업데이트되지 않는 경우 의심스러운 활동을 **닫습니다**.

5. 위의 모든 질문에 대한 대답이 '아니요'인 경우 악의적이라고 가정합니다.

**수정**

[Net Cease 도구](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b)를 사용하여 이 공격으로부터 사용자 환경을 강화합니다.

## <a name="remote-execution-attempt-detected"></a>원격 실행 시도 검색됨

**설명**

관리자 자격 증명을 손상시키거나 0일 익스플로잇을 사용하는 공격자가 도메인 컨트롤러에서 원격 명령을 실행할 수 있습니다. 지속성 유지, 정보 수집, DoS(서비스 거부) 공격 등의 이유로 사용될 수 있습니다. ATA에서 PSexec 및 원격 WMI 연결을 검색합니다.

**조사**

1. 도메인 컨트롤러에 대한 관리 작업을 수행하는 IT 팀 멤버 또는 서비스 계정에 일반적인 작업입니다. 그러한 경우 동일한 관리자 및/또는 컴퓨터에서 해당 작업을 수행한 이후에 경고가 업데이트되면 경고를 **표시하지 않습니다**.

2. 의심스러운 **컴퓨터**에서 도메인 컨트롤러에 대해 이 원격 실행을 수행할 수 있나요?

 - 의심스러운 **계정**에서 도메인 컨트롤러에 대해 이 원격 실행을 수행할 수 있나요?

 - 두 질문에 대한 답이 모두 *예*인 경우 경고를 **닫습니다**.

3. 두 질문 중 하나에 대한 답이 *아니요*인 경우 참 긍정으로 간주됩니다.

**수정**

1. 비계층 0 컴퓨터에서 도메인 컨트롤러에 대한 원격 액세스를 제한합니다.

2. 강화된 컴퓨터만 관리자에 대한 도메인 컨트롤러에 연결할 수 있도록 [권한 있는 액세스](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access)를 구현합니다.

## <a name="sensitive-account-credentials-exposed--services-exposing-account-credentials"></a>노출된 중요한 계정 자격 증명 및 계정 자격 증명을 노출하는 서비스

**설명**

일부 서비스에서는 계정 자격 증명을 일반 텍스트로 보냅니다. 이 경우는 중요한 계정에서도 발생할 수 있습니다. 트래픽을 모니터링하는 공격자가 악의적인 목적으로 이러한 자격 증명을 다시 사용할 수 있습니다. 중요한 계정에 대한 모든 일반 텍스트 암호의 경우 경고를 트리거하지만, 중요하지 않은 계정의 경우 5개 이상의 다른 계정에서 동일한 원본 컴퓨터의 일반 텍스트 암호를 보내는 경우 경고가 트리거됩니다. 

**조사**

해당 경고를 클릭하여 세부 정보 페이지로 이동합니다. 노출된 계정을 확인합니다. 그러한 계정이 많은 경우 **세부 정보 다운로드**를 클릭하여 Excel 스프레드시트의 목록을 봅니다.

일반적으로 LDAP 단순 바인딩을 사용하는 원본 컴퓨터에는 스크립트 또는 레거시 응용 프로그램이 있습니다.

**수정**

원본 컴퓨터의 구성을 확인하고 LDAP 단순 바인딩을 사용하지 않도록 합니다. LDAP 단순 바인딩을 사용하는 대신 LDAP SALS 또는 LDAPS를 사용할 수 있습니다.

## <a name="suspicious-authentication-failures"></a>의심스러운 인증 실패

**설명**

무차별 대입 공격의 경우 공격자가 하나 이상의 계정에 대해 올바른 암호를 찾을 때까지 다른 계정에 대해 여러 다른 암호로 인증을 시도합니다. 일단 찾았으면 공격자가 해당 계정을 사용하여 로그인할 수 있습니다.

이 검색에서 많은 인증 실패가 발생하면 경고가 트리거됩니다. 이는 여러 사용자 간에 작은 암호 집합을 사용하는 '가로로'이거나 소수의 사용자만 큰 암호 집합을 사용하는 '세로로'이며, 이 두 가지 옵션을 조합하여 사용할 수도 있습니다.

**조사**

1. 관련된 계정이 많은 경우 **세부 정보 다운로드**를 클릭하여 Excel 스프레드시트의 목록을 봅니다.

2. 해당 경고를 클릭하여 세부 정보 페이지로 이동합니다. 로그인 시도가 성공적인 인증으로 완료되었는지 확인합니다. 이러한 시도는 인포그래픽의 오른쪽에 **추측된 계정**으로 표시됩니다. 그러한 경우 **추측된 계정**이 원본 컴퓨터에서 일반적으로 사용되는 계정인가요? 그렇다면 의심스러운 활동을 **표시하지 않습니다**.

3. **추측된 계정**이 없으면 원본 컴퓨터에서 일반적으로 사용되는 **공격받은 계정**인가요? 그렇다면 의심스러운 활동을 **표시하지 않습니다**.

**수정**

[복잡하고 긴 암호](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy)는 무차별 암호 대입 공격에 대한 첫 번째 수준의 보안을 제공합니다.

## <a name="suspicion-of-identity-theft-based-on-abnormal-behavior"></a>비정상적인 동작에 따른 ID 도용 의심

**설명**

ATA는 가변적인 3주 동안 사용자, 컴퓨터 및 리소스에 대한 엔터티 동작을 확인합니다. 동작 모델은 엔터티에서 로그인한 컴퓨터, 엔터티에서 액세스를 요청한 리소스 및 이러한 작업이 수행된 시간과 같은 활동을 기반으로 합니다. 기계 학습 알고리즘에 기반한 엔터티의 동작에서 벗어나는 경우 ATA에서 경고를 보냅니다. 

**조사**

1. 의심스러운 사용자가 이러한 작업을 수행할 수 있나요?

2. 휴가에서 돌아온 사용자, 업무의 일부로 과도한 액세스를 수행하는 IT 직원(예: 특정 일 또는 주에 지원 센터의 지원 급증), 원격 데스크톱 응용 프로그램과 함께 경고를 **닫고 제외**할 때 사용자가 더 이상 검색에 참여하지 않는 경우를 잠재적인 거짓 긍정으로 간주합니다.


**수정**

이러한 비정상적인 동작이 발생한 원인에 따라 별도의 작업을 수행해야 합니다. 예를 들어 이러한 동작이 네트워크 검색으로 인해 발생하면 해당 컴퓨터가 네트워크에서 차단되어야 합니다(승인된 경우는 제외).

## <a name="unusual-protocol-implementation"></a>비정상적인 프로토콜 구현


**설명**

공격자가 표준이 아닌 방식으로 다양한 프로토콜(SMB, Kerberos, NTLM)을 구현하는 도구를 사용합니다. 이러한 유형의 네트워크 트래픽은 일반적으로 Windows에서 경고 없이 허용되지만, ATA에서는 잠재적인 악의적 의도를 인식할 수 있습니다. 이 동작은 Over-Pass-the-Hash 및 무차별 대입 공격과 같은 기술뿐만 아니라 WannaCry와 같은 고급 랜섬웨어에서 사용되는 악용도 나타냅니다.

**조사**

비정상적인 프로토콜 확인 - 의심스러운 활동 타임라인에서 의심스러운 활동을 클릭하여 세부 정보 페이지로 이동합니다. 프로토콜(Kerberos 또는 NTLM)이 화살표 위에 표시됩니다.

- **Kerberos**: Mimikatz와 같은 해킹 도구가 사용되어 잠재적으로 Overpass-the-Hash 공격을 수행하는 경우 이 프로토콜이 자주 트리거됩니다. 원본 컴퓨터에서 Kerberos RFC를 따르지 않고 자체 Kerberos 스택을 구현하는 응용 프로그램을 실행하는지 확인합니다. 그러한 경우 무해한 참 긍정이고 경고를 **닫을** 수 있습니다. 경고가 계속 트리거되고 여전히 이러한 경우이면 경고를 **표시하지 않을** 수 있습니다.

- **NTLM**: WannaCry 또는 Metasploit, Medusa 및 Hydra와 같은 도구일 수 있습니다.  

WannaCry 공격인지 확인하려면 다음 단계를 수행합니다.

1. 원본 컴퓨터에서 Metasploit, Medusa 또는 Hydra와 같은 공격 도구를 실행하고 있는지 확인합니다.

2. 공격 도구가 검색되지 않으면 원본 컴퓨터에서 자체 NTLM 또는 SMB 스택을 구현하는 응용 프로그램을 실행하고 있는지 확인합니다.

3. 그렇지 않은 경우 WannaCry 스캐너 스크립트, 예를 들어 의심스러운 활동과 관련된 원본 컴퓨터에 대해 [이 스캐너](https://github.com/apkjet/TrustlookWannaCryToolkit/tree/master/scanner)를 실행하여 WannaCry가 원인인지 확인합니다. 스캐너에서 컴퓨터가 감염되었거나 취약한 것으로 인식하면 컴퓨터에 패치를 적용하고 맬웨어를 제거하고 네트워크에서 차단합니다.

4. 스크립트에서 컴퓨터가 감염되었거나 취약한 것으로 확인되지 않으면 여전히 감염되어 있을 수 있지만 SMBv1이 비활성화되었거나 컴퓨터에 패치가 적용되어 검색 도구에 영향을 주었을 수도 있습니다.

**수정**

특히 보안 업데이트를 적용하여 모든 컴퓨터에 패치를 적용합니다.

1. [SMBv1을 사용하지 않습니다](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/).

2. [WannaCry를 제거합니다](https://support.microsoft.com/help/890830/remove-specific-prevalent-malware-with-windows-malicious-software-remo).

3. WanaKiwi에서는 사용자가 컴퓨터를 다시 시작하거나 끄지 않은 경우에만 일부 랜섬 소프트웨어의 데이터를 암호 해독할 수 있습니다. 자세한 내용은 [Wanna Cry 랜섬웨어(영문)](https://answers.microsoft.com/en-us/windows/forum/windows_10-security/wanna-cry-ransomware/5afdb045-8f36-4f55-a992-53398d21ed07?auth=1)를 참조하세요.

## <a name="related-videos"></a>관련 동영상
- [보안 커뮤니티에 가입](https://channel9.msdn.com/Shows/Microsoft-Security/Join-the-Security-Community)


## <a name="see-also"></a>참고 항목
- [ATA 의심스러운 활동 플레이북](http://aka.ms/ataplaybook)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [의심스러운 활동 작업](working-with-suspicious-activities.md)
