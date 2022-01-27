해당 레파지토리의 내용은 L-CLOUD 작업에서 제가 변경 및 수정 참여한 내용에 대해 기록을 남기기 위해 작성된 저장소입니다 👍👍👍
## 1월 27일
## 추가 UCSD 개발 (ohter.setStaticIPpool.js)
추가 개발 항목….


UCSD cloupia 스크립트를 통해  prefix 에 대한 정보값을 받고 가용할 IP를 UCSD에  저장하여 다른 Task를 통해 장비에 라우팅 하여 사용할 수 있게끔 처리하는 로직을 만들게 되었다 입력값은 ipPool,prefix 정보를 받게 되며 input이라는 객체를 통해 UCSD 솔루션 포탈 화면에서 값을 받고 스크립트에서 활용하였다. 해당로직에서는 슈퍼넷팅을 지원하지 않으며 서브넷팅을 통한 대역 구성만을 생성하게 해달라는 요구조건으로 개발되었다


로직 형태
	
	1. 입력 받은 prefix,ipPool 에 대한 input 값에 대한 validation 체크

	2. 계산식을 통해 가용 IP 대역 정의


*해당 로직을 개발하기 위한 환경은 JS와 거의 동일하나 자체적인 라이브러리 및 변수 타입에 대한 설정이 ‘var’로 고정되는 점이 있음

## 1월 25일
## 추가 함수 개발 사항 (ohter.setMigStaticIpPool.py)
추가 개발 항목….


개발하는 과정에서 추가로 개발해야되는 함수들이 있어 정리하여 개발 하였다…(db 접속 후 IP Pool정보, IP 대역 체크, 네트워크 장비의 Group ID,규칙화된 이름으로 변경 )

IP Pool 정보, Group ID 의 정보값을 어떻게 가져오는 사용하고 있는 UCSD 정보를 조회해오게 되는데 후의 UCSD를 제거하게 되었을 때를 대비하여 따로 개발하게 되었다 데이터는 
장비에서 직접 가져와 Json 형태로 리턴 해주는 로직으로 설계하기로 했다


로직 형태
	
	1. 명령어와 함께 API 호출 하여 리턴 값 받기

	2. 리턴 값에대해 필요한 정보인 IP 정보만 받아오기

	3. IP 정보를 Pool형태로 변형 후 리스트로 전달 하기



*그룹 ID도 동일한 형태로 제작 되었습니다, 추가로 개발된 사항 중 설명에 없는 로직은 간단 로직으로서 따로 설명을 적지않았습니다

## 1월 20일  
### <u>**DataCrolling.데이터 수집 **<u>

Cloud 프로젝트가 막바지에 다가갈수록 사용자들의 편의성을 돕기 위해 여러가지 메뉴얼을 제작하는 과정 중이다. 그 중  용어사전과 FAQ 제작에 필요한 데이터를 Ncloud에서 수집하기 위해 크롤링 로직을 짜게 되었다 해당 데이터를 수집하는데 있어서 ‘Ncloud’에서 데이터를 동적으로 사용자에게 제공해 줌으로 ‘soup’ 대신 ’selenium’을 선택하게 되었는데 ’selenium’은 크롤링 모듈이라기 보다는 테스트 모듈에서 더 많이 활용되고 있다

Ncloud_dic 로직 형태
	
	입력 값 : a~z 까지 알파벳(소문자)
	
	1. ‘selenium’을 통해 원하고자 하는 URL 주소에 접속(URL+입력받은 알파벳)

	2. 수집하고자 하는 ‘text’ 데이터가 있는 태그 위치를 입력  

	3. 태그 위치를 통해 데이터 수집

	4. 수집한 데이터를 ‘pandas’ 를 통해 정형화

	5. 정형화 된 데이터를 ‘csv’ 파일로 저장


Ncloud_faq 로직 형태

	입력 값 : URL주소,페이지번호,정규화시 사용될 Category명, 정규화시 사용될 subCategory명

	1. ‘selenium’을 통해 원하고자 하는 URL 주소에 접속(URL+페이지번호)
	
	2. 접속한 페이지에 질문을 클릭하여 이동

	2. 수집하고자 하는 ‘text’ 데이터가 있는 태그 위치를 입력  

	3. 태그 위치를 통해 데이터 수집

	4. 수집한 데이터를 ‘pandas’ 를 통해 정형화

	5. 정형화 된 데이터를 ‘xlsx’ 파일로 저장


