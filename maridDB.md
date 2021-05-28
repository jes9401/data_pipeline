# maridDB설치

[참조 링크](https://bamdule.tistory.com/59)

- vi /etc/yum.repos.d/MariaDB.repo 명령어 실행

    ![mariaDB](https://github.com/jes9401/data_pipeline/blob/main/image/mariaDB/maria0.png?raw=true)

- 빈 파일에 해당 내용 작성 후 저장

    ![mariaDB](https://github.com/jes9401/data_pipeline/blob/main/image/mariaDB/maria1.png?raw=true)

- yum install MariaDB 명령어를 통해 설치

- rpm -qa | grep MariaDB 명령어를 통해 설치 확인

    ![mariaDB](https://github.com/jes9401/data_pipeline/blob/main/image/mariaDB/maria2.png?raw=true)

- systemctl start mariadb 명령어 → mariaDB 실행

- /usr/bin/mysqladmin -u root password '변경한 비밀번호'

- netstat -anp | grep 3306 명령어 실행 후 확인

    ![mariaDB](https://github.com/jes9401/data_pipeline/blob/main/image/mariaDB/maria3.png?raw=true)

- vi /etc/my.cnf 설정 파일 들어가서 해당 내용 추가

    (characterSet을 utf8mb4로 변경)

    ![mariaDB](https://github.com/jes9401/data_pipeline/blob/main/image/mariaDB/maria4.png?raw=true)

- systemctl restart mariadb 명령어 사용해서 재시작

- mysql -u root -p 로 실행 후

    show variables like 'c%'; 명령어 통해 확인

    ![mariaDB](https://github.com/jes9401/data_pipeline/blob/main/image/mariaDB/maria5.png?raw=true)

- 리붓 시 자동으로 실행되도록 설정

    ![mariaDB](https://github.com/jes9401/data_pipeline/blob/main/image/mariaDB/maria6.png?raw=true)