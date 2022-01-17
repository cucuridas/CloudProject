해당 레파지토리의 내용은 L-CLOUD 작업에서 제가 변경 및 수정 참여한 내용에 대해 기록을 남기기 위해 작성된 저장소입니다
입력 값 및 출력 값에 대한 정보는 실제 동작하는 로직과 상이하며 아키텍처 또는 중요문서에 대한 내용은 다루고 있지않음을 미리 공지하는 바입니다 👍👍👍

1월 17일 수정사항

getFirePowerAclNew 화면 출력 오류 (수정항목)

*해당내용은 다른 개발자가 제작한 코드를 수정한 내용입니다


1.현 개발이 완료된 화면에서 ACL 정보를 가져오게 될때 ‘API에서 return 되는 값’, ‘포탈화면 DB’에 저장되어 있는 값이 같을때 화면에 출력되게 되는 로직으로 개발이 되어 있는데 장비에서 해당 ACL 정책의 기간이 만료 되었을 때 API는 해당 정책에 대한 정보를 보내주지 않음으로 인해 포탈화면에서 정책에 대한 관리가 불가능 해지는 결함
2.기존의 데이터를 정형화 시킬때 조건문과 띄어쓰기를 통한 인덱싱을 통한 방법이 특정 패턴에 대하여 정형화하지 못하는 문제

getAcl 형태
	 
	1.들어오는 input 값 형태에 맞춰 명령어 구조 정의
	
	2.앞의 두 내용을 합하여 해당 네트워크 장비에 명령어 호출
	
	3.comand 수행 후 return 값 리턴

	4.조건문을 활용한 필요정보 선택 후 전달 Dic에 추가

	5. 완성된 Dic을 리턴

수정내용 :
1. 5번항목 에대해 기존의 ‘inactive’ 내용을 가지면 항목에서 제외하는 내용을 삭제 후 API가 보내주는 정보에 ‘state’:’inactive’로 표시 해주는 형태로 변경 하여 포탈에서도 해당 내용을 통해 정책 만료에 대한 처리를 진행할 수 있도록 진행
2. 로직 전반에 대한 내용을 수정하게 되었는데 기존의 조건문,인덱싱을 통한 정형화 방법을 '정규표현식'을 통한 정형화 방법으로 구축, 해당 과정에서 일반적으로 나오는 패턴에 대해서는 먼저 패턴을 정의해둔 상태(실제 패턴을 활용하여 정형화 시키는 로직 파일과 상수로서 패턴을 정의하는 파일을 구분하여 제작 -> 새로운 패턴이 생길때 패턴을 정의하는 파일에 대해서만 수정하는것으로 변경)
