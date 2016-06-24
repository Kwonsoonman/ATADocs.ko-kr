---
# required metadata

title: ATA 설치 - 4단계 | Microsoft Advanced Threat Analytics
description: ATA 설치 4단계에서는 ATA Gateway를 설치합니다.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 6bbc50c3-bfa8-41db-a2f9-56eed68ef5d2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 설치 - 4단계

>[!div class="step-by-step"]
[« 3단계](install-ata-step3.md)
[5단계 »](install-ata-step5.md)

## 4단계. ATA Gateway 설치
ATA Gateway를 설치하기 전에 포트 미러링이 올바르게 구성되어 있는지와 ATA Gateway에서 도메인 컨트롤러로 들어오고 나가는 트래픽을 볼 수 있는지를 확인합니다. 자세한 내용은 [포트 미러링 유효성 검사](/advanced-threat-analytics/plandesign/validate-port-mirroring)를 참조하세요.

> [!IMPORTANT]
> [KB2919355](http://support.microsoft.com/kb/2919355/)가 설치되었는지 확인합니다.  다음 PowerShell cmdlet을 실행하여 핫픽스가 설치되어 있는지 확인합니다.
>
> `Get-HotFix -Id kb2919355`

ATA Gateway 서버에서 다음 단계를 수행합니다.

1.  zip 파일에서 파일을 추출합니다.

2.  관리자 명령 프롬프트에서 Microsoft ATA Gateway Setup.exe를 실행하고 설치 마법사를 따릅니다.

3.  **시작** 페이지에서 언어를 선택하고 **다음**을 클릭합니다.

4.  **ATA Gateway 구성** 아래에서 사용자 환경에 따라 다음 정보를 입력합니다.

    ![ATA Gateway 구성 이미지](media/ATA-Gateway-Configuration.JPG)

    |필드|설명|설명|
    |---------|---------------|------------|
    |설치 경로|ATA Gateway를 설치할 위치입니다. 기본적으로 %programfiles%\Microsoft Advanced Threat Analytics\게이트웨이입니다.|기본값을 그대로 둡니다.|
    |ATA Gateway 서비스 SSL 인증서|ATA Gateway에서 사용할 인증서입니다.|자체 서명된 인증서는 랩 환경에만 사용합니다.|
    |ATA Gateway 등록|ATA 관리자의 사용자 이름 및 암호를 입력합니다.|ATA Gateway에서 ATA Center에 등록할 수 있도록 ATA Center를 설치한 사용자의 사용자 이름 및 암호를 입력합니다. 이 사용자는 ATA Center에서 다음 로컬 그룹 중 하나의 구성원이어야 합니다.<br /><br />-   Administrators<br />-   Microsoft Advanced Threat Analytics Administrators **참고:** 이러한 자격 증명은 등록에만 사용되며 ATA에 저장되지 않습니다.|
    ATA Gateway 설치 중에 다음 구성 요소가 설치되고 구성됩니다.

    -   KB 3047154

        > [!IMPORTANT]
        > -   가상화 호스트에 KB 3047154를 설치하지 마세요. 포트 미러링이 제대로 작동하지 않을 수 있습니다.
        > -   메시지 분석기, Wireshark 또는 기타 네트워크 캡처 소프트웨어를 ATA Gateway에 설치하지 마세요. 네트워크 트래픽을 캡처해야 하는 경우 Microsoft Network Monitor 3.4를 설치하고 사용합니다.

    -   ATA Gateway 서비스

    -   Microsoft Visual C++ 2013 재배포 가능 패키지

    -   사용자 지정 성능 모니터 데이터 컬렉션 집합

5.  설치가 완료되면 **시작**을 클릭하여 브라우저를 열고 ATA 콘솔에 로그인합니다.


>[!div class="step-by-step"]
[« 3단계](install-ata-step3.md)
[5단계 »](install-ata-step5.md)

## 참고 항목

- [지원이 필요한 경우 포럼을 확인하세요.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [이벤트 수집 구성](/advanced-threat-analytics/plandesign/configure-event-collection)
- [ATA 필수 구성 요소](/advanced-threat-analytics/plandesign/ata-prerequisites)


<!--HONumber=Apr16_HO2-->


