---
# required metadata

title: ATA 설치 | Microsoft Advanced Threat Analytics
description: ATA 설치의 마지막 단계에서는 단기 임대 서브넷과 허니토큰 사용자를 구성합니다.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 설치 - 6단계

>[!div class="step-by-step"]
[« 5단계](install-ata-step5.md)

## 6단계. 단기 임대 서브넷 및 허니토큰 사용자 구성
단기 임대 서브넷은 IP 주소 할당이 매우 빠르게(몇 초 내지 몇 분 이내) 변경되는 서브넷입니다. 예를 들어 VPN에 사용되는 IP 주소와 Wi-Fi IP 주소가 여기에 해당합니다. 조직에서 사용되는 단기 임대 서브넷 목록을 입력하려면 다음 단계를 따르세요.

1.  ATA Gateway 컴퓨터의 ATA 콘솔에서 설정 아이콘을 클릭하고 **구성**을 선택합니다.

    ![ATA 구성 설정](media/ATA-config-icon.JPG)

2.  **검색** 아래에서 단기 임대 서브넷에 대해 다음을 입력합니다. 슬래시 표기법 형식(예: `192.168.0.0/24`)을 사용하여 단기 임대 서브넷을 입력하고 더하기 기호를 클릭합니다.

3.  허니토큰 계정 SID에는 네트워크 활동이 없는 사용자의 SID를 입력하고 더하기 기호를 클릭합니다. 예를 들면 `S-1-5-21-72081277-1610778489-2625714895-10511`과 다음과 같습니다.

    > [!NOTE]
    > 사용자의 SID를 찾으려면 Windows PowerShell cmdlet `Get-ADUser UserName`을 실행합니다.

4.  제외를 구성합니다. 특정한 의심스러운 활동에서 제외할 IP 주소를 구성할 수 있습니다. 자세한 내용은 [ATA 검색 설정 작업](working-with-detection-settings.md)을 참조하세요.

5.  **저장**을 클릭합니다.

![변경 내용 저장](media/ATA-VPN-Subnets.JPG)

축하합니다. Microsoft Advanced Threat Analytics를 성공적으로 배포했습니다.

공격 타임라인에서 검색된 의심스러운 활동을 보고, 사용자 또는 컴퓨터를 검색하여 해당 프로필을 확인하세요.

ATA에서 동작 프로필을 만드는 데 최소 3주가 걸리므로 처음 3주 동안에는 의심스러운 동작 활동이 표시되지 않습니다.


>[!div class="step-by-step"]
[« 5단계](install-ata-step5.md)


## 참고 항목

- [지원이 필요한 경우 포럼을 확인하세요.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [이벤트 수집 구성](/advanced-threat-analytics/plandesign/configure-event-collection)
- [ATA 필수 구성 요소](/advanced-threat-analytics/plandesign/ata-prerequisites)


<!--HONumber=Apr16_HO2-->


