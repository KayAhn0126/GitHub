# Github Commands

## 🍎 작업 상태
- modified - 수정은 되었지만 로컬 저장소에 커밋하지 않은 상태
- staged - Staging Area에 추가된 상태
- commited - 커밋한 상태
- pushed - 원격 저장소로 밀어넣은 상태

## 🍎 현재 폴더에 적용된 Configuration 보기
- 터미널에서 git config --list로 현재 폴더에 적용된 설정값(configuration)들을 알 수 있다.
- 처음엔 git config --list를 하면 나의 정보를 보여주는것으로 생각했지만, 그것이 아니라 내가 현재 위치하고 있는 폴더와 연동되어있는 configuration을 보여주는것이다.
- 즉, A라는 폴더에서 git config --list를 하면 A에 설정된 git configuration을 보여주는것.

## 🍎 새로운 파일 추가 후 저장소 초기화
- 보통 Github 웹사이트에서 repo 생성 후 HTTPS url을 이용해 clone을 받아 작업을 시작한다.
- 폴더을 생성하고 터미널로 해당 폴더에서 git init을 해주면 .git(안보임)이 생성되고 깃 저장소로 만들어준다.

## 🍎 수정된 부분 확인하기
- unstaged + modified 상태에서만 확인할 수 있다.
```bash
git diff
```

## 🍎 특정 파일을 추적 대상에서 제외 시키기
```bash
git rm --cached README.md 
git status
```
- Git에서 특정 파일을 인덱스(stage)에서 제거하지만, 작업 디렉토리에서 실제 파일은 삭제하지 않는 명령어.
- 이 명령어를 사용하면 파일이 Git의 추적 대상에서 제외되지만, 로컬 디렉토리에서는 그대로 남아 있게된다.

## 🍎 git add 명령어로 staging한 파일들을 unstaged 상태로 되돌리기
- 현재 stage 상태의 모든 파일을 unstaged 상태로 되돌리는 명령어
```bash
git reset
```
- 특정 파일을 unstaged 상태로 되돌리는 명령어
```bash
git reset README.md
```