특이사항 : 용어사전집을 크롤링 할 때에는 시간적인 문제나 크롤링하는 위치를 찾아가는데 있어서 어려움이 없어 로직을 구성하는데 문제가 없었으나 FAQ 크롤링을 함에 있어서 데이터를 찾기 위해 페이지 이동을 3번이나하는 문제와 함께 시간적 여유가 없었다...먼저 제작했던 'Ncloud_dic' 을 최대한 활용하기위해 형태 변경을 줄이는 대신 카데고리명이나 서브카데고리명에 대해서는 입력을 받아 처리하도록 로직을 구성하였다



## 1월 18일 수정사항 
### <u>**AGP.getAgpPortGroup 조회 오류**<u>

*해당내용은 다른 개발자가 제작한 코드를 수정한 내용입니다

Airflow(가칭: D+)에서 장비정보를 받아와서 포탈 백엔드로 API 데이터를 넘겨 줄때 이름 규칙을 정해 놓았는데 ‘문자_문자_문자’ 형태로 전달 해주게끔 정해 놓았으나 테스트하는 스테이징 서버에는 반영 되지 않아  조회가 되지않는 결함이 있음

getAgpPortGroup 호출 형태
	
	1. Airflow(가칭:D+)에서 인프라 오케스트레이션 솔루션인 UCSD DB를 조회

	2. 해당 데이터를 정형화 

	3. 정형화 된 데이터를 포탈 백엔드 API 호출에 맞춰 전달

<img width="613" alt="스크린샷 2022-01-18 오후 2 50 37" src="https://user-images.githubusercontent.com/65060314/149878973-526c29f4-c705-4780-b946-f557e7e58f51.png">


수정내용 :
2번 정형화 과정에서 현재 ‘문자_문자-문자’로 출력되는 데이터에 대해 정의되는 key 값을 확인 후 vlaue 값을 정의 할 때에 ‘replace()’함수를 통해 약속된 이름 규칙으로 변경하도록 로직을 추가
*다른 패턴의 출력에 대해서는 존재하지 않다는 가정하에 코드를 수정……. 



## 1월 17일 수정사항 
### <u>**FW.getFirePowerAclNew 화면 출력 오류**<u>

*해당내용은 다른 개발자가 제작한 코드를 수정한 내용입니다


1.현 개발이 완료된 화면에서 ACL 정보를 가져오게 될때 ‘API에서 return 되는 값’, ‘포탈화면 DB’에 저장되어 있는 값이 같을때 화면에 출력되게 되는 로직으로 개발이 되어 있는데 장비에서 해당 ACL 정책의 기간이 만료 되었을 때 API는 해당 정책에 대한 정보를 보내주지 않음으로 인해 포탈화면에서 정책에 대한 관리가 불가능 해지는 결함
	
2.기존의 데이터를 정형화 시킬때 조건문과 띄어쓰기를 통한 인덱싱을 통한 방법이 특정 패턴에 대하여 정형화하지 못하는 문제

#### getAcl 형태
	 
	1.들어오는 input 값 형태에 맞춰 명령어 구조 정의
	
	2.앞의 두 내용을 합하여 해당 네트워크 장비에 명령어 호출
	
	3.comand 수행 후 return 값 리턴

	4.조건문을 활용한 필요정보 선택 후 전달 Dic에 추가

	5. 완성된 Dic을 리턴

#### 수정내용 :
1. 5번항목 에대해 기존의 ‘inactive’ 내용을 가지면 항목에서 제외하는 내용을 삭제 후 API가 보내주는 정보에 ‘state’:’inactive’로 표시 해주는 형태로 변경 하여 포탈에서도 해당 내용을 통해 정책 만료에 대한 처리를 진행할 수 있도록 진행
2. 로직 전반에 대한 내용을 수정하게 되었는데 기존의 조건문,인덱싱을 통한 정형화 방법을 '정규표현식'을 통한 정형화 방법으로 구축, 해당 과정에서 일반적으로 나오는 패턴에 대해서는 먼저 패턴을 정의해둔 상태(실제 패턴을 활용하여 정형화 시키는 로직 파일과 상수로서 패턴을 정의하는 파일을 구분하여 제작 -> 새로운 패턴이 생길때 패턴을 정의하는 파일에 대해서만 수정하는것으로 변경)
