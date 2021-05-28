# centos7 설치 및 설정

- virtualbox, centos7
    - [참조 링크](https://blog.naver.com/chch1234569/222265855427)
    - cent os 설치

        [참조링크1(centos 설치)](https://blog.naver.com/chch1234569/222265855427)

        [참조링크2(파티션 관련)](https://gdtbgl93.tistory.com/166)

        - 참조링크1을 따라서 부팅까지 진행(유의 사항, 메모리 8GB 용량 100GB)

        - 키보드에 영어(미국) 추가

            ![centos](https://github.com/jes9401/data_pipeline/blob/main/image/centos7/cent0.png?raw=true)

        - 소프트웨어 선택을 누른 후 개발 및 창조를 위한 워크스텡션 선택

            ![centos](https://github.com/jes9401/data_pipeline/blob/main/image/centos7/cent1.png?raw=true)

        - 설치 대상을 눌러 "파티션을 설정합니다" 선택 후 완료 클릭

        - 해당 부분 클릭하면 파티션 생성

            ![centos](https://github.com/jes9401/data_pipeline/blob/main/image/centos7/cent2.png?raw=true)

        - 루트 디렉토리의 용량을 -2GB해서 적용해주고 파일 시스템을 ext4로 변경(밑 사진의 용량은 신경x)

            ![centos](https://github.com/jes9401/data_pipeline/blob/main/image/centos7/cent3.png?raw=true)

        - swap 용량을 최초 설정한 8GB에 +2GB를 한 10GB로 설정

            ![centos](https://github.com/jes9401/data_pipeline/blob/main/image/centos7/cent4.png?raw=true)

            ![centos](https://github.com/jes9401/data_pipeline/blob/main/image/centos7/cent5.png?raw=true)

        - boot 디렉토리의 파일 시스템도 ext4로 변경 (밑 사진 용량 신경 x)

            ![centos](https://github.com/jes9401/data_pipeline/blob/main/image/centos7/cent6.png?raw=true)

        - 완료 키를 누르고 변경 사항 적용

        - 네트워크 및 호스트명을 눌러 이더넷 활성화 시키기

            ![centos](https://github.com/jes9401/data_pipeline/blob/main/image/centos7/cent7.png?raw=true)

        - root 암호 및 사용자 생성

            ![centos](https://github.com/jes9401/data_pipeline/blob/main/image/centos7/cent8.png?raw=true)

        - 설치가 끝나면 os 재부팅 진행, 라이센스 동의 후에 네트워크 연결 확인하고 설정 완료 클릭
    - cpu2개 설정

        [참조 링크](https://technote.kr/180) 

        - 해당 가상머신의 설정버튼 클릭

            ![centos](https://github.com/jes9401/data_pipeline/blob/main/image/centos7/cent9.png?raw=true)

        - 설정-시스템-프로세서 프로세서 개수 2개로 설정

            ![centos](https://github.com/jes9401/data_pipeline/blob/main/image/centos7/cent10.png?raw=true)

        - 터미널에서 명령어 실행했을 때 core 2개로 나오는 것 확인

            ![centos](https://github.com/jes9401/data_pipeline/blob/main/image/centos7/cent11.png?raw=true)

    - selinux
        - 터미널에 sestatus 명령어 입력해서 상태 확인

            ![centos](https://github.com/jes9401/data_pipeline/blob/main/image/centos7/cent12.png?raw=true)

        - su - 명령어 실행 후

            vi /etc/selinux/config 명령어 실행

            ![centos](https://github.com/jes9401/data_pipeline/blob/main/image/centos7/cent13.png?raw=true)

        - SELINUX=disabled로 변경 후 저장

            i를 눌러 입력모드로 전환, esc → wq 엔터 누르면 저장

            ![centos](https://github.com/jes9401/data_pipeline/blob/main/image/centos7/cent14.png?raw=true)

        - vi /etc/sysconfig/selinux 명령어 실행해서 똑같이 진행
        - 
        - reboot 후 sestatus 명령어 입력해서 확인

            ![centos](https://github.com/jes9401/data_pipeline/blob/main/image/centos7/cent15.png?raw=true)

    - 방화벽
        - su - 명령어를 통해 root 계정으로 로그인 후

            systemctl disable firewalld 명령어 실행(재부팅시 방화벽 실행하지 않기)

            ![centos](https://github.com/jes9401/data_pipeline/blob/main/image/centos7/cent16.png?raw=true)

        - firewall-cmd —status 명령어 실행 후 not running 확인

            ![centos](https://github.com/jes9401/data_pipeline/blob/main/image/centos7/cent17.png?raw=true)