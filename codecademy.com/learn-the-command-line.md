- 네비게이션 명령
    - ls, pwd, cd, mkdir, touch

- 명령어 옵션
    - ls -alt # 숨길 파일 포함, 긴 설명, 수정한 순으로 정렬

- 조작 명령
    - cp file1 file2 target_dir # 파일 복사 이동
    - cp m*.txt target_dir # 파일 복사 이동
    - cp file target_file # 파일 내용 복사 덮어쓰기
    - mv
    - rm -r

- 리다이렉션 명령
    - echo "hello" # "hello"를 받아 출력한다.
    - echo "hello" &gt; hello.txt # "hello"를 받아 hello.txt 파일에 덮어씌운다.
    - cat hello.txt
    - cat glaciers.txt &gt;&gt; hello.txt # "hello"를 받아 hello.txt 파일에 추가한다.
    - cat &lt; lakes.txt
    - cat volcanoes.txt | wc # 왼쪽 명령의 out을 오른쪽 명령의 in으로 보낸다.
    - sort lakes.txt &gt; sorted-lakes.txt

- 출력 명령
    - echo, cat, sort, uniq
    - grep -i Mount mountains.txt # Mount가 있는 라인을 대소문자 가리지 않고 찾아서 출력한다.
    - grep -R Desert /home/geography # Desert가 있는 라인을 경로 아래 모든 디렉토리에 있는 파일에서 찾아서 출력한다.
    - grep -Rl Desert /home/geography # Desert가 있는 파일을 경로 아래 모든 디렉토리에서  찾아서 출력한다.
    - sed 's/snow/rain/' forests.txt # 줄마다 첫 snow를 rain으로 바꿔서 출력한다.
    - sed 's/snow/rain/g' forests.txt # 모든 snow를 rain으로 바꿔서 출력한다.

- 터미널 환경설정
    - nano ~/.bash_profile # 환경설정을 담는 파일
    - source ~/.bash_profile # 현재 세션에 반영
    - .bash_profile
        - alias pd="pwd" # 별명
        - export USER="bsscco" # 사용자정의 환경변수
        - expert PS1="&gt;&gt; " # 프롬프트 환경변수

    - echo $USER # 사용자정의 환경변수 출력
    - echo $HOME # 홈 디렉토리 환경변수 출력
    - echo $PATH # 스크립트가 담겨있는 경로들을 세미콜론(;)으로 나눠놓은 환경변수
    - env # 환경변수 목록을 출력
