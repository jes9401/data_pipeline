# Apache, Tomcat 설치

[참조링크1(아파치,톰캣 설치 및 설명)](https://developerhjg.tistory.com/171)

- Apache 설치
    - yum list installed | grep httpd 명령어를 통해 설치되어 있는지 확인

        ![Apache&Tomcat](https://github.com/jes9401/data_pipeline/blob/main/image/Apache&Tomcat/0.png?raw=true)

    - 설치가 안돼있을 경우

        yum install -y httpd 명령어를 통해 설치 후 다시 확인

        ![Apache&Tomcat](https://github.com/jes9401/data_pipeline/blob/main/image/Apache&Tomcat/1.png?raw=true)

    - 주요 디렉토리 설명

        ![Apache&Tomcat](https://github.com/jes9401/data_pipeline/blob/main/image/Apache&Tomcat/2.png?raw=true)

        ![Apache&Tomcat](https://github.com/jes9401/data_pipeline/blob/main/image/Apache&Tomcat/3.png?raw=true)

    - 재부팅시 실행되게 설정하는 명령어

        서비스 시작하는 명령어 입력

        ![Apache&Tomcat](https://github.com/jes9401/data_pipeline/blob/main/image/Apache&Tomcat/4.png?raw=true)

    - 브라우저에 아이피를 입력해서 접속 확인 진행 해당 화면이 나오면 아파치 설치 및 구동 완료

        ![Apache&Tomcat](https://github.com/jes9401/data_pipeline/blob/main/image/Apache&Tomcat/5.png?raw=true)

    - /et/httpd/conf/httpd.conf 파일을 vi로 열면 아래와 같은 내용이 있음, DocumentRoot 부분을 보면 해당 위치에 문서를 위치시키면 화면에 뿌려 준다는 뜻

        ![Apache&Tomcat](https://github.com/jes9401/data_pipeline/blob/main/image/Apache&Tomcat/6.png?raw=true)

    - /var/www/html 폴더로 이동 후 index.html 파일을 생성하고 적당히 페이지 작성

        ![Apache&Tomcat](https://github.com/jes9401/data_pipeline/blob/main/image/Apache&Tomcat/7.png?raw=true)

    - 아래로 좀 더 내려보면 index.html을 기본 문서로 지정한 걸 볼 수 있음, 실제로 해당 디렉토리에 파일이 존재하지 않기 때문에 아까와 같은 화면이 보여지는 것임

        ![Apache&Tomcat](https://github.com/jes9401/data_pipeline/blob/main/image/Apache&Tomcat/8.png?raw=true)

         

    - 홈페이지 화면이 바뀐 것을 확인할 수 있음

        ![Apache&Tomcat](https://github.com/jes9401/data_pipeline/blob/main/image/Apache&Tomcat/9.png?raw=true)

- Tomcat 설치
    - yum list installed | grep tomcat 명령어를 통해 설치 유무 확인

        ![Apache&Tomcat](https://github.com/jes9401/data_pipeline/blob/main/image/Apache&Tomcat/10.png?raw=true)

    - yum install -y tomcat* 명령어를 통해 설치

    - 설치 경로는 /usr/share/tomcat 에서 확인

    - systemctl enable tomcat (리붓 시 자동실행)

    - systemctl start tomcat (서비스 시작)

    - 브라우저 주소창에 127.0.0.1:8080 입력 후 접속 확인

        ![Apache&Tomcat](https://github.com/jes9401/data_pipeline/blob/main/image/Apache&Tomcat/11.png?raw=true)

- 연동
    - yum install gcc gcc-c++ httpd-devel  명령어 입력
        - mod_jk 설치를 위해 gcc,  gcc-c++, httpd-devel 세 가지 패키지 설치

    - [다운로드 링크](http://tomcat.apache.org/download-connectors.cgi) ← 링크 클릭 후 해당 부분 우클릭 후 링크 주소 복사 클릭

        ![Apache&Tomcat](https://github.com/jes9401/data_pipeline/blob/main/image/Apache&Tomcat/12.png?raw=true)

    - 터미널에 wget -c 링크주소 입력해서 다운로드

    - tar zxvf tomcat-connector*  명령어로 압축 해제

    - 압축 해제 후 해당 폴더의 하위 폴더 native로 이동

        ![Apache&Tomcat](https://github.com/jes9401/data_pipeline/blob/main/image/Apache&Tomcat/13.png?raw=true)

    - 명령어 사용해서 Makefile 생성

        ![Apache&Tomcat](https://github.com/jes9401/data_pipeline/blob/main/image/Apache&Tomcat/14.png?raw=true)

    - make 명령어로 컴파일 실행

    - make install 실행

    - install 후 /etc/httpd/modules 경로에 mod_jk.so 파일 생성 확인

        ![Apache&Tomcat](https://github.com/jes9401/data_pipeline/blob/main/image/Apache&Tomcat/15.png?raw=true)

    - 뒤에 과정 너무 복잡.. 링크 따라하면됨