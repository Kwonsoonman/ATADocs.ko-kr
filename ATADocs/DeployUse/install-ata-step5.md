---
# required metadata

title: ATA 설치 - 5단계 | Microsoft Advanced Threat Analytics
description: ATA 설치 5단계에서는 ATA Gateway에 대한 설정을 구성합니다.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 2a5b6652-2aef-464c-ac17-c7e5f12f920f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 설치 - 5단계

>[!div class="step-by-step"]
[« 4단계](install-ata-step4.md)
[6단계 »](install-ata-step6.md)


## 5단계. ATA Gateway 설정 구성
ATA Gateway를 설치한 후에는 다음 단계를 수행하여 ATA Gateway에 대한 설정을 구성합니다.

1.  ATA Gateway 컴퓨터의 ATA 콘솔에서 **구성**을 클릭하고 **ATA Gateway** 페이지를 선택합니다.

2.  다음 정보를 입력합니다.



  - **설명**: <br>ATA Gateway에 대한 설명을 입력합니다.
  - **도메인 컨트롤러**(필수): <br>컨트롤러 목록에 대한 자세한 내용은 아래를 참조하세요.<br>도메인 컨트롤러의 전체 FQDN을 입력하고 더하기 기호를 클릭하여 목록에 추가합니다. 예를 들면  **dc01.contoso.com**과 같습니다.<br /><br />![예제 FDQN 이미지](media/ATAGWDomainController.png)<br>목록에서 첫 번째 도메인 컨트롤러의 개체는 LDAP 쿼리를 통해 동기화됩니다. 도메인 크기에 따라 다소 시간이 걸릴 수 있습니다.<br>
  **참고:** <br>첫 번째 도메인 컨트롤러가 읽기 전용이 **아닌지** 확인합니다. 읽기 전용 도메인 컨트롤러는 초기 동기화를 완료한 후에만 추가해야 합니다.<br>


 - **네트워크 어댑터 캡처**(필수):<br>도메인 컨트롤러 트래픽을 수신할 대상 미러 포트로 구성된 스위치에 연결된 네트워크 어댑터를 선택합니다.|네트워크 어댑터 캡처를 선택합니다.
    ![게이트웨이 설정 구성 이미지](media/ATA-Config-GW-Settings.jpg)

3.  **저장**을 클릭합니다.

    > [!NOTE]
    > ATA Gateway 서비스를 처음 시작하는 데 몇 분 정도 걸립니다. ATA Gateway에서 사용되는 네트워크 캡처 파서의 캐시를 작성하기 때문입니다.

다음 정보는 **도메인 컨트롤러** 목록에 입력한 서버에 적용됩니다.

-   목록의 첫 번째 도메인 컨트롤러는 ATA Gateway에서 LDAP 쿼리를 통해 도메인에 있는 개체를 동기화하는 데 사용됩니다. 도메인 크기에 따라 다소 시간이 걸릴 수 있습니다.

-   ATA Gateway에서 포트 미러링을 통해 모니터링하는 트래픽의 모든 도메인 컨트롤러가 **도메인 컨트롤러** 목록에 나열되어야 합니다. 도메인 컨트롤러가 **도메인 컨트롤러** 목록에 나열되지 않은 경우 의심스러운 활동 검색이 예상대로 작동하지 않을 수 있습니다.

-   첫 번째 도메인 컨트롤러가 RODC(읽기 전용 도메인 컨트롤러)가 **아닌지** 확인합니다.

    읽기 전용 도메인 컨트롤러는 초기 동기화를 완료한 후에만 추가해야 합니다.

-   목록에 있는 하나 이상의 도메인 컨트롤러는 글로벌 카탈로그 서버입니다. 이를 통해 ATA는 포리스트의 다른 도메인에 있는 컴퓨터 및 사용자 개체를 확인할 수 있습니다.

구성 변경은 ATA Gateway와 ATA Center 간의 예정된 다음 동기화 시 ATA Gateway에 적용됩니다.

### 설치 유효성 검사:
ATA Gateway가 성공적으로 배포되었는지 유효성을 검사하려면 다음을 확인합니다.

1.  Microsoft Advanced Threat Analytics Gateway 서비스가 실행 중인지 확인합니다. ATA Gateway 설정을 저장한 후 서비스를 시작하는 데 몇 분 정도 걸릴 수 있습니다.

2.  서비스가 시작되지 않는 경우 기본 폴더 “%programfiles%\Microsoft Advanced Threat Analytics\Gateway\Logs”에 있는 “Microsoft.Tri.Gateway-Errors.log” 파일을 검토하고 “transfer” 또는 “service start”가 포함된 항목을 검색합니다.

3.  다음 Microsoft ATA Gateway 성능 카운터를 확인합니다.

    -   **NetworkListener Captured Messages/sec**: 이 카운터는 ATA에서 초당 캡처되는 메시지 수를 추적합니다. 값은 모니터링 중인 도메인 컨트롤러 수 및 각 도메인 컨트롤러의 사용 빈도에 따라 수백에서 수천이어야 합니다. 한 자리 또는 두 자리 값은 포트 미러링 구성 문제를 나타낼 수 있습니다.

    -   **EntityTransfer Activity Transfers/Sec**: 이 값은 몇 초마다 수백 개 범위여야 합니다.

4.  이번에 처음으로 ATA Gateway를 설치한 경우 몇 분 후에 ATA 콘솔에 로그인하여 열려 있는 화면의 오른쪽을 살짝 밀어 알림 창을 엽니다. 콘솔 오른쪽의 알림 표시줄에 **최근에 학습된 엔터티** 목록이 표시됩니다.

5.  설치가 성공적으로 완료되었는지 유효성을 검사합니다.

    콘솔의 검색 창에서 도메인의 사용자 또는 그룹과 같은 항목을 검색합니다.

    성능 모니터를 엽니다. 성능 트리에서 **성능 모니터**를 클릭한 다음 더하기 아이콘을 클릭하여 **카운터 추가**를 수행합니다. **Microsoft ATA Gateway**를 확장하고 아래의 **Network Listener Captured Messages per Second**로 스크롤하여 이를 추가합니다. 그러면 그래프에 활동이 표시됩니다.

    ![성능 카운터 추가 이미지](media/ATA-performance-monitoring-add-counters.png)


>[!div class="step-by-step"]
[« 4단계](install-ata-step4.md)
[6단계 »](install-ata-step6.md)

## 참고 항목

- [지원이 필요한 경우 포럼을 확인하세요.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [이벤트 수집 구성](/advanced-threat-analytics/plandesign/configure-event-collection)
- [ATA 필수 구성 요소](/advanced-threat-analytics/plandesign/ata-prerequisites)


<!--HONumber=Apr16_HO2-->


