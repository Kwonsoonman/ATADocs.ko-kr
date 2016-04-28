---
# required metadata

title: ATA 구성 변경 - 캡처 네트워크 어댑터의 이름 | Microsoft Advanced Threat Analytics
description: ATA 게이트웨이 연결을 끝내지 않고 캡처 네트워크 어댑터로 구성된 네트워크 어댑터의 이름을 변경하는 방법을 설명합니다.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 3225a81e-0395-43ca-9a48-0cbe7171e5de

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 구성 변경 - 캡처 네트워크 어댑터의 이름

>[!div class="step-by-step"]
[« 도메인 연결 암호](modifying-ata-config-dcpassword.md)

## ATA 게이트웨이 캡처 네트워크 어댑터의 이름 변경
현재 캡처 네트워크 어댑터로 구성되어 있는 네트워크 어댑터의 이름을 변경하면 ATA 게이트웨이 서버가 시작되지 않게 됩니다. ATA 게이트웨이 연결을 끝내지 않고 이름을 원활하게 변경하려면 다음 프로세스를 수행합니다.

1.  ATA 게이트웨이 구성 페이지에서 이름을 바꿀 네트워크 어댑터를 선택 취소하고 해당 캡처 네트워크 어댑터를 대신할 다른 네트워크 어댑터를 선택합니다. 이것은 중간 네트워크 어댑터 또는 관리 네트워크 어댑터일 수 있습니다. 이 시간 동안 ATA는 도메인 컨트롤러에서 포트 미러링되는 트래픽을 캡처하지 않습니다. 새 구성을 저장합니다.

2.  ATA 게이트웨이에서 제어판을 열고 네트워크 연결을 선택하여 네트워크 어댑터의 이름을 바꿉니다.

3.  그런 다음 ATA 콘솔의 ATA 게이트웨이 구성 페이지로 다시 이동합니다. 페이지를 새로 고쳐야 목록에 새 이름의 네트워크 어댑터가 표시될 수 있습니다. 1단계에서 선택한 어댑터를 선택 취소하고 새로 명명된 어댑터를 선택합니다. 마지막으로 새 구성을 저장합니다.

이 프로세스를 수행하지 않고 네트워크 어댑터 이름을 바꾼 경우 ATA 게이트웨이는 시작되지 않고 Microsoft.Tri.Gateway Errors.log 로그 파일에 ATA 게이트웨이에 대한 다음 오류가 발생합니다. 아래 예제에서 **Capture**는 설정한 네트워크 어댑터의 원래 이름입니다.

`Error [NetworkListener] Microsoft.Tri.Infrastructure.ExtendedException: Unavailable network adapters [UnavailableCaptureNetworkAdapterNames=Capture]`

이 문제를 해결하려면 네트워크 어댑터 이름을 ATA 설정 시 사용했던 원래 이름으로 다시 변경한 다음, 위에 설명된 이름 변경 프로세스를 진행합니다.

>[!div class="step-by-step"]
[« 도메인 연결 암호](modifying-ata-config-dcpassword.md)


## 참고 항목
- [ATA 콘솔 작업](/advanced-threat-analytics/understand/working-with-ata-console)
- [ATA 설치](install-ata.md)
- [지원이 필요한 경우 포럼을 확인하세요.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


