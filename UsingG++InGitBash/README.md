# Using G++ In GitBash
- GitBash에서 G++ 컴파일러를 사용해 C++ 파일 컴파일 하는 방법을 기술.
- 이 방법은 Windows 전역에 컴파일러를 설치하는 방법으로 GitBash 뿐만 아니라 PowerShell에서도 동일하게 사용 가능.

## 🍎 설치 방법
- 설치는 큰 카테고리에서, seh 파일을 다운로드, 압축 풀기, 폴더 위치 변경, 환경 변수 설정, 버전 확인 순서로 진행된다.

### 📖 다운로드
- sourceforge.net이라는 웹사이트에서 MinGW64를 설치해야 한다.
- 아래의 웹사이트 주소로 접속하면 상단에 "MinGW-w64 - for 32 and 64 bit Windows"라고 적힌 페이지를 볼 수 있다.
    - [MinGW64 Download](https://sourceforge.net/projects/mingw-w64/files/)
- files 탭이 선택되었는지 확인하고 스크롤을 내려 MinGW-W64 GCC-8.1.0 카테고리로 온다.
- 아래와 같은 카테고리를 볼 수 있다면 "x86_64-posix-seh"를 다운로드한다.

![sourceforge](https://github.com/KayAhn0126/GitHub/assets/40224884/844787d3-7a08-49da-ba85-c18c1882e483)

### 📖 압축 풀기
- 다운로드하게 되면 "x86_64-8.1.0-release-posix-seh-rt_v6-rev0.7z"라는 압축 폴더을 볼 수 있다.
    - 바탕화면을 경로로 잡고 해당 압축 폴더를 풀어준다.
    - 그럼 동일한 이름의 폴더가 생기는데 이 폴더 안에 들어가면 "mingw64"라는 폴더가 하나 있는것을 볼 수 있다.
    
### 📖 폴더 위치 변경
- 이 폴더를 "C:\Program Files" 경로에 넣어준다.
- 그럼 mingw64의 현재 경로는 "C:\Program Files\mingw64"임을 확인할 수 있다.

### 📖 환경 변수 설정
- Windows에서 GCC, G++ 컴파일러를 사용하기 위해선 환경변수를 설정 해야한다.
- 윈도우 키 -> "시스템 환경변수 편집" 입력 -> 고급 탭 선택 -> 환경변수 클릭 -> 시스템 변수
    - 변수 이름을 "PATH"로 설정할건데, 
    - 만약 PATH 라는 변수가 이미 존재한다면 아래와 같이 ';'(세미콜론)을 사용해 기존 경로에 덧붙여 추가할 수 있다.
        - "C:\Windows\System32;C:\Program Files\mingw64\bin"
            - 여기서 "C:\Windows\System32"는 기존에 PATH에 저장되어 있던 값. 여기에 새로운 값을 추가해 주기 위해 세미콜론 사용.
    - PATH 라는 변수가 존재하지 않는다면, mingw64의 경로 + \bin을 추가해 윈도우에서 전역에서 bin 폴더 내 존재하는 GCC, G++ 컴파일러를 사용할 수 있게 한다.
        - "C:\Program Files\mingw64\bin"
- 확인을 눌러 종료한다.

### 📖 버전 확인
- GitBash 또는 Windows PowerShell에서 "gcc -v" 명령어와 "g++ -v" 명령어를 통해 정상적으로 설치 되었는지 확인하면 설치는 완료.

## 🍎 사용 방법
- cpp 파일 생성 -> 코드 작성 -> 실행
```bash
// cpp 파일 생성
touch hello.cpp 

// 코드 작성
vs 2022 hello.cpp

// 전처리 -> 컴파일 -> 링킹 과정까지 진행 후 a.exe 실행 파일 생성 이후 ./a.exe 명령어로 파일 실행
g++ hello.cpp 

// 위와 동일한 과정을 거치지만 이름을 사용자가 원하는대로 설정 가능
g++ hello.cpp -o myFirstProgram
```
- "-c" 옵션을 사용해 Linking 전까지만 진행해 목적 파일(*.o)를 얻는 방법과, "-g" 옵션을 사용해 디버깅을 용이하게 할 수도 있다.

## 🍎 PATH 환경변수
- 어떻게 화면에 g++ 명령어만으로 cpp 파일을 컴파일을 할 수 있을까? → 환경변수 덕분이다.
- 사용자가 명령 프롬프트(PowerShell or GitBash)에서 g++를 입력하게 되면 아래와 같은 절차로 g++ 실행파일(.exe)을 찾는다.
    - 먼저 현재 작업 디렉토리에서 g++.exe라는 실행 파일을 찾는다.
    - 현재 디렉터리에 g++.exe 파일을 찾을 수 없다면, 환경변수 PATH에 저장된 디렉터리들을 순차적으로 검색하면서 g++라는 실행파일(.exe)를 찾는다.
    - 환경변수에 저장된 디렉터리에 있다면 해당 실행파일을 실행해 cpp 파일을 컴파일한다.
    - 없다면 "command not found"를 반환한다.

## 🍎 참고 자료
- [GitBash or Windows에서 GCC, G++ 사용하기](https://sooseongcom.com/post/MinGW-w64-HowToInstall)
- [G++로 C++ 컴파일하기](https://sooseongcom.com/post/gppbuild)