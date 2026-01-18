# 🛠 Ansible Server: AWS Infrastructure as Code (IaC)

이 저장소는 AWS VPC부터 Jenkins 서버, 로드밸런서, Auto Scaling 환경까지 **전체 프로젝트 인프라를 Ansible로 코드화하여 자동 구축·관리**하는 Infrastructure as Code(IaC) 프로젝트입니다.  
수동 콘솔 작업 없이 동일한 인프라 환경을 언제든 재현 가능하도록 설계했습니다.

---

## 🏗 Infrastructure Components
- **Network:** VPC, Public/Private Subnets, Internet Gateway, NAT Gateway
- **Compute:** EC2 (Jenkins Server, WAS Instances)
- **Traffic:** Application Load Balancer (ALB), Target Groups
- **Automation:** Ansible Playbooks & Roles (network, iam, security, jenkins, loadbalance, asg, dns)

---

## 🌟 Key Features
- **Idempotency (멱등성)**  
  동일 플레이북을 여러 번 실행해도 항상 동일한 인프라 상태 유지

- **Full Lifecycle Management**  
  자원 생성뿐 아니라 `cleanup.yml`을 통한 안전한 전체 인프라 회수 자동화

- **Security by Design**
