---

copyright:
  years: 2017, 2018
lastupdated: "2018-04-27"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# 계약 구문 분석 이해
{: #contract_parsing}

{{site.data.keyword.cnc_short}}은 식별된 각 요소의 분석과 함께 구문 분석된 계약을 리턴합니다.

다음 절에서는 리턴된 JSON이 분석을 제공하는 방법을 설명합니다.

## Types
{: #contract_types}

`types` 배열에는 값이 요소의 2행구를 식별하는 `nature` 및 `party` 키가 각각 포함된 여러 오브젝트가 있습니다. 다음 표에는 `nature` 및 `party` 키의 가능한 값이 나열됩니다.

`nature` 값에는 문장에 필요한 조치 유형이 나열됩니다.

| `nature`         |설명                                                |
|:----------------:|-----------------------------------------------------------|
|`Definition`      |이 요소는 조항, 관계 또는 이와 유사한 항목을 분명하게 합니다. 조치는 요소를 완료하는 데 필요하지 않으며 영향을 받는 당사자도 없습니다.|
|`Disclaimer`      |요소의 `party`는 요소에서 지정된 조항을 이행해야 하는 의무도 없지만 이행이 금지되지도 않습니다.|
|`Exclusion`       |요소의 `party`가 요소에서 지정된 조항을 이행하지 않습니다.|
|`Obligation`      |요소의 `party`가 요소에서 지정된 조항을 이행해야 합니다.|
|`Right`           |요소의 `party`가 요소에서 지정된 조항을 받아들이게 됩니다.|
|`Recommendation`  |요소의 `party`가 요소에서 지정된 조항을 이행할 의무는 없지만 권장됩니다.|

## Parties
{: #contract_parties}

`parties` 배열은 계약에 나열된 참가자를 지정합니다. 식별된 각 `party` 오브젝트에는 이름별로 식별된 당사자가 나열되며 이 오브젝트는 `party` 오브젝트의 역할을 분류하는 `role` 오브젝트와 일치합니다. 계약에 대해 리턴할 수 있는 `role` 값은 다음과 같습니다.

| `role`           |설명                                                |
|:----------------:|-----------------------------------------------------------|
|`Buyer`           |계약에 나열된 서비스 또는 상품에 대한 비용을 지불해야 하는 당사자입니다.|
|`End User`        |제공된 상품 또는 서비스와 상호작용할 당사자이며, 명시적으로 `Buyer`와 구분됩니다.|
|`None`            |요소에 대해 식별된 당사자가 없습니다. 이 값은 항상 `Definition` 네이처와 쌍을 이룹니다.|
|`Supplier`        |계약에 나열된 상품 또는 서비스를 제공해야 하는 당사자입니다.|

## Categories
{: #contract_categories}

`categories` 배열은 문장의 주제를 정의합니다. 현재 지원되는 categories는 다음과 같습니다.

| `categories`     |설명                                                |
|:----------------:|-----------------------------------------------------------|
|`Amendments`      |서명된 후 계약의 변경 또는 표준 계약의 수정을 지정하는 요소입니다. 계약 수정 및 계약 변경을 나타내는 요소도 이 카테고리에 속합니다.|
|`Asset Use`       |한 당사자가 계약에 따라 의무(권한 및 제한사항 포함)를 수행하는 다른 당사자의 자산(라이센스 또는 장비)을 사용해야 하는 상황을 나타내는 요소입니다.|
|`Assignments`     |권한, 의무 또는 둘 다를 서드파티로 전송하는 일을 설명하는 요소입니다.|
|`Audits`          |이 카테고리에는 레코드 보관 및 다른 당사자의 문서 또는 레코드를 검사하는 당사자의 권한을 나타내는 요소, 그리고 준수를 검사하거나 검토하는 당사자의 권한 또는 검사나 준수 검토에 당사자가 사용 가능한 요구사항을 나타내는 요소가 포함됩니다.|
|`Business Continuity`|매출, 합병 또는 당사자 중 하나에 대한 계약의 중요한 변경사항의 영향을 나타내는 요소에 대한 좁은 범위의 카테고리입니다.|
|`Communication`  |알림, 통신 방법에 대한 세부사항(정보 교환 행동 또는 프로세스), 연락 담당자 및 연락 정보를 제공하거나 알리는 데 필요한 요구사항을 나타내는 요소입니다. 또한 당사자 간 정보 교환의 허용 가능한 수단을 나타내는 요소입니다.|
|`Confidentiality` |이 카테고리에는 당사자가 계약 완성 과정에서 학습하는 정보를 사용하는 방법을 설명하는 요소, 영업비밀 유지를 논의하는 요소 및 비공개 비즈니스 정보를 설명하는 요소가 포함됩니다.|
|`Deliverables`    |이 카테고리에는 한 당사자가 다른 당사자에게 화폐를 지불하는 조건으로 제공하는 품목을 지정하는 요소 및 상품 준비를 설명하는 요소가 포함됩니다.|
|`Delivery`        |한 당사자에서 다른 당사자로 `Deliverables` 카테고리의 품목을 전달하는 수단을 지정하는 요소입니다. 예를 들어, 한 당사자가 액세스 또는 클라우드 서비스를 판매하는 경우 이 액세스를 가져오는 수단이 이 카테고리에 속합니다.|
|`Dispute Resolution`|이 카테고리에는 계약 당사자 간에 발생하는 분쟁을 해결하기 위한 조항(예: 중재 패널과 같은 정의된 프로시저로 해결)을 논의하는 요소가 포함됩니다. 분쟁은 중재가 아닌 다른 다양한 방법으로 해결될 수 있습니다(예: 회복할 수 없는 손해, 법원 명령 받기 또는 "이를 클래스 조치로 진행할 수 없다"는 취지의 성명). 분쟁의 예에는 노동 쟁의와 송장 또는 청구에 대한 분쟁이 있습니다. 카테고리에는 특정 국가 또는 관할법과 같은 계약의 준거법 또는 법률 선정을 지정하는 요소도 포함됩니다.|
|`Force Majeure`   |당사자의 제어 밖에 있는 가동 중단 이벤트를 나타내는 요소입니다. 이는 특정 책임 제한입니다.|
|`Indemnification` |특정 법적 책임의 조치방안을 지정하는 요소입니다. 보상은 계약의 한 당사자가 다른 당사자의 법적 책임에 대한 비용을 지불하게 되는 경우입니다. 보상은 법적 책임이 발생했음을 내포합니다.|
|`Insurance`       |한 당사자가 다른 당사자에게 제공하는 모든 유형의 보험담보 범위 또는 보험 적용 범위를 나타내는 요소입니다.|
|`Intellectual Property`|예제는 두 개의 카테고리로 나뉩니다. 하나는 일반적으로 법규에서 가져온 특허권, 저작권 및 상표에 대한 공식적 정의를 사용하는 예제이고 다른 하나는 발명, 저자 및 노하우에 대한 넓은 범위의 개념을 사용하는 예제입니다. 또한 정의는 이와 같은 재산권의 위반에 대해 소송을 제기하고 손해 배상금을 요구하는 권한과 같은 지적재산권에 대해 제공될 수 있습니다. `Intellectual Property`에는 특허권, 특허권에 적용할 권한, 상표, 상표명, 서비스표, 도메인 이름, 저작권 및 이와 같은 전 세계적, Schematic, 산업 모델, 발명, 노하우, 영업 비밀, 컴퓨터 소프트웨어 프로그램 및 기타 무형의 독점 정보의 모든 적용 및 등록이 포함됩니다. "서드파티 코드"에서는 코드의 임의 파트가 누군가에게 속하는 경우 IP를 콜아웃해야 합니다.|
|`Liability`       |임의 당사자에게 책임을 부여하는 시기와 방법을 판별하기 위한 방법을 설명하는 요소입니다.|
|`Payment Terms & Billing`|계약에 따른 최종 지불 모드 또는 한 당사자가 비용을 지불하는 방법을 나타내는 요소, 당사자가 비용을 지불받는 방법과 시기 또는 당사자가 비용을 지불하거나 청구받는 품목의 유형을 설명하는 요소, 모든 유형의 요금 지불을 나타내는 요소(특정 가격 또는 수치를 나타내는 요소 제외) 및 계약에 따라 지불받는 당사자를 나타내는 요소를 포함해, 당사자가 비용을 지불하거나 받는 방식을 설명하는 요소가 포함된 넓은 범위의 카테고리입니다.|
|`Pricing & Taxes` |이 카테고리에는 당사자가 지불하거나 지불받는 내용을 설명하는 요소가 포함됩니다. 카테고리에는 특정 요소의 비용에 대한 세부사항을 포함해 교환되는 개별 상품과 연관된 특정 금액 및 세금을 나타내는 요소 및 가격 계산을 위한 특정 수치 또는 방법을 설명하는 요소가 포함됩니다.|
|`Privacy`         |개인 정보(즉, 보호해야 하는 특정 개인에 대한 사적 정보)의 처리를 지정하는 요소입니다. 카테고리는 더 넓은 범위의 `Confidentiality` 카테고리의 특정 서브세트입니다.|
|`Responsibilities`|당사자 중 하나만 감독하고 제어하는, 계약의 보조 태스크입니다. 이 카테고리에 속한 요소의 유형은 계약의 네이처에 따라 다릅니다.|
|`Safety and Security`|직장 안전 개선을 나타내는 요소뿐만 아니라 데이터 및 시스템에 대한 물리적 안전 또는 사이버보안 보호를 나타내는 요소입니다.|
|`Scope of Work`   |이 카테고리는 계약에 있는 내용 대 계약에 없는 내용을 정의합니다. 일반적으로 특정 주문을 정의하는 방법을 당사자에게 알리는 요소가 이 카테고리에 속합니다. 그 예에는 "작업기술서"에 대한 토론 또는 적용 가능한 통신 표준에 대한 설명이 포함됩니다.|
|`Subcontracts`    |계약에 따라 특정 의무를 수행하는 서드파티 고용 및 여기에서 발생하는 권한, 제한사항 및 결과를 나타내는 요소입니다.|
|`Term & Termination`|종료 이후에 적용되는 의무를 포함해, 계약 지속 기간, 계약 종료 스케줄 및 조항, 그리고 종료의 결과를 나타내는 요소입니다.|
|`Warranties`      |당사자가 믿을 수 있는 가정을 바탕으로 하는 배경을 나타내는 요소입니다. 보증 위반 결과도 이 카테고리에 속합니다.|

## Attributes
{: #attributes}

`attributes` 배열은 문장에서 식별되는 속성을 지정합니다. 배열의 각 오브젝트에는 세 가지 키, 즉 `type`(다음 표의 속성 유형), `text`(적용 가능한 텍스트) 및 `attribute`(문서의 속성에 대한 시작점 및 종료점)가 포함됩니다. 현재 지원되는 속성은 다음과 같습니다.

| `attributes`     |설명                                                |
|:----------------:|-----------------------------------------------------------|
|`Location`        |지리적 위치 또는 지역입니다.                         |
|`DateTime`        |날짜, 시간, 날짜 범위 또는 시간 범위입니다.                   |
|`Currency`        |화폐 가치 및 단위입니다.                                  |

# Assurance
{: #assurance}

{{site.data.keyword.cnc_short}}은 식별되는 각 `type` 또는 `category` 요소에 보증 등급을 제공합니다. 현재 하나의 보증 값 `High`가 있으며, 이는 나열된 분류가 컨텐츠를 나타낸다는 의미 있는 증거가 있음을 표시합니다.

## Provenance
{: #provenance}

`types` 및 `categories` 배열의 각 오브젝트에는 `provenance` 오브젝트가 있습니다. `provenance` 오브젝트에는 하나 이상의 `id` 키가 있습니다. 각 `id` 키에는 피드백을 제공하거나 지원을 받기 위해 IBM에 보낼 수 있는 해시 값이 있습니다.

