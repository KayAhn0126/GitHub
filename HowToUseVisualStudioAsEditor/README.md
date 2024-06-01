# Gitbash에서 Visual Studio를 통해 파일 열기
- 파일을 수정할 때, 에디터를 Visual Studio로 설정하는 방법
- alias를 설정해 쉽게 여는 방법도 포함한다.

## 🍎 순서
- 후술할 devenv.exe 파일은 Visual Studio IDE를 시작하는 역할을 한다.
- 즉, 이 파일을 통해 내가 열고 싶은 파일을 여는것이다.
- Visual Studio의 실행 파일인 devenv.exe의 위치를 알아야 한다.
- 대부분 아래의 경로에 있다.
```bash
/c/Program Files/Microsoft Visual Studio/2022/Community/Common7/IDE/devenv.exe
```
- Gitbash에서 README.md 파일을 devenv.exe를 통해 열기 위해선 아래의 코드를 README.md의 위치에서 입력한다.
```bash
"/c/Program Files/Microsoft Visual Studio/2022/Community/Common7/IDE/devenv.exe" README.md
```
- 해당 경로에 있는 devenv.exe 실행 파일을 통해 README.md을 열겠다는 명령어.
    - 하지만 매번 README.md 파일이나 다른 파일을 열고 수정할 때, /c/...로 시작하는 경로를 일일하 다 입력할 순 없다.
    - 이러한 과정을 단순화해 사용하기 위해 alias를 설정하면 간편하게 사용할 수 있다.
- 먼저 GitBash에서 아래의 명령어를 입력해 현재 사용자의 홈 디렉토리로 위치를 이동한다.
```bash
cd ~
```
- 이미 설치되어 있는 기본 에디터를 통해 .bashrc 파일을 만든다.
```bash
nano .bashrc
```
- 참고)
    - .bashrc 파일은 사용자가 로그인할 때마다 실행되지 않고, 각 새로운 Bash 셸 세션(예: 터미널 창이나 Git Bash 창을 열 때)마다 실행된다.
- .bashrc 파일을 기존에 생성하지 않았다면 현재는 아무것도 없는 상태여야 정상이다. 여기에 아래와 같이 alias를 설정한다.
```bash
alias vs2022='"/c/Program Files/Microsoft Visual Studio/2022/Community/Common7/IDE/devenv.exe"'
```
- 입력했다면 저장하고 빠져나와서 .bashrc를 다시 로드한다.
```bash
source ~/.bashrc
```
- 참고)
    - '~/' 의 의미는..
    - ~ <- 현재 사용자의 홈 디렉토리
    - '/' <- 내부의
    - 즉, 현재 사용자의 홈 디렉토리 내부의 .bashrc를 다시 로드한다는 뜻.
- 마지막으로 설정된 alias로 수정하고 싶은 파일을 수정하면 끝.
```bash
vs2022 README.md
```