## 🍎 브랜치 생성
- **로컬**
```bash
git branch STEP1
```
- **원격**
```bash
git push --set-upstream origin STEP1

            or

git push -u origin STEP1 (recommended)
```
- **git push -u remote branch name** 분석
    - **-u**는 원격 레포지토리에 성공적으로 push된 모든 브랜치에 tracking ref를 생성한다. 그로인해 한번 리모트와 연결되면 로컬 브랜치에서 push를 할 때 자동으로 원격 브랜치로 연결된다. 이것은 pull을 할때에도 마찬가지로 원격 브랜치에서 다른 인자 없이 바로 pull을 받을수 있도록 해준다.    
    - **remote**는 변경사항이 저장될 원격 저장소의 이름이 된다. 만약 원격 레포지토리를 클론했다면 `origin`이라는 이름 아래 remote 레포지토리의 이름이 담겨있다. 또한, 원격 레포지토리의 URL을 사용해도 된다.
    - **branch name**은 변경사항이 적용될 원격저장소의 branch이다.
    - [분석 원본](https://www.educative.io/answers/what-is-the-git-push--u-remote-branch-name-command?utm_campaign=systemdesign&utm_source=google&utm_medium=ppc&utm_content=display&eid=5082902844932096&utm_term=&utm_campaign=%5BNew%5D+System+Design+-Performance+Max&utm_source=adwords&utm_medium=ppc&hsa_acc=5451446008&hsa_cam=18511913007&hsa_grp=&hsa_ad=&hsa_src=x&hsa_tgt=&hsa_kw=&hsa_mt=&hsa_net=adwords&hsa_ver=3&gclid=CjwKCAjw2OiaBhBSEiwAh2ZSP8yGMunodXadSAeKWcm-Sl7whsFHKAFMPM0DgV9LO0hf1x-23ICBYxoCNjMQAvD_BwE)

## 🍎 브랜치 삭제
- **로컬**
```bash
git branch -d STEP1
```
- 로컬 브랜치를 강제로 삭제하려면 `--delete --force:`의 바로 가기인 -D 옵션을 사용.
```bash
git branch -D STEP1
```
- **원격**
```bash
git push origin -d STEP1
```
## 🍎 브랜치 병합
- 만약 STEP1 브랜치를 main브랜치에 병합하고 싶다면 main 브랜치로 이동 후 아래와 같이 커맨드 입력.
```bash
git merge STEP1
git push
```
- 만약, main 브랜치와 STEP1 브랜치가 같은 조상 커밋을 공유하고, 병합 하는 브랜치가 분기 후손이 없을때(main -> 병합하는 브랜치, STEP1 -> 병합 당하는 브랜치) 일반적으로 하는 'git merge STEP1'을 적용하면 "원래부터 Main에서 직접 작업한것" 처럼 합병된다.
    - 이것을 "fast-forward" merge라고 한다.
- fast-forward merge는 '같은 조상을 가지고 현재 브랜치가 후손 커밋이 없을때, 다른 브랜치에서 커밋된 상태를 그대로 따라가겠다' 의미이다.
- fast-forward merge 경우 안 좋은점이 있는데, 어느 브랜치에서 작업이 이루어졌는지 확인할 수 없다.
![](https://i.imgur.com/0JYUOAi.png)
- 마지막 커밋 "가입화면 구현"은 login_UI_minor_feature에서 작업이 되었고 커밋도 해당 브랜치에서 진행이 되었지만 main 브랜치가 login_UI_minor_feature 브랜치를 f-f merge를 하면 위의 사진과 같이 어디서 작업이 이루어 졌는지 확인 할 수 없다.
- 이 경우는 '**-no-ff**' 플래그 사용으로 f-f merge를 방지할 수 있다.
- 사용법
    ```bash
    git merge --no-ff STEP1 
    ```
- **적용 후**
    ![](https://i.imgur.com/HoauNyX.png)
    ```bash
    git merge --no-ff login_UI_minor_feature
    ```

## 🍎 커밋 후 커밋 메세지 변경
```bash
git commit --amend
```

## 🍎 unstaged 상태의 파일 discard
```bash
git restore .
```

## 🍎 같은 프로젝트 내 다른 브랜치 가져오기
- 만약 STEP1의 내용을 그대로 다른 브랜치로 가져와 기능을 추가하고 싶다면
- 먼저 가져오고 싶은 내용이 있는 브랜치(STEP1)로 이동 후 아래 command 입력
```bash
git checkout -b STEP2
```
- 위의 command는 (현재 STEP1 브랜치에 있다고 가정) **현재 STEP1이 가지고 있는 내용을 STEP2라는 브랜치에 복사하고 STEP2로 checkout까지 한다**는 의미
- 그럼 현재 HEAD는 어디에? -> STEP2! 
- 이제 원격 저장소에도 방금 생긴 브랜치를 만들어준다.
```bash
git push -u origin STEP3
```

## 🍎 .DS_Store 삭제 방법
- 저장소 상위 디렉토리에서 현재 디렉토리 아래의 모든 .DS_Store 파일을 제거
```bash
find . -name .DS_Store -print0 | xargs -0 git rm -f --ignore-unmatch
```
- 만약, 앞으로도 .DS_Store 파일을 업로드하지 않을거라면,
- 저장소 상위 디렉토리에 .gitignore 파일 생성 및 .DS_Store 파일 추가
```bash
echo .DS_Store >> .gitignore
```
- 변경 사항을 원격 저장소에 push
```bash
git add --all
git commit -m '.DS_Store removed'
git push origin main
```

## 🍎 dquote > 를 만났을때
- 커밋 메세지의 무언가가 잘못되었다는것이다.
- ctrl + g를 눌러 탈출하고 다시 예쁘게 커밋 메세지를 작성하자.

## 🍎 git stash
- [git stash](https://gmlwjd9405.github.io/2018/05/18/git-stash.html)

## 🍎 줄 단위로 커밋하기
- git add -p
[김정환님블로그](https://jeonghwan-kim.github.io/dev/2020/02/10/git-usage.html)

## 🍎 merging 상태
- merging 상태는 병합 도중 충돌이 발생했을 때 나타나는 상태.
    - 충돌 파일 확인:
        - 병합 중 충돌이 발생한 파일을 확인한다.
        - 아래의 명령어를 실행하면 충돌된 파일들이 both modified 상태로 표시될 것이다.
        - git status
    - 충돌 해결:
        - 충돌된 파일을 열어보면 충돌이 발생한 부분에 다음과 같은 형식의 구분선이 있다.
        ```text
        <<<<<<< HEAD
        (현재 브랜치 내용)
        =======
        (병합 중인 다른 브랜치 내용)
        >>>>>>> (브랜치 이름 또는 커밋 ID)
        ```
    - 수정 완료 후 add:
        - 충돌이 발생한 파일을 수정한 후, 수정된 파일을 staging area에 추가한다.
        ```bash
        git add <filename>
        ```
    - 병합 완료 / 병합 취소
        ```bash
        // 병합 완료
        git merge --continue
        
        // 병합 취소
        git merge --abort
        ```

## 🍎 Citation
[merge](https://mylko72.gitbooks.io/git/content/branch/bcd1_d569.html)
[how to not commit on same ancestors](https://barbagroup.github.io/essential_skills_RRC/git/branching/#git-merge) 
[git의 origin](https://velog.io/@seochanh/00011)
[깃의 되돌리기](https://git-scm.com/book/ko/v2/Git%EC%9D%98-%EA%B8%B0%EC%B4%88-%EB%90%98%EB%8F%8C%EB%A6%AC%EA%B8%B0)
[커밋 또는 push된 내용 되돌리기](https://brownbears.tistory.com/477)
[내용 되돌리기](https://jupiny.com/2019/03/19/revert-commits-in-remote-repository/)
[git stash](https://gmlwjd9405.github.io/2018/05/18/git-stash.html)