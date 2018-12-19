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


---
참고 : 분석 환경을 위한 인스턴스 대표 유형 리스트

1) 일반 분석용

|모델|vCPU|시간당 CPU 크레딧|메모리(GiB)|스토리지|네트워크 성능(Gbps)|가격(USD/hr)|
|---|---|---|---|---|---|---|
|t3.nano|2|6|0.5|EBS 전용|최대 5|0.0052|
|t3.micro|2|12|1|EBS 전용|최대 5|0.0104|
|t3.small|2|24|2|EBS 전용|최대 5|0.0208|
|t3.medium|2|24|4|EBS 전용|최대 5|0.0416|
|t3.large|2|36|8|EBS 전용|최대 5|0.0832|
|t3.xlarge|4|96|16|EBS 전용|최대 5|0.1664|
|t3.2xlarge|8|192|32|EBS 전용|최대 5|0.3328|
|t2.nano|1|3|0.5|EBS 전용|낮음|0.0058|
|t2.micro|1|6|1|EBS 전용|낮음에서 중간|0.0116|
|t2.small|1|12|2|EBS 전용|낮음에서 중간|0.023|
|t2.medium|2|24|4|EBS 전용|낮음에서 중간|0.0464|
|t2.large|2|36|8|EBS 전용|낮음에서 중간|0.0928|
|t2.xlarge|4|54|16|EBS 전용|중간|0.1856|
|t2.2xlarge|8|81|32|EBS 전용|중간|0.3712|

2) 고성능 CPU를 활용한 분석

 |모델|vCPU|메모리(GiB)|스토리지(GiB)|전용 EBS 대역폭(Mbps)|네트워크 성능(Gbps)|가격(USD/hr)|
|---|---|---|---|---|---|---|
|c5.large|2|4|EBS 전용|최대 3,500|최대 10|0.085|
|c5.xlarge|4|8|EBS 전용|최대 3,500|최대 10|0.17|
|c5.2xlarge|8|16|EBS 전용|최대 3,500|최대 10|0.34|
|c5.4xlarge|16|32|EBS 전용|3,500|최대 10|0.68|
|c5.9xlarge|36|72|EBS 전용|7,000|10|1.53|
|c5.18xlarge|72|144|EBS 전용|14,000|25|3.06|
|c5d.large|2|4|1 x 50 NVMe SSD|최대 3,500|최대 10|0.096|
|c5d.xlarge|4|8|1 x 100 NVMe SSD|최대 3,500|최대 10|0.192|
|c5d.2xlarge|8|16|1 x 200 NVMe SSD|최대 3,500|최대 10|0.384|
|c5d.4xlarge|16|32|1 x 400 NVMe SSD|3,500|최대 10|0.768|
|c5d.9xlarge|36|72|1 x 900 NVMe SSD|7,000|10|1.728|
|c5d.18xlarge|72|144|2 x 900 NVMe SSD|14,000|25|3.456|
|c5n.large|2|5.25|EBS 전용|최대 3,500|최대 25|0.108|
|c5n.xlarge|4|10.5|EBS 전용|최대 3,500|최대 25|0.216|
|c5n.2xlarge|8|21|EBS 전용|최대 3,500|최대 25|0.432|
|c5n.4xlarge|16|42|EBS 전용|3,500|최대 25|0.864|
|c5n.9xlarge|36|96|EBS 전용|7,000|50|1.944|
|c5n.18xlarge|72|192|EBS 전용|14,000|100|3.888|
|c4.large|2|3.75|EBS 전용|500|중간|0.1|
|c4.xlarge|4|7.5|EBS 전용|750|높음|0.199|
|c4.2xlarge|8|15|EBS 전용|1,000|높음|0.398|
|c4.4xlarge|16|30|EBS 전용|2,000|높음|0.796|
|c4.8xlarge|36|60|EBS 전용|4,000|10기가비트|1.591|

3) 고성능 GPU+CPU를 활용한 분석

|모델|GPU|vCPU|메모리(GiB)|GPU 메모리(GiB)|GPU P2P|가격(USD/hr)|
|---|---|---|---|---|---|---|
|p3.2xlarge|1|8|61|16|-|3.06|
|p3.8xlarge|4|32|244|64|NVLink|12.24|
|p3.16xlarge|8|64|488|128|NVLink|24.48|
|p3dn.24xlarge*|8|96|768|256|NVLink|31.212|
|p2.xlarge|1|4|61|12|높음|0.9|
|p2.8xlarge|8|32|488|96|10기가비트|7.2|
|p2.16xlarge|16|64|732|192|25기가비트|14.4|

---

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


