# xe3-docker
내가 도커파일을 세심하게 정리할 시간이 없어서 아직 불편하지만 작동버전을 올려 놓았다.
사전 작업으로 
  1. 로칼에 볼률 디렉토리를 생성한다.
    mkdir db_data
    mkdir html
    mkdir log
  2. xpressengine/files에 있는 파일들을 html/에 복사한다.
     cp ./xpressengine/files/.xe_install_config.j2 html/
     cp ./xpressengine/files/entrypoint.sh html/.
     
 마지막으로 docker-compose up -d --build 하면 된다.
