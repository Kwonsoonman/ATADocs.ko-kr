---
title: "위조된 PAC 공격 조사 | Microsoft 문서"
description: "이 문서에서는 위조된 PAC 공격을 설명하고 이 위협이 네트워크에서 발견될 경우 조사 지침을 제공합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/16/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: f3db435e-9553-40a2-a2ad-278fad4f0ef5
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 437f387815fbbfbe261a192764a428e0d285ef32
ms.sourcegitcommit: 97aced94f47cf3c1b473d25b77d10a300c3f517e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.7*

# <a name="investigating-forged-pac-attacks"></a>위조된 PAC 공격 조사

Microsoft에서는 보안 검색 기능 및 보안 분석가에게 거의 실시간으로 실행 가능한 정보를 제공하는 기능을 지속적으로 개선합니다. 이러한 변경은 Microsoft ATA(Advanced Threat Analytics)을 기반으로 합니다. ATA가 네트워크에서 위조된 PAC의 의심스러운 활동을 발견하고 이를 경고하면 이 문서를 통해 해당 활동을 파악하고 조사할 수 있습니다.

## <a name="what-is-a-privileged-access-certificate-pac"></a>PAC(Privileged Access Certificate)란?

PAC(Privilege Attribute Certificate)는 그룹 등록, 보안 식별자 및 사용자 프로필 정보를 비롯한 권한 부여 정보를 포함하는 Kerberos 티켓의 데이터 구조입니다. Active Directory 도메인에서는 PAC를 사용하여 DC(도메인 컨트롤러)에서 제공된 권한 부여 데이터를 인증 및 권한 부여 목적으로 다른 멤버 서버 및 워크스테이션으로 전달할 수 있습니다. 등록 정보 이외에 PAC에는 추가 자격 증명 정보, 프로필 및 정책 정보, 지원하는 보안 메타데이터가 포함됩니다. 

PAC 데이터 구조는 인증 프로토콜(ID를 확인하는 프로토콜)에 의해 리소스 액세스를 제어하는 권한 부여 정보를 전송하는 데 사용됩니다.

### <a name="pac-validation"></a>PAC 유효성 검사

