프로젝트 생성
VM 생성
방화벽규칙에서 http, https 포트를 전부 열어주기
https://cloud.google.com/sdk/docs/configurations
$ gcloud init
$ gcloud config configurations list
$ gcloud config configurations activate {name}
$ gcloud config configurations -h
$ gcloud compute instances list
$ gcloud compute scp [LOCAL_FILE_PATH] [INSTANCE_NAME]:~/
$ dpkg-reconfigure tzdata #GMT-9로 바꿔주기
$ netstat -tnlp
$ ps aux | grep node
$ nohup node app.js &
