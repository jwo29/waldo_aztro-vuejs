# waldo project 

## aztro-vue

첫번째 왈도해적단 프로젝트.<br>
Dockerfile을 작성하여 vue.js 프로젝트를 띄워보기<br>

aztro API를 호출하여 daily horoscope 정보를 얻고<br>
vue.js로 화면에 표현하기



## How to write the Dockerfile

* FROM: 베이스 이미지

* MAINTAINER: 이미지를 생성한 개발자의 정보 (1.13.0 이후 사용 X)
* LABEL: 이미지에 <i>key-value</i> 형태의 메타데이터를 추가
* RUN: 새로운 레이어에서 명령어를 실행하고, 새로운 이미지를 생성
  * RUN 명령어를 실행할 때마다 레이어가 생성되고 캐시됨
  * 따라서 RUN 명령어를 따로 실행하면 <i>apt-get update</i>는 다시 실행되지 않아서 최신 패키지를 설치할 수 <strong>없음</strong>
  * 반대로 최신 패키지를 설치하려면 하나의 RUN 명령에 apt-get update와 install을 같이 사용하면 됨
* WORKDIR: 작업 디렉토리를 지정. 해당 디렉토리가 없으면 새로 생성
  * 작업 디렉토리를 지정하면 그 이후 명령어는 해당 디렉토리를 기준으로 동작함
  * <i>cd</i> 명령어와 동일함
* EXPOSE: Dockerfile의 빌드로 생성된 이미지에서, 열어줄 포트를 의미함
  * 호스트 머신과 컨테이너의 포트를 매핑할 때 사용됨
  * 컨테이너 생성 시 -p 옵션에 컨테이터 포트 값으로 EXPOSE 값을 적어야 함
* USER: 이미지를 실행할 계정을 지정
  * 기본적으로 root 계정으로 설정
* COPY/ADD: build 명령 중간에 호스트의 파일 또는 폴더를 이미지로 가져옴
  * ADD 명령문은 좀 더 파워풀한 COPY 명령이라고 생각할 수 있음(조사 후 내용 추가/수정)
  * ADD 명령문은 일반 파일 뿐만 아니라 압축 파일이나 네트워크 상의 파일도 사용 가능하기 때문
  * 위와 같은 특수한 파일을 다루는 게 아니라면 COPY 명령문을 사용하는 것이 권장됨
* ENV: 이미지에서 사용할 환경 변수 값을 지정
  * path 등
* CMD/ENTRYPOINT: 컨테이너를 생성/실행할 때의 사용할 명령어
  * docker run 으로 컨테이너를 생성하거나, docker start 로 정지된 컨테이너를 시작할 때 사용
    * 보통 컨테이너 내부에서 항상 돌아가야 하는 서버를 띄울 때 사용(데몬)
  * CMD
    * CMD는 <i>docker run</i> 실행 시, 추가적인 명령어에 따라 설정한 명령어를 수정하고자 할 때 사용됨
    * CMD 명령은 세가지 형태가 있음
      * <i>CMD [“executable”,”param1”,”param2”]</i>
      * <i>CMD [“param1”,”param2”]</i>
      * <i>CMD command param1 param2</i>
    * <strong>CMD는 Dockerfile 내부에 여러 줄 작성할 수 있지만, 결국 가장 마지막 한줄만 수행됨</strong>
  * ENTRYPOINT
    * ENTRYPOINT는 docker run 실행 시, 추가적인 명령어의 존재 여부와 상관 없이 무조건 실행되는 명령
    * ENTYPOINT 명령은 두가지 형태가 있음
      * <i>ENTRYPOINT [“executable”, “param1”, “param2”]</i>
      * <i>ENTRYPOINT command param1 param2</i>