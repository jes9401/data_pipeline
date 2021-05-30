# elk 실습

- 프로그램들 시작 or 재시작

    ![elk](https://github.com/jes9401/data_pipeline/blob/main/image/elk/0.png?raw=true)

- 원하는 경로에 csv파일 옮기기

    ![elk](https://github.com/jes9401/data_pipeline/blob/main/image/elk/1.png?raw=true)

- cctv 정보 담을 인덱스 생성

    ```bash
    curl -X PUT localhost:9200/cctv?pretty
    ```

- cctv 인덱스 조회

    ```bash
    curl -X GET localhost:9200/cctv?pretty
    ```

- 같은 경로에 cctv_mapping.json 파일 생성 및 내용 작성

    ![elk](https://github.com/jes9401/data_pipeline/blob/main/image/elk/2.png?raw=true)

    - 내용

    ```json
    {
            "doc" : {
                    "properties" : {
                            "facility" : {
                                    "type" : "text"
                            },
                            "road" : {
                                    "type" : "text"
                            },
                            "address" : {
                                    "type" : "text"
                            },
                            "role" : {
                                    "type" : "text"
                            },
                            "count" : {
                                    "type" : "integer"
                            },
                            "pixel" : {
                                    "type" : "integer"
                            },
                            "direction" : {
                                    "type" : "text"
                            },
                            "archive" : {
                                    "type" : "integer"
                            },
                            "install_date" : {
                                    "type" : "date",
                                    "format" : "yyyy-MM"
                            },
                            "telephone" : {
                                    "type" : "text"
                            },
                            "location" : {
                                    "type" : "geo_point"
                            },
                            "data_date" : {
                                    "type" : "date",
                                    "format" : "yyyy-MM-DD"
                            },
                            "facility_code" : {
                                    "type" : "integer"
                            },
                            "facility_name" : {
                                    "type" : "text"
                            }
                    }
            }
    }
                                       
    ```

- 다음 명령어를 통해 맵핑

    ```bash
    curl -X PUT localhost:9200/cctv/doc/_mapping?include_type_name=true -d @cctv_mapping.json -H 'Content-Type: application/json'
    ```

- 현재 경로에 logstash.conf 파일 생성

    ```bash
    vi logstash.conf
    ```

- logstash.conf 파일 작성

    ```bash
    input {
            file {
              path => "/root/cctv.csv"   //실제 파일이 있는 지점으로 path 변경 후 주석 제거
              start_position => "beginning"  
              sincedb_path => "/dev/null" 
            }
          }
          filter {
            csv {
                separator => "," 
                columns => ["facility","road","address","role","count","pixel","direction","archive","install_date","telephone","latitude","longitude","data_date","facility_code","facility_name"]
            }   
            mutate {
              convert => {"latitude" => "float"}  
              convert => {"longitude" => "float"} 
            }
            mutate {
              rename => {
                "latitude" => "[location][lat]"  
              }
              rename => {
                "longitude" => "[location][lon]"
              }
            }
            mutate {
             convert => { "[location]" => "float" } 
            }
            mutate {
              remove_field => ["facility_code","facility_name"]  
            }
          }
          output {
              elasticsearch {
                  hosts => "localhost"  
                  index => "cctv"       
              }
              stdout {}
          }

    ```

- logstash.conf 파일 이동

    ```bash
    cp logstash.conf /etc/logstash/conf.d/logstash.conf
    ```

- 해당 명령어를 통해 정보 입력

    ```bash
    /usr/share/logstash/bin/logstash -f /etc/logstash/conf.d/logstash.conf
    ```

- 정보가 다 입력될 때까지 대기

- 브라우저에서 127.0.0.1:5601 접속 후 시각화 진행

- 인덱스 패턴 생성하기

    ![elk](https://github.com/jes9401/data_pipeline/blob/main/image/elk/3.png?raw=true)

    클릭 후 제일 아래로 내리기

    ![elk](https://github.com/jes9401/data_pipeline/blob/main/image/elk/4.png?raw=true)

    stack Management 선택

    ![elk](https://github.com/jes9401/data_pipeline/blob/main/image/elk/5.png?raw=true)

    인덱스 패턴 클릭

    ![elk](https://github.com/jes9401/data_pipeline/blob/main/image/elk/6.png?raw=true)

    create index pattern 클릭

    ![elk](https://github.com/jes9401/data_pipeline/blob/main/image/elk/7.png?raw=true)

    cctv* 입력 후 Next Step

    ![elk](https://github.com/jes9401/data_pipeline/blob/main/image/elk/8.png?raw=true)

    Time field를 data_date로 선택 후 생성

    ![elk](https://github.com/jes9401/data_pipeline/blob/main/image/elk/9.png?raw=true)

    Discover로 들어온 데이터 확인해보기

    ![elk](https://github.com/jes9401/data_pipeline/blob/main/image/elk/10.png?raw=true)

    필터를 cctv로 설정, 기간을 넉넉하게 2017년으로 설정하였음

    ![elk](https://github.com/jes9401/data_pipeline/blob/main/image/elk/11.png?raw=true)

    cctv데이터 이기 때문에 지도로 시각화

    ![elk](https://github.com/jes9401/data_pipeline/blob/main/image/elk/12.png?raw=true)

    Add layer 클릭 후 Clusters and grids 클릭

    ![elk](https://github.com/jes9401/data_pipeline/blob/main/image/elk/13.png?raw=true)

    인덱스 패턴, Geos 필드 확인 후 추가

    ![elk](https://github.com/jes9401/data_pipeline/blob/main/image/elk/14.png?raw=true)

    Map으로 시각화 완료