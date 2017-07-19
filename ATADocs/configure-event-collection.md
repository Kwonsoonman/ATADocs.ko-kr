---
title: "Advanced Threat Analytics에서 Windows 이벤트 전달 구성 | Microsoft Docs"
description: "ATA를 통해 Windows 이벤트 전달 기능을 구성하는 옵션에 대해 설명합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/2/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 6469f602d2da833e96bba72003aad3fe2b67eb48
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*



# <a name="configuring-windows-event-forwarding"></a>Windows 이벤트 전달 구성

검색 기능을 강화하려면 ATA에 Windows 이벤트 4776, 4732, 4733, 4728, 4729, 4756, 4757이 있어야 합니다. 이러한 이벤트는 ATA 경량 게이트웨이에서 자동으로 읽거나, ATA 경량 게이트웨이가 배포되지 않은 경우 두 가지 방법 중 하나로 ATA 게이트웨이에 전달될 수 있습니다. 하나는 ATA 게이트웨이가 SIEM 이벤트를 수신하도록 구성하는 것이고, 다른 하나는 [Windows 이벤트 전달을 구성](#configuring-windows-event-forwarding)하는 것입니다.

> [!NOTE]
> ATA 버전 1.8 이상에서는 ATA 경량 게이트웨이에 이벤트 수집 구성이 더 이상 필요하지 않습니다. 이제 ATA 경량 게이트웨이가 이벤트 전달을 구성하지 않고도 로컬에서 이벤트를 읽을 수 있습니다.

### <a name="wef-configuration-for-ata-gateways-with-port-mirroring"></a>포트 미러링으로 ATA 게이트웨이에 대한 WEF 구성

도메인 컨트롤러에서 ATA 게이트웨이로의 미러링을 구성하고 나면 원본에서 시작된 구성을 사용하여 아래 지침에 따라 Windows 이벤트 전달을 구성합니다. 이것이 Windows 이벤트 전달을 구성하는 한 가지 방법입니다. 

**1단계: 도메인 Event Log Readers 그룹에 네트워크 서비스 계정 추가** 

이 시나리오에서는 ATA 게이트웨이가 도메인의 멤버라고 간주합니다.

1.  Active Directory 사용자 및 컴퓨터를 열고 **Builtin** 폴더로 이동하여 **Event Log Readers** 그룹을 두 번 클릭합니다. 
2.  **멤버**를 선택합니다.
4.  **네트워크 서비스**가 목록에 없으면 **추가**를 클릭하고, **선택할 개체 이름을 입력하십시오** 필드에 **네트워크 서비스**를 입력합니다. **이름 확인**클릭한 다음 **확인**을 두 번 클릭합니다. 

**네트워크 서비스**를 **Event Log Readers** 그룹에 추가 한 후 변경 내용을 적용하려면 도메인 컨트롤러를 다시 부팅해야 합니다.

**2단계: 대상 구독 관리자 구성 설정을 위해 도메인 컨트롤러에서 정책 만들기** 
> [!Note] 
> 이러한 설정에 대한 그룹 정책을 만들고 ATA 게이트웨이에서 모니터링할 각 도메인 컨트롤러에 그룹 정책을 적용할 수 있습니다. 다음 단계는 도메인 컨트롤러의 로컬 정책을 수정합니다.     

1.  각 도메인 컨트롤러에서 *winrm quickconfig* 명령을 실행합니다.
2.  명령 프롬프트에 *gpedit.msc*를 입력합니다.
3.  **컴퓨터 구성 정책 > 관리 템플릿 > Windows 구성 요소 > 이벤트 전달**을 확장합니다.

 ![로컬 정책 그룹 편집기 이미지](media/wef 1 local group policy editor.png)

4.  **대상 가입 관리자 구성**을 두 번 클릭합니다.
   
    1.  **사용**을 선택합니다.
    2.  **옵션**에서 **표시**를 클릭합니다.
    3.  **SubscriptionManagers**에서 다음 값을 입력하고 **확인**을 클릭합니다. *Server=http://<fqdnATAGateway>:5985/wsman/SubscriptionManager/WEC,Refresh=10* (For example: Server=http://atagateway9.contoso.com:5985/wsman/SubscriptionManager/WEC,Refresh=10)
 
   ![대상 구독 구성 이미지](media/wef 2 config target sub manager.png)
   
    5.  **확인**을 클릭합니다.
    6.  관리자 권한 명령 프롬프트에서 *gpupdate /force*를 입력합니다. 

**3단계: ATA Gateway 서버에서 다음 단계 수행** 

1.  관리자 권한 명령 프롬프트를 열고 *wecutil qc*를 입력합니다.
2.  **이벤트 뷰어**를 엽니다. 
3.  마우스 오른쪽 단추로 **구독**을 클릭하고 **구독 만들기**를 클릭합니다. 

   1.   구독에 대한 이름과 설명을 입력합니다. 
   2.   **대상 로그**에서 **전달된 이벤트**가 선택되어 있는지 확인합니다. ATA에서 이벤트를 읽으려면 대상 로그가 **전달된 이벤트**여야 합니다. 
   3.   **원본 컴퓨터 시작**을 선택하고 **컴퓨터 그룹 선택**을 클릭합니다.
        1.  **도메인 컴퓨터 추가**를 클릭합니다.
        2.  **선택할 개체 이름을 입력하십시오** 필드에 도메인 컨트롤러의 이름을 입력합니다. **이름 확인**을 클릭하고 **확인**을 클릭합니다. 
       
        ![이벤트 뷰어 이미지](media/wef3 event viewer.png)
   
        
        3.  **확인**을 클릭합니다.
   4.   **이벤트 선택**을 클릭합니다.

        1. **로그 기준**을 클릭하고 **보안**을 선택합니다.
        2. **이벤트 ID 포함/제외** 필드에 이벤트 번호를 입력하고 **확인**을 클릭합니다. 

 ![쿼리 필터 이미지](media/wef 4 query filter.png)

   5.   만들어진 구독을 마우스 오른쪽 단추로 클릭하고 **런타임 상태**를 선택하여 상태에 문제가 있는지 확인합니다. 
   6.   몇 분 후에 전달되도록 설정한 이벤트가 ATA 게이트웨이의 전달된 이벤트에 표시되는지 확인합니다.


자세한 내용은 [이벤트를 전달하고 수집하도록 컴퓨터 구성](https://technet.microsoft.com/library/cc748890)을 참조하세요.

## <a name="see-also"></a>참고 항목
- [ATA 설치](install-ata-step1.md)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
