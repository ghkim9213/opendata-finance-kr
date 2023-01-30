### Abstract

opendata-finance-kr은 국내 자본시장 관련 공공데이터로부터 자주 활용되는 주요 데이터를 선별, 추출 및 산출하여 재배포하는 오픈데이터 프로젝트로,
자본시장 관련 데이터 수집 및 전처리로부터 발생하는 시간과 비용을 줄이는 데 도움이 되고자 기획되었습니다.

- [web](http://www.opendart-finance-kr.com)
- [github](https://github.com/ghkim9213/opendata-finance-kr)

---

### Sources

본 프로젝트가 제공하는 모든 데이터는 다음 공공데이터를 원천으로 합니다.

- 공공데이터포털
  - 금융위원회_KRX상장종목정보: 한국거래소 상장종목 오픈API로, 본 프로젝트에서 1일 1회 업데이트 상태를 확인하여 데이터 추출 및 산출 대상 종목을 특정합니다. [link](https://www.data.go.kr/tcs/dss/selectApiDataDetailView.do?publicDataPk=15094775)
  - 금융위원회_주식시세정보: 상장종목의 가격데이터 오픈API로, 본 프로젝트에서 1일 1회 업데이트 상태를 확인하여 상장종목의 시가총액, 가격비율, 누적수익률 등 가격관련 데이터를 산출합니다. [link](https://www.data.go.kr/tcs/dss/selectApiDataDetailView.do?publicDataPk=15094808)
- 전자공시 OPENDART 시스템
  - 재무정보 일괄다운로드: 분기별 재무제표구분별 데이터셋으로, 본 프로젝트에서 1일 1회 업데이트 상태를 확인하여 주요 재무제표 계정별 패널 데이터를 구성합니다. [link](https://opendart.fss.or.kr/disclosureinfo/fnltt/dwld/main.do)


### Contents

본 프로젝트가 제공하는 모든 데이터는 다음과 같이 분류할 수 있습니다.

**종목별 월별 (분기별) 주요지표 데이터**

  - 단일계정: 전자공시 OPENDART 시스템 재무정보 일괄다운로드 서비스로부터 분석에 자주 활용되는 계정을 선별 및 추출하여 연율화 (누적 1년)한 데이터들의 클래스로, 클래스명 'SingleAccount'로 관리되고 있습니다. 자산총계, 당기순이익 등 주요 재무계정 데이터들이 이 클래스에 속합니다.

  - 복합계정: 전자공시 OPENDART 시스템 재무정보 일괄다운로드 서비스로부터 다수의 단일계정으로 특정할 수 있는 (혹은 단일계정으로 특정할 수 없는) 계정의 데이터를 추출하여 연율화 (누적 1년)한 데이터들의 클래스로, 클래스명 'MixedAccount'로 관리되고 있습니다. 장부가치 등 주요 지표 데이터들이 이 클래스에 속합니다.

  > **복합계정 구분의 필요성** <br /> 명확히 같은 성격을 가진 계정임에도 불구하고 기업의 특성에 따라 다른 이름으로 보고되는 경우가 존재하며, 이를 통제하기 위해 원천으로부터 조건부로 데이터를 추출한 복합계정을 클래스를 관리합니다. 예를 들어, 보통주와 우선주를 모두 발행하는 기업의 경우 보통주자본금(issued capital of common stock)과 우선주자본금(issued capital of preferred stock), 그리고 그 합인 자본금(issued capital)을 모두 보고하는 반면, 우선주를 따로 발행하지 않는 기업의 경우 보통주자본금이 자본금의 전부이기 때문에, 이를 자본금으로 보고할 수도 있고 보통주자본금으로 보고할 수도 있습니다. 이 때, 기업별 자본금 데이터를 얻기 위해 '자본금'으로 데이터를 추출하면 '자본금을 보통주자본금으로 보고한 기업'의 데이터가 누락되는 문제가 발생합니다. 이에 '자본금 데이터가 누락된 경우 보통주자본금을 추출한다'는 조건부 추출 논리를 통해 자본금과 보통주자본금의 복합계정인 '장부가치 (book equity)' 데이터를 생성했습니다.

  - 재무비율: 단일계정 및 복합계정 사이 비율을 나타내는 데이터들의 클래스로, 'AccountRatio'라는 클래스명으로 관리되고 있습니다. ROA, ROE 등 주요 재무비율 지표 데이터들이 이 클래스에 속합니다.

  - 가격비율: 단일계정 및 복합계정을 가격변수로 나눈 비율을 나타내는 데이터들의 클래스로, 클래스명 'PriceRatio'으로 관리되고 있습니다. 장부가치 (시가총액대비), 수익주가비율 (P/E의 역수) 등 주요 가격비율 지표 데이터들이 이 클래스에 속합니다.

  - 모멘텀: 수익률 모멘텀을 나타내는 데이터들의 클래스로, 클래스명 'Momentum'으로 관리되고 있습니다. 누적수익률 (2/12) 등 주요 모멘텀 지표 데이터들이 이 클래스에 속합니다.

  - 규모: 기업의 규모를 나타내는 데이터 클래스로, 클래스명 'Size'로 관리되고 있습니다. 시가총액 등 주요 규모 지표 데이터들이 이 클래스에 속합니다.


**요인 포트폴리오별 수익률 데이터**

종목별 월별 (분기별) 주요지표 데이터를 구성기준으로 요인 포트폴리오를 구성하여 구성기준별 포트폴리오별 수익률 데이터를 제공합니다.


### Data

다음의 방식으로 본 프로젝트가 제공하는 데이터에 접근할 수 있습니다.

- [openAPI](apidoc)
- [download dataset](datasets)


### Database

주요지표 데이터베이스는 [독립적인 프로젝트](https://github.com/ghkim9213/opendata-finance-kr-marketdata-manager)로 구성되어 관리되고 있습니다. 링크에서 데이터 수집, 전처리, 지표 산출 등 세부 과정을 확인할 수 있습니다.


### Contact
- email: gkim9213@gmail.com
