---
title: "Advanced Threat Analytics 설치 - 7단계 | Microsoft Docs"
description: "이 ATA 설치 단계에서는 VPN을 통합합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 10/31/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e0aed853-ba52-46e1-9c55-b336271a68e7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 748121a709ac05756edf34e04e13b996190e9711
ms.sourcegitcommit: b951c64228d4f165ee1fcc5acc0ad6bb8482d6a2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/31/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*



# <a name="install-ata---step-7"></a>ATA 설치 - 7단계

>[!div class="step-by-step"]
[« 5단계](install-ata-step5.md)
[8단계 »](install-ata-step7.md)

## <a name="step-7-integrate-vpn"></a>7단계. VPN 통합

Microsoft ATA(Advanced Threat Analytics) 버전 1.8에서는 VPN 솔루션의 계정 정보를 수집할 수 있습니다. 구성되면 사용자의 프로필 페이지에는 IP 주소 및 연결이 시작된 위치와 같은 VPN 연결 정보가 포함됩니다. 그러면 사용자 작업에 대한 추가 정보를 제공하여 조사 프로세스를 보완합니다. 위치에 대한 외부 IP 주소를 확인하는 호출은 익명입니다. 이 호출에서는 개인 식별자가 전송되지 않습니다.

ATA는 ATA Gateway로 전달되는 RADIUS 계정 이벤트를 수신하여 VPN 솔루션과 통합합니다. 이 메커니즘은 표준 RADIUS 계정([RFC 2866](https://tools.ietf.org/html/rfc2866))을 기반으로 하며 다음과 같은 VPN 공급 업체가 지원됩니다.

-   Microsoft
-   F5
-   Check Point
-   Cisco ASA

## <a name="prerequisites"></a>전제 조건

VPN 통합을 사용하려면 다음 항목을 설정해야 합니다.

-   ATA Gateways 및 ATA Lightweight Gateways에서 UDP 1813 포트 열기

-   들어오는 IP 주소의 위치를 쿼리할 수 있도록 ATA 센터를 인터넷에 연결

아래 예제에서는 Microsoft RRAS(라우팅 및 원격 액세스 서버)를 사용하여 VPN 구성 프로세스를 설명합니다.

타사 VPN 솔루션을 사용하는 경우 RADIUS 계정을 사용하는 방법에 대한 지침은 해당 설명서를 참조하세요.

## <a name="configure-radius-accounting-on-the-vpn-system"></a>VPN 시스템에서 RADIUS 계정 구성

RRAS 서버에서 다음을 수행합니다.
 
1.  라우팅 및 원격 액세스 콘솔을 엽니다.
2.  서버 이름을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.
3.  **보안** 탭의 **계정 공급자** 아래에서 **RADIUS 계정**을 선택하고 **구성**을 클릭합니다.

    ![RADIUS 설정](./media/radius-setup.png)

4.  **RADIUS 서버 추가** 창에서 가장 가까운 ATA Gateway 또는 ATA Lightweight Gateway의 **서버 이름**을 입력합니다. **포트** 아래에서 1813라는 기본 포트가 구성되어야 합니다. **변경**을 클릭하고 기억할 수 있는 영숫자로 새 공유 암호 문자열을 입력합니다. ATA 구성의 뒷부분에서 입력해야 합니다. **RADIUS 계정 켜기 및 계정 끄기 메시지 보내기** 상자를 확인한 후 모든 열린 대화 상자에서 **확인**을 클릭합니다.
 
     ![VPN 설정](./media/vpn-set-accounting.png)
     
### <a name="configure-vpn-in-ata"></a>ATA에서 VPN 구성

ATA는 컴퓨터를 네트워크에 연결하는 위치를 프로파일링하는 데 도움이 되고 비정상적인 VPN 연결을 검색할 수 있는 VPN 데이터를 수집합니다.

ATA에서 VPN 데이터를 구성하려면 다음과 같이 합니다.

1.  ATA 콘솔에서 ATA 구성 페이지를 열고 **VPN**으로 이동합니다.
 
  ![ATA 구성 메뉴](./media/config-menu.png)

2.  **Radius 계정**을 설정하고, 이전에 RRAS VPN 서버에서 구성한 **공유 암호**를 입력합니다. 그런 다음 **Save**(저장)를 클릭합니다.
 

  ![ATA VPN 구성](./media/vpn.png)


ATA VPN을 사용하도록 설정한 후에 모든 ATA Gateways 및 Lightweight Gateways가 RADIUS 계정 이벤트를 1813 포트에서 수신합니다. 

이제 설정이 완료되면 사용자의 프로필 페이지에 VPN 작업이 표시됩니다.
 
   ![VPN 설정](./media/vpn-user.png)

ATA 게이트웨이에서 VPN 이벤트를 수신하고 처리를 위해 ATA 센터로 보낸 후 ATA 센터는 HTTPS 포트 443에서 지리적 위치에 대해 VPN 이벤트의 외부 IP 주소를 확인할 수 있도록 인터넷 연결이 필요합니다.





>[!div class="step-by-step"]
[« 6단계](install-ata-step5.md)
[8 단계»](install-ata-step7.md)



## <a name="related-videos"></a>관련 동영상
- [ATA 배포 개요](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [올바른 ATA 게이트웨이 유형 선택](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>참고 항목
- [ATA POC 배포 가이드](http://aka.ms/atapoc)
- [ATA 크기 조정 도구](http://aka.ms/atasizingtool)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [이벤트 수집 구성](configure-event-collection.md)
- [ATA 필수 구성 요소](ata-prerequisites.md)

