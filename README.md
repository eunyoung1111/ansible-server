# 🛠 Ansible Server: AWS Infrastructure as Code (IaC)

이 저장소는 AWS의 가상 네트워크 환경(VPC)부터 젠킨스 서버, 로드밸런서 등 전체 프로젝트 인프라를 Ansible을 통해 자동 구축하고 관리하는 코드를 포함하고 있습니다.

## 🏗 Infrastructure Components
- **Network:** VPC, Public/Private Subnets, Internet Gateway, NAT Gateway
- **Compute:** EC2 (Jenkins Server, WAS Instances)
- **Traffic:** Application Load Balancer (ALB), Target Groups
- **Automation:** Ansible Playbooks, Roles (Network, Server, Security)

## 🌟 Key Features
- **Idempotency (멱등성):** 동일한 플레이북을 여러 번 실행해도 일관된 인프라 상태 유지
- **Resource Management:** 자원 생성뿐만 아니라 사용 후 안전하게 회수하는 `cleanup.yml` 구현
- **Security:** 최소 권한 원칙에 따른 보안그룹(SG) 설계 및 IAM Role 기반 권한 관리

## 📝 Troubleshooting Case Study
### [NAT Gateway 의존성 및 자원 회수 루프 해결]
- **문제**: 인프라 삭제 시 NAT Gateway가 계속 새로 생성되거나, 의존성 문제로 VPC 삭제가 실패하는 현상
- **원인**: 기존 자원 조회 로직 부재로 인한 중복 생성 및 삭제 시 비동기 자원(ENI)의 회수 대기 시간 누락
- **해결**: `ec2_vpc_nat_gateway_info` 모듈로 기존 자원 유무를 먼저 확인하도록 로직을 개선하고, 삭제 태스크에 명시적인 `wait` 로직을 추가하여 완벽한 클린업 달성

## 🚀 How to Use
1. AWS CLI 및 Ansible 설치
2. `group_vars/all.yml`에 프로젝트 변수 설정
3. 인프라 구축: `ansible-playbook deploy-network.yml`
4. 인프라 파기: `ansible-playbook cleanup.yml`

## 📌 아키텍처
![architecture](images/AWS_architecture.png.png)
![ServiceAccessFlow](images/Service_Access_Flow.png)
