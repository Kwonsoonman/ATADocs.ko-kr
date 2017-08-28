---
title: "Advanced Threat Analytics 설치 - 7단계 | Microsoft Docs"
description: "ATA 설치의 마지막 단계에서는 허니 토큰 사용자를 구성합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/20/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 527e62553913dc12b2b0d5ff149f765002de7946
ms.sourcegitcommit: 129bee06ff89b72d21b64f9aa0d1a29f66bf9153
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*



# <a name="install-ata---step-7"></a>ATA 설치 - 7단계

>[!div class="step-by-step"]
[« 6단계](install-ata-step6.md)

## <a name="step-7-configure-ip-address-exclusions-and-honeytoken-user"></a>7단계. IP 주소 제외 및 Honeytoken 사용자 구성
ATA를 사용하면 많은 검색에서 특정 IP 주소 또는 사용자를 제외할 수 있습니다. 

예를 들어 한 **DNS 정찰 제외**는 검색 메커니즘으로 DNS를 사용하는 보안 스캐너일 수 있습니다. 이 제외를 통해 ATA에서 이러한 스캐너를 무시할 수 있습니다. *Pass-the-Ticket* 예외의 예로는 NAT 장치가 있습니다.    

ATA에서는 허니 토큰 사용자를 구성하여 악의적인 행위자에 대한 트랩으로 사용됩니다. 즉 경고를 트리거하는 이 계정(일반적으로 유휴 상태)과 연관된 인증이 됩니다.

이를 구성하려면 다음이 단계를 따르세요.

1.  ATA 콘솔에서 설정 아이콘을 클릭하고 **구성**을 선택합니다.

    ![ATA 구성 설정](media/ATA-config-icon.png)

2.  **검색**에서 **일반**을 클릭합니다.

2. **Honeytoken 계정**에서 Honeytoken 계정 이름을 입력합니다. Honeytoken 계정 필드는 검색 가능하며 네트워크의 엔터티를 자동으로 표시합니다.

   ![Honeytoken](media/honeytoken.png)

3. **제외**를 클릭합니다. 각 위협 유형에 대해 이러한 위협의 검색에서 제외할 사용자 계정 또는 IP 주소를 입력하고 *더하기* 기호를 클릭합니다. **엔터티 추가**(사용자 또는 컴퓨터) 필드는 검색 가능하며 해당 필드에 네트워크의 엔터티가 자동으로 채워집니다. 자세한 내용은 [검색에서 엔터티 제외](excluding-entities-from-detections.md)를 참조하세요.

   ![제외](media/exclusions.png)


  > [!NOTE]
  > 사용자에 대한 SID를 찾으려면 ATA 콘솔에서 사용자를 검색한 다음 **계정 정보** 탭을 클릭합니다. 

4.  **저장**을 클릭합니다.


축하합니다. Microsoft Advanced Threat Analytics를 성공적으로 배포했습니다.

공격 타임라인에서 검색된 의심스러운 활동을 보고, 사용자 또는 컴퓨터를 검색하여 해당 프로필을 확인하세요.

ATA는 즉시 의심스러운 활동에 대한 검색을 시작합니다. 일부 의심스러운 동작과 같은 일부 활동은 ATA에서 동작 프로필을 작성할 시간(최소 3주)을 소요한 다음에야 사용할 수 있습니다.

ATA이 실행되고 네트워크에서 위반을 catch하는지 확인하려면 [ATA 공격 시뮬레이션 플레이북](https://docs.microsoft.com/enterprise-mobility-security/solutions/ata-attack-simulation-playbook)을 확인할 수 있습니다.


>[!div class="step-by-step"]
[« 6단계](install-ata-step6.md)



## <a name="related-videos"></a>관련 동영상
- [올바른 ATA 게이트웨이 유형 선택](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>참고 항목
- [ATA POC 배포 가이드](http://aka.ms/atapoc)
- [ATA 크기 조정 도구](http://aka.ms/atasizingtool)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [이벤트 수집 구성](configure-event-collection.md)
- [ATA 필수 구성 요소](ata-prerequisites.md)