PAC 유효성 검사는 특히 사용자 가장이 사용되는 응용 프로그램에서 공격자가 메시지 가로채기(man-in-the-middle) 공격을 통해 시스템 또는 관련 리소스에 대한 무단 액세스 권한을 얻지 못하도록 하는 보안 기능입니다. 가장에는 리소스에 액세스하고 작업을 실행할 상승된 권한이 부여되는 서비스 계정과 같은 신뢰할 수 있는 ID가 포함됩니다. PAC 유효성 검사는 가장이 발생하는 Kerberos 인증 설정에서 더 안전한 권한 부여 환경을 강화합니다. [PAC 유효성 검사](https://blogs.msdn.microsoft.com/openspecification/2009/04/24/understanding-microsoft-kerberos-pac-validation/)에서는 사용자가 Kerberos 티켓에서 부여된 대로 정확한 권한 부여 데이터를 제공하고 티켓의 권한이 수정되지 않았는지 확인합니다.

PAC 유효성 검사가 수행되면 서버에서는 PAC 서명 유형 및 길이가 포함된 요청 메시지를 인코딩하고 이를 DC에 전송합니다. DC에서는 요청을 디코딩하고 서버 체크섬 및 KDC 체크섬 값을 추출합니다. 체크섬 확인에 성공하면 DC에서는 성공 코드를 서버에 반환합니다. 실패 반환 코드는 PAC가 변경되었음을 나타냅니다. 

Kerberos PAC 콘텐츠는 두 번 서명됩니다. 
- 악의적인 서버 쪽 서비스가 권한 부여 데이터를 변경하지 못하도록 KDC의 마스터 키를 사용하여 한 번 서명되고,
- 사용자가 PAC 콘텐츠를 수정하고 자신의 권한 부여 데이터를 추가하지 못하도록 대상 리소스 서버 계정의 마스터 키를 사용하여 한 번 서명됩니다.

### <a name="pac-vulnerability"></a>PAC 취약성
보안 게시판 [MS14-068](https://technet.microsoft.com/library/security/MS14-068.aspx) 및 [MS11-013](https://technet.microsoft.com/library/security/ms11-013.aspx)에서는 공격자가 유효한 Kerberos 티켓에서 PAC 필드를 조작하여 자신들에게 추가 권한을 부여하도록 허용할 수 있는 Kerberos KDC의 취약성을 처리합니다.

## <a name="forged-pac-attack"></a>위조된 PAC 공격

위조된 PAC 공격은 공격자가 이러한 취약성을 이용하여 Active Directory 포리스트 또는 도메인에서 권한을 상승시키려는 시도입니다. 이 공격을 수행하려면 공격자는 다음을 충족해야 합니다.
-    도메인 사용자에 대한 자격 증명이 있어야 합니다.
-    손상된 자격 증명에 대해 인증하는 데 사용될 수 있는 도메인 컨트롤러에 네트워크로 연결되어 있어야 합니다.
-    적합한 도구가 있어야 합니다. PyKEK(Python Kerberos Exploitation Kit)는 PAC를 위조하는 알려진 도구입니다.

공격자에게 필요한 자격 증명과 연결이 있으면 이들은 기존 Kerberos 사용자 로그온 토큰(TGT)의 PAC(Privileged Access Certificate)를 수정하거나 위조할 수 있습니다. 공격자는 그룹 등록 클레임을 변경하여 더 높은 권한이 부여된 그룹(예: “Domain Administrators” 또는 “Enterprise Administrators”)을 포함합니다. 그 다음에 공격자는 수정된 PAC를 Kerberos 티켓에 포함합니다. 이 Kerberos 티켓을 사용하여 패치되지 않은 DC(도메인 컨트롤러)에서 서비스 티켓을 요청하면 도메인 및 권한 부여에서 공격자에게 수행하면 안 되는 작업을 수행할 상승된 권한이 제공됩니다. 공격자는 리소스 액세스 토큰(TGS)을 요청하여 도메인의 모든 리소스에 대한 액세스 권한을 얻기 위해 수정된 사용자 로그온 토큰(TGT)을 제공합니다. 이는 공격자가 Active Directory의 모든 사용자에 대한 권한 부여 데이터(PAC)를 위장하는 방식으로 네트워크에서 액세스를 제한하는 모든 구성된 리소스 ACL을 무시할 수 있다는 것을 의미합니다.

## <a name="discovering-the-attack"></a>공격 검색
공격자가 권한을 상승시키려고 시도하면 ATA가 이 시도를 검색하고 심각도가 높은 경고로 표시합니다.

![위조된 PAC의 의심스러운 활동](./media/forged-pac.png)

ATA는 의심스러운 활동 경고에 위조된 PAC가 성공 또는 실패했는지 여부를 표시합니다. 실패한 시도는 사용자 환경에 공격자가 있음을 나타낼 수 있기 때문에 성공 및 실패 경고를 둘 다 조사해야 합니다.

## <a name="investigating"></a>조사
ATA에서 위조된 PAC 경고를 받은 후에는 공격을 최소화하기 위해 수행해야 할 작업을 결정해야 합니다. 이 작업을 하려면 먼저 경고를 다음 중 하나로 분류해야 합니다. 
-    True Positive: ATA가 발견한 악의적인 작업
-    False Positive: 거짓 경고 - 위조된 PAC가 실제로 발생하지 않음(ATA가 위조된 PAC 공격을 잘못 검색한 이벤트)
-    Benign True Positive: ATA가 발견한, 침투 테스트와 같이 실재하지만 악의적이지 않은 작업

다음 차트를 사용하여 수행해야 하는 단계를 결정할 수 있습니다.

![위조된 PAC 다이어그램](./media/forged-pac-diagram.png)

1. 먼저 ATA 공격 시간 표시 막대에서 경고를 확인하여 위조된 권한 부여 시도가 성공 또는 실패하거나 시도되었는지 확인합니다(시도된 공격도 실패한 공격임). 성공한 시도와 실패한 시도는 둘 다 True Positive가 되지만 환경 내에서의 심각도는 다릅니다.
 
 ![위조된 PAC의 의심스러운 활동](./media/forged-pac-sa.png)


2.    발견된 위조된 PAC 공격이 성공한 경우:
    -    경고가 발생한 DC가 제대로 패치되면 False Positive입니다. 이 경우 경고를 해제하고 검색을 지속적으로 개선할 수 있도록 ATAEval@microsoft.com의 ATA 팀에게 알리는 메일을 보내야 합니다. 
    -    경고의 DC가 제대로 패치되지 않은 경우:
        -    경고에 나열된 서비스에 자체 권한 부여 메커니즘이 없으면 True Positive이고 조직의 IR(인시던트 응답) 프로세스를 실행해야 합니다. 
        -    경고에 나열된 서비스에 권한 부여 데이터를 요청하는 내부 권한 부여 메커니즘이 있으면 위조된 PAC로 거짓으로 식별될 수 있습니다. 

3.    발견된 공격이 실패한 경우:
    -    PAC를 수정할 운영 체제 또는 응용 프로그램이 알려지면 Benign True Positive일 수 있고 응용 프로그램 또는 운영 체제 소유자와 함께 이 동작을 수정해야 합니다.

    -    PAC를 수정할 운영 체제 또는 응용 프로그램이 알려지지 않은 경우: 

        -    나열된 서비스에 자체 권한 부여 서비스가 없으면 True Positive이고 조직의 IR(인시던트 응답) 프로세스를 실행해야 합니다. 공격자가 도메인에서 권한을 상승시키는 데 실패하더라도 사용자는 네트워크에 공격자가 있는 것으로 추정할 수 있고 이들이 권한을 상승시키기 위해 다른 알려진 끈질긴 사전 공격을 시도하기 전에 가능한 한 빠르게 찾으려고 합니다. 
        -    경고에 나열된 서비스에 권한 부여 데이터를 요청하는 자체 권한 부여 메커니즘이 있으면 위조된 PAC로 거짓으로 식별될 수 있습니다.


Microsoft 계정 팀을 통해 연락할 수 있는 전문 인시던트 응답 및 복구 팀의 지원을 받아 공격자가 네트워크에 지속성 방법을 배포했는지 검색하는 것이 좋습니다. 이러한 공격은 악의적인 소프트웨어를 통해서나 분실된 자격 증명 및 Golden Ticket과 같은 ID 위반을 통해 이루어질 수 있습니다.


## <a name="see-also"></a>참고 항목
- [의심스러운 활동 작업](working-with-suspicious-activities.md)
- [ATA 구성 수정](modifying-ata-configuration.md)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
