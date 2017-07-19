---
title: "Advanced Threat Analytics 설치 - 4단계 | Microsoft 문서"
description: "ATA 설치 4단계에서는 ATA Gateway를 설치합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/18/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 6bbc50c3-bfa8-41db-a2f9-56eed68ef5d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 2713f6939c8756d0ecb438e866e6649f13d3c490
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/30/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*



# <a name="install-ata---step-4"></a>ATA 설치 - 4단계

>[!div class="step-by-step"]
[« 3단계](install-ata-step3.md)
[5단계 »](install-ata-step5.md)

## <a name="step-4-install-the-ata-gateway"></a>4단계. ATA Gateway 설치

전용 서버에 ATA Gateway를 설치하기 전에 포트 미러링이 올바르게 구성되어 있는지와 ATA Gateway에서 도메인 컨트롤러로 들어오고 나가는 트래픽을 볼 수 있는지를 확인합니다. 자세한 내용은 [포트 미러링 유효성 검사](validate-port-mirroring.md)를 참조하세요.


> [!IMPORTANT]
> [KB2919355](http://support.microsoft.com/kb/2919355/)가 설치되었는지 확인합니다.  다음 PowerShell cmdlet을 실행하여 핫픽스가 설치되어 있는지 확인합니다.
>
> `Get-HotFix -Id kb2919355`

ATA Gateway 서버에서 다음 단계를 수행합니다.

1.  zip 파일에서 파일을 추출합니다. 
> [!NOTE] 
> Zip 파일에서 직접 설치할 수 없습니다.

2.  **Microsoft ATA Gateway Setup.exe**를 실행하고 설치 마법사를 따릅니다.

3.  **시작** 페이지에서 언어를 선택하고 **다음**을 클릭합니다.

4.  설치 마법사는 서버가 도메인 컨트롤러인지, 전용 서버인지 자동으로 확인합니다. 도메인 컨트롤러인 경우 ATA 경량 게이트웨이가 설치되고, 전용 서버인 경우 ATA 게이트웨이가 설치됩니다. 
    
    예를 들어 ATA 게이트웨이의 경우 전용 서버에 ATA 게이트웨이가 설치된다고 알리는 다음과 같은 화면이 표시됩니다.
    
    ![ATA 게이트웨이 설치](media/ata-gw-install.png) **다음**을 클릭합니다.

    > [!NOTE] 
    > 도메인 컨트롤러 또는 전용 서버가 설치에 대한 최소 하드웨어 요구 사항에 맞지 않으면 경고를 받게 됩니다. 이렇게 해도 **다음**을 클릭하여 설치를 계속할 수 있습니다. 이 ATA 설치 옵션은 데이터 저장소 공간이 충분하지 않은 작은 연구실 테스트 환경에서 적절할 수 있습니다. 프로덕션 환경에서는 ATA의 [용량 계획](ata-capacity-planning.md) 가이드에 따라 작업하여 도메인 컨트롤러 또는 전용 서버가 필수 요구 사항에 맞는지 확인하는 것이 좋습니다.

4.  **게이트웨이 구성**에서 사용자 환경에 따라 다음 정보를 입력합니다.

    ![ATA Gateway 구성 이미지](media/ata-gw-configure.png)

    > [!NOTE]
    > ATA 게이트웨이를 배포할 때는 자격 증명을 제공할 필요가 없습니다. ATA 게이트웨이 설치가 Single Sign-On을 사용하여 자격 증명을 검색하지 못하는 경우(예: 이 문제는 ATA 센터가 도메인에 없는 경우, ATA 게이트웨이가 도메인에 없는 경우 또는 ATA 관리자 자격 증명이 없는 경우에 발생할 수 있음) 다음 화면에서와 같이 자격 증명을 제공하라는 메시지가 표시됩니다. 

  ![ATA 게이트웨이가 자격 증명을 제공합니다.](media/ata-install-credentials.png)

   - 설치 경로: ATA 게이트웨이를 설치할 위치입니다. 기본적으로 %programfiles%\Microsoft Advanced Threat Analytics\Gateway입니다. 기본값을 그대로 둡니다.
    
5. **설치**를 클릭합니다. ATA Gateway 설치 중에 다음 구성 요소가 설치되고 구성됩니다.

    -   KB 3047154(Windows Server 2012 R2만 해당)

        > [!IMPORTANT]
        > -   가상화 호스트에 KB 3047154를 설치하지 마세요(가상화를 실행 중인 호스트, 가상 컴퓨터에서 실행하는 것은 문제 없음). 포트 미러링이 제대로 작동하지 않을 수 있습니다. 
        > -   메시지 분석기, Wireshark 또는 기타 네트워크 캡처 소프트웨어를 ATA Gateway에 설치하지 마세요. 네트워크 트래픽을 캡처해야 하는 경우 Microsoft Network Monitor 3.4를 설치하고 사용합니다.

    -   ATA Gateway 서비스
    -   Microsoft Visual C++ 2013 재배포 가능 패키지
    -   사용자 지정 성능 모니터 데이터 컬렉션 집합

5.  설치가 완료되면 ATA 게이트웨이의 경우 **시작**을 클릭하여 브라우저를 열고 ATA 콘솔에 로그인합니다. ATA 경량 게이트웨이의 경우 **마침**을 클릭합니다.


>[!div class="step-by-step"]
[« 3단계](install-ata-step3.md)
[5단계 »](install-ata-step5.md)

## <a name="see-also"></a>참고 항목

- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [이벤트 수집 구성](configure-event-collection.md)
- [ATA 필수 구성 요소](ata-prerequisites.md)

