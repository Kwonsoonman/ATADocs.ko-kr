---
# required metadata

title: ATA 설치 - 1단계 | Microsoft Advanced Threat Analytics
description: ATA를 설치하는 첫 번째 단계에는 ATA Center를 다운로드하여 선택한 서버에 설치하는 과정이 포함됩니다.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 설치 - 1단계

>[!div class="step-by-step"]
[« 설치 전 단계](install-ata-preinstall.md)
[2단계 »](install-ata-step2.md)

## 1단계. ATA Center 다운로드 및 설치
서버가 요구 사항을 충족하는지 확인한 후 ATA Center 설치를 진행할 수 있습니다.

ATA Center 서버에서 다음 단계를 수행합니다.

1.  [TechNet 평가 센터](http://www.microsoft.com/en-us/evalcenter/)에서 ATA를 다운로드합니다.

2.  로컬 관리자 그룹의 구성원인 사용자로 로그인합니다.

3.  관리자 명령 프롬프트에서 Microsoft ATA Center Setup.EXE를 실행하고 설치 마법사를 따릅니다.

4.  **시작** 페이지에서 언어를 선택하고 **다음**을 클릭합니다.

5.  최종 사용자 사용권 계약을 읽고 조건에 동의하는 경우 **다음**을 클릭합니다.

6.  **센터 구성** 페이지에서 사용자 환경에 따라 다음 정보를 입력합니다.

    |필드|설명|설명|
    |---------|---------------|------------|
    |설치 경로|ATA Center를 설치할 위치입니다. 기본적으로 %programfiles%\Microsoft Advanced Threat Analytics\Center입니다.|기본값을 그대로 둡니다.|
    |데이터베이스 데이터 경로|MongoDB 데이터베이스 파일이 있는 위치입니다. 기본적으로 %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data입니다.|크기 조정에 따라 증가할 여유가 있는 곳으로 위치를 변경합니다. **참고:** <ul><li>프로덕션 환경에서는 용량 계획에 따라 충분한 공간이 있는 드라이브를 사용해야 합니다.</li><li>대규모 배포의 경우 데이터베이스는 별도의 물리적 디스크에 있어야 합니다.</li></ul>크기 조정에 대한 자세한 내용은 [ATA 용량 계획](/advanced-threat-analytics/PlanDesign/ata-capacity-planning)을 참조하세요.|
    |데이터베이스 저널 경로|데이터베이스 저널 파일이 있는 위치입니다. 기본적으로 %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data\journal입니다.|대규모 배포의 경우 데이터베이스 저널은 데이터베이스 및 시스템 드라이브와 별도의 물리적 디스크에 있어야 합니다. 데이터베이스 저널에 대한 여유가 있는 곳으로 위치를 변경합니다.|
    |ATA Center 서비스 IP 주소: 포트|ATA Center 서비스가 ATA Gateway 통신을 위해 수신 대기할 IP 주소입니다.<br /><br />**기본 포트:** 443|ATA Center 서비스에서 사용할 IP 주소를 선택하려면 아래쪽 화살표를 클릭합니다.<br /><br />ATA Center 서비스의 IP 주소 및 포트는 ATA 콘솔의 IP 주소 및 포트와 같을 수 없습니다. ATA 콘솔의 포트를 변경해야 합니다.|
    |ATA Center 서비스 SSL 인증서|ATA Center 서비스에서 사용할 인증서입니다.|열쇠 아이콘을 클릭하여 설치된 인증서를 선택하거나, 랩 환경에 배포하는 경우 자체 서명된 인증서를 선택합니다.|
    |ATA 콘솔 IP 주소|ATA 콘솔용 IIS에서 사용할 IP 주소입니다.|ATA 콘솔에서 사용하는 IP 주소를 선택하려면 아래쪽 화살표를 클릭합니다. **참고:** ATA Gateway에서 ATA 콘솔에 보다 쉽게 액세스하려면 이 IP 주소를 적어 두세요.|
    |ATA 콘솔 SSL 인증서|IIS에서 사용할 인증서입니다.|열쇠 아이콘을 클릭하여 설치된 인증서를 선택하거나, 랩 환경에 배포하는 경우 자체 서명된 인증서를 선택합니다.|
    ![ATA Center 구성 이미지](media/ATA-Center-Configuration.JPG)

7.  **설치**를 클릭하여 ATA와 해당 구성 요소를 설치하고 ATA Center와 ATA 콘솔 간의 연결을 만듭니다.

8.  설치가 완료되면 **시작**을 클릭하여 ATA 콘솔에 연결합니다.

    ATA Center 설치 중에 다음 구성 요소가 설치되고 구성됩니다.

    -   IIS(인터넷 정보 서비스)

    -   MongoDB

    -   ATA Center 서비스 및 ATA 콘솔 IIS 사이트

    -   사용자 지정 성능 모니터 데이터 컬렉션 집합

    -   자체 서명된 인증서(설치 중에 선택한 경우)

> [!NOTE]
> 문제 해결 및 제품 향상을 지원하려면 MongoVue 또는 기타 MongoDB 추가 기능을 설치하거나 원하는 다른 타사 도구를 설치하는 것이 좋습니다. MongoVue를 사용하려면 .Net Framework 3.5를 설치해야 합니다.

### 설치 유효성 검사

1.  Microsoft Advanced Threat Analytics Center 서비스가 실행 중인지 확인합니다.

2.  바탕 화면에서 Microsoft Advanced Threat Analytics 바로 가기를 클릭하여 ATA 콘솔에 연결합니다. ATA Center를 설치하는 데 사용한 것과 동일한 사용자 자격 증명으로 로그인합니다. ATA 콘솔에 처음 로그인하면 **도메인 연결 설정** 페이지로 자동으로 이동됩니다. 여기에서 ATA Gateway 구성 및 배포를 계속할 수 있습니다.

3.  기본 위치 %programfiles%\Microsoft Advanced Threat Analytics\Center\Logs에 있는 **Microsoft.Tri.Center-Errors.log** 파일에서 오류 파일을 검토합니다.

>[!div class="step-by-step"]
[« 설치 전 단계](install-ata-preinstall.md)
[2단계 »](install-ata-step2.md)

## 참고 항목

- [지원이 필요한 경우 포럼을 확인하세요.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [이벤트 수집 구성](/advanced-threat-analytics/plandesign/configure-event-collection)
- [ATA 필수 구성 요소](/advanced-threat-analytics/plandesign/ata-prerequisites)


<!--HONumber=Apr16_HO2-->


