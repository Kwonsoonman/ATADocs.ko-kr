---
title: "Advanced Threat Analytics 설치 - 7단계 | Microsoft Docs"
description: "이 ATA 설치 단계에서는 VPN을 통합합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 09/19/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e0aed853-ba52-46e1-9c55-b336271a68e7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 384384ebd6b6fadcaa5636200ccd08667d9c41a5
ms.sourcegitcommit: 34c3d6f56f175994b672842c7576040956ceea69
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*



# <a name="install-ata---step-7"></a>ATA 설치 - 7단계

>[!div class="step-by-step"]
[« 5단계](install-ata-step5.md)
[8단계 »](install-ata-step7.md)

## <a name="step-7-integrate-vpn"></a>7단계. VPN 통합

### <a name="configuring-vpn"></a>VPN 구성

ATA는 컴퓨터를 네트워크에 연결하는 위치를 프로파일링하는 데 도움이 되고 비정상적인 VPN 연결을 검색할 수 있는 VPN 데이터를 수집합니다.

ATA에서 VPN 데이터를 구성하려면 다음과 같이 합니다.

1. **구성**으로 이동한 다음 **VPN** 탭을 클릭합니다.

2. RADIUS 서버의 **계정 공유 암호**를 입력합니다. 공유 암호를 가져오려면 VPN 설명서를 참조하세요.

 ![ATA VPN 구성](media/vpn.png)

3.  ATA VPN을 사용하도록 설정하면 모든 ATA 게이트웨이 및 경량 게이트웨이가 RADIUS 계정 이벤트에 대해 1813 포트에서 수신합니다. 

4.  VPN의 RADIUS 계정 이벤트는 구성된 후 모든 ATA 게이트웨이 또는 ATA 경량 게이트웨이로 전달되어야 합니다.

5.  ATA 게이트웨이에서 VPN 이벤트를 수신하고 처리를 위해 ATA 센터로 보낸 후 ATA 센터는 HTTPS 포트 443에서 지리적 위치에 대해 VPN 이벤트의 외부 IP 주소를 확인할 수 있도록 인터넷 연결이 필요합니다.

위치에 대한 외부 IP 주소를 확인하는 호출은 익명입니다. 이 호출에서는 개인 식별자가 전송되지 않습니다.

지원되는 VPN 공급업체는 다음과 같습니다.
- Microsoft
- F5
- Check Point
- Cisco ASA




>[!div class="step-by-step"]
[« 6단계](install-ata-step5.md)
[8 단계»](install-ata-step7.md)



## <a name="related-videos"></a>관련 동영상
- [올바른 ATA 게이트웨이 유형 선택](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>참고 항목
- [ATA POC 배포 가이드](http://aka.ms/atapoc)
- [ATA 크기 조정 도구](http://aka.ms/atasizingtool)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [이벤트 수집 구성](configure-event-collection.md)
- [ATA 필수 구성 요소](ata-prerequisites.md)

