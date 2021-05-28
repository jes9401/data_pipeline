# maridDB설치

[참조 링크](https://bamdule.tistory.com/59)

- vi /etc/yum.repos.d/MariaDB.repo 명령어 실행

    ![maridDB%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8E%E1%85%B5%20d6556e70941e4a2d82e49fda017a35f7/Untitled.png](maridDB%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8E%E1%85%B5%20d6556e70941e4a2d82e49fda017a35f7/Untitled.png)

- 빈 파일에 해당 내용 작성 후 저장

    ![maridDB%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8E%E1%85%B5%20d6556e70941e4a2d82e49fda017a35f7/Untitled%201.png](maridDB%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8E%E1%85%B5%20d6556e70941e4a2d82e49fda017a35f7/Untitled%201.png)

- yum install MariaDB 명령어를 통해 설치

- rpm -qa | grep MariaDB 명령어를 통해 설치 확인

    ![maridDB%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8E%E1%85%B5%20d6556e70941e4a2d82e49fda017a35f7/Untitled%202.png](maridDB%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8E%E1%85%B5%20d6556e70941e4a2d82e49fda017a35f7/Untitled%202.png)

- systemctl start mariadb 명령어 → mariaDB 실행

- /usr/bin/mysqladmin -u root password '변경한 비밀번호'

- netstat -anp | grep 3306 명령어 실행 후 확인

    ![maridDB%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8E%E1%85%B5%20d6556e70941e4a2d82e49fda017a35f7/Untitled%203.png](maridDB%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8E%E1%85%B5%20d6556e70941e4a2d82e49fda017a35f7/Untitled%203.png)

- vi /etc/my.cnf 설정 파일 들어가서 해당 내용 추가

    (characterSet을 utf8mb4로 변경)

    ![maridDB%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8E%E1%85%B5%20d6556e70941e4a2d82e49fda017a35f7/Untitled%204.png](maridDB%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8E%E1%85%B5%20d6556e70941e4a2d82e49fda017a35f7/Untitled%204.png)

- systemctl restart mariadb 명령어 사용해서 재시작

- mysql -u root -p 로 실행 후

    show variables like 'c%'; 명령어 통해 확인

    ![maridDB%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8E%E1%85%B5%20d6556e70941e4a2d82e49fda017a35f7/Untitled%205.png](maridDB%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8E%E1%85%B5%20d6556e70941e4a2d82e49fda017a35f7/Untitled%205.png)

- 리붓 시 자동으로 실행되도록 설정

    ![maridDB%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8E%E1%85%B5%20d6556e70941e4a2d82e49fda017a35f7/Untitled%206.png](maridDB%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8E%E1%85%B5%20d6556e70941e4a2d82e49fda017a35f7/Untitled%206.png)