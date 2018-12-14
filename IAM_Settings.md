# AWS IAM 사용자 추가 방법
- AIRLab 대표 계정으로 접속

## Page 1

### 사용자 세부 정보 설정
- '사용자 이름' : 회사 이메일 주소를 입력

### AWS 액세스 유형 선택
- '액세스 유형' : 프로그래밍 방식 / AWS Mgmt Console 모두 선택
- '콘솔 비밀번호' : 자동 생성된 비밀 번호
- '비밀번호 재설정 필요' : 사용자가 다음에 로그인할 때 새 비밀번호 생성 요청

## Page 2

### 권한 설정
- '그룹에서 사용자 추가' 선택 후 'AIRLab' 선택

## Page 3

### 태그 추가(선택 사항)
- 'Name' : 본명(English)
- 'E-mail' : 회사 이메일 주소
- 'Team' : 팀 명(English)

## Page 4
- 설정 내용 확인

## Page 5
- 페이지 상단 '성공' 표시 확인
- '.csv 다운로드' : credentials.csv를 다운로드 후 사용자에게 전달
- '이메일 전송' : 접속 관련 정보를 회사 이메일로 송부


# AWS IAM 사용자 접속 방법

1. credentials.csv에 저장된 'Console login link'의 주소를 읽어온다.
 - 예 : https://{YOUR_AWS_ACCOUNT_NUMBER_(12DIGITS)}.signin.aws.amazon.com/console
 - 상기 링크는 외우기 어려우므로 별도 즐겨찾기 추가 필요

2. 사용자 이름(회사 이메일 주소)과 암호를 입력한다.
 - 초기 로그인의 경우, 암호는 credentials.csv 파일을 참조한다. 이후 비밀번호 변경 페이지가 나타나면 개인의 희망 암호로 변경한다.

3. AWS Management Console 접속 완료
 - 좌측 상단 '서비스' 메뉴를 클릭 후 본인이 원하는 서비스를 이용한다.
 - 분석 환경을 이용하기 위해서는 별도 Tutorial을 참고한다.
