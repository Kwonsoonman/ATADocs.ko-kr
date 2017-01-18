---
title: "ATA 설치 | Microsoft 문서"
description: "ATA 설치의 마지막 단계에서는 허니 토큰 사용자를 구성합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 09/20/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 85e285c5d88e5916e0bf0eb7dd327cb4cb45b4cb
ms.openlocfilehash: 17833f000135337fce82d69efb63fc6e1f9ea307


---

*적용 대상: Advanced Threat Analytics 버전 1.7*



# <a name="install-ata---step-6"></a>ATA 설치 - 6단계

>[!div class="step-by-step"]
[« 5단계](install-ata-step5.md)

## <a name="step-6-configure--ip-address-exclusions-and-honeytoken-user"></a>6단계. IP 주소 제외 및 허니 토큰 사용자 구성
ATA에서는 **DNS 정찰** 및 **Pass-the-Ticket** 두 가지 유형의 검색에서 특정 IP 주소를 제외할 수 있습니다. 

예를 들어 한 **DNS 정찰 제외**는 검색 메커니즘으로 DNS를 사용하는 보안 스캐너일 수 있습니다. 이 제외를 통해 ATA에서 이러한 스캐너를 무시할 수 있습니다. *Pass-the-Ticket* 예외의 예로는 NAT 장치가 있습니다.    

ATA에서는 허니 토큰 사용자를 구성하여 악의적인 행위자에 대한 트랩으로 사용됩니다. 즉 경고를 트리거하는 이 계정(일반적으로 유휴 상태)과 연관된 인증이 됩니다.

이를 구성하려면 다음이 단계를 따르세요.

1.  ATA 콘솔에서 설정 아이콘을 클릭하고 **구성**을 선택합니다.

    ![ATA 구성 설정](media/ATA-config-icon.JPG)

2.  **검색 제외**에서 *DNS 정찰* 또는 *Pass-the-Ticket*에 대한 IP 주소를 입력하고 *더하기* 기호를 클릭합니다.

    ![변경 내용 저장](media/ATA-exclusions.png)

3.  **Detection settings**(감지 설정)에서 허니 토큰 계정 SID를 입력하고 더하기 기호를 클릭합니다. 예: `S-1-5-21-72081277-1610778489-2625714895-10511`.

    ![ATA 구성 설정](media/ATA-honeytoken.png)

    > [!NOTE]
    > 사용자에 대한 SID를 찾으려면 ATA 콘솔에서 사용자를 검색한 다음 **계정 정보** 탭을 클릭합니다. 

4.  **저장**을 클릭합니다.


축하합니다. Microsoft Advanced Threat Analytics를 성공적으로 배포했습니다.

공격 타임라인에서 검색된 의심스러운 활동을 보고, 사용자 또는 컴퓨터를 검색하여 해당 프로필을 확인하세요.

ATA는 즉시 의심스러운 활동에 대한 검색을 시작합니다. 일부 의심스러운 동작과 같은 일부 활동은 ATA에서 동작 프로필을 작성할 시간(최소 3주)을 소요한 다음에야 사용할 수 있습니다.


>[!div class="step-by-step"]
[« 5단계](install-ata-step5.md)


## <a name="see-also"></a>참고 항목

- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [이벤트 수집 구성](configure-event-collection.md)
- [ATA 필수 구성 요소](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Jan17_HO1-->


