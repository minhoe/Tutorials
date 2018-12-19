# AWS 일반 사용자(IAM) 설정 방법

1. credentials.csv에 저장된 `Console login link`의 주소를 읽어온다.
 - 예 : https://{YOUR_AWS_ACCOUNT_NUMBER_(12DIGITS)}.signin.aws.amazon.com/console
 - 상기 링크는 외우기 어려우므로 별도 즐겨찾기 추가 필요

2. 사용자 이름(회사 이메일 주소)과 암호를 입력한다.
 - 초기 로그인의 경우, 암호는 credentials.csv 파일을 참조한다. 이후 비밀번호 변경 페이지가 나타나면 개인의 희망 암호로 변경한다.

3. AWS Management Console 접속 완료
 - 좌측 상단 `서비스` 메뉴를 클릭 후 본인이 원하는 서비스를 이용한다.
 - 분석 환경을 이용하기 위해서는 별도 Tutorial을 참고한다.

4. EC2 인스턴스 개수 제한 해제 신청
 - 사용자 계정으로 접속 후 `인스턴스 생성`을 진행하게 되면 최종 단계에서 다음과 같은 메세지가 뜨면서 생성이 중단되는 것을 확인할 수 있다. 이는 신규 발급된 계정에서 생성 가능한 EC2 인스턴스의 개수가 0개로 초기화 되어 있기 때문이다.

`시작 실패
You have requested more instances (1) than your current instance limit of 0 allows for the specified instance type. Please visit http://aws.amazon.com/contact-us/ec2-request to request an adjustment to this limit.`

 - 개수 제한 신청은 다음의 방법을 따른다.

  1. 계정 로그인 후 Support Center 로 이동합니다(우측 상단 지원 링크 클릭 후 지원센터) URL : https://console.aws.amazon.com/support 
  2. Support Center에서 `Create Case` 클릭 
  3. `Regarding`에서 `Service Limit Increase` 선택 
  4. `Limit Type`에서 제한을 해제하고자 하는 인스턴스 유형을 선택한다. 일반적인 기계학습을 위해 사용하는 인스턴스는 `EC2 Instances` 이다.
  5. `Request` 에서 제한 해제 `Region`은 `US West(Oregon)` 선택
  6. `Primary Instance Type`에서 개수를 해제하고자 하는 인스턴스를 선택한다. AIR랩에서 주로 사용하는 인스턴스 리스트는 아래를 참조한다.
  7. `Limit`은 기본 `Instance Limit`을 선택
  8. `New limit value` - 2 입력 (동일 계정에서 해당 인스턴스를 최대 2개까지 생성 가능하도록 변경한다는 의미 입니다.)
  9. 추가로 해제가 필요한 인스턴스에 대해서 `Add another request`를 클릭 후 5 ~ 8번을 반복한다.
  10. `Use Case Description`에 영어로 간단한 사유를 작성한다.
  11. 그 외 수정사항이 없으면 맨 아래 `Submit`을 클릭한다. 신청 완료 후 약 1시간 ~ 4시간 정도 소요 되며, 제한 해제 완료 시 계정 이메일로 내용을 확인할 수 있다.


# AWS 관리자(Root) 설정 방법 : IAM 사용자 추가
- AIRLab 대표 계정으로 접속

## Page 1

### 사용자 세부 정보 설정
- `사용자 이름` : 회사 이메일 주소를 입력

### AWS 액세스 유형 선택
- `액세스 유형` : 프로그래밍 방식 / AWS Mgmt Console 모두 선택
- `콘솔 비밀번호` : 자동 생성된 비밀 번호
- `비밀번호 재설정 필요` : 사용자가 다음에 로그인할 때 새 비밀번호 생성 요청

## Page 2

### 권한 설정
- `그룹에서 사용자 추가` 선택 후 `AIRLab` 선택

## Page 3

### 태그 추가(선택 사항)
- `Name` : 본명(English)
- `E-mail` : 회사 이메일 주소
- `Team` : 팀 명(English)

## Page 4
- 설정 내용 확인

## Page 5
- 페이지 상단 `성공` 표시 확인
- `.csv 다운로드` : credentials.csv를 다운로드 후 사용자에게 전달
- `이메일 전송` : 접속 관련 정보를 회사 이메일로 송부


