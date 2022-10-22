# 깃 기초

## 기초 명령어

### init

```
git init
```

- 프로젝트에서 깃을 사용하고 싶을 때 해당 프로젝트 폴더 `"내부"`에서 최초 1회 입력해야 할 명령어.

<br>

### add

```
git add file1.txt            // file1을 스테이징

git add file1.txt file2.txt  // file1와 file2를 스테이징

git add .                    //모든 변화한 file들을 스테이징
```

- 스테이징이란 `commit` 하고 싶은 파일들을 `commit` 전에 모아 놓는 것.
- `add`는 변화한 파일을 스테이징 하고 싶을 때 사용하는 명령어
- 파일이 새로 생성되거나 내용이 변경 되었을때만 add가 작동한다.

<br>

### commit

```
git commit -m "커밋 제목"   // 커밋함과 동시에 커밋의 제목을 기록(필수)

git commit -m "커밋 제목    // 커밋의 제목과 더불어 내용도 기록

커밋 내용"

```

- `commit`은 스테이징 된 파일을 로컬 저장소에 기록하는 것을 말한다.
- `commit`은 스테이징 된 파일이있어야 실행 할 수 있다.
- `commit`은 제목을 입력해야만 한다.
- `init` 후 첫 커밋 시 'master'라는 이름의 로컬 브랜치를 자동으로 생성하고 그곳에 커밋된다. 첫 커밋을 하기 위해서는 하나 이상의 파일을 생성해야한다.

<br>

### push

```
git push 저장소명 브랜치명  // 해장 저장소의 해당 브랜치로 push

git push -u 저장소명 브랜치명 // 앞으로 저장소, 브랜치 명 생략하고 push 가능

$ git config --global push.default current // 브랜치 파트에서 ㄱ
```

- `push`는 로컬의 커밋을 미리 연결 해 놓은 원격저장소로 저장해줌
- 브랜치 최소 메인 커밋 하나이상 있어야 실행됨
- `-u` 옵션은 실행되는 브랜치 기준임, 즉 브랜치마다 각각 -u를 설정하면 모든 브랜치에서 `push`만 짧게 입력 가능

<br>

### branch

```
git branch
    // 현재 프로젝트의 브랜치들을 보여준다. 별도의 브랜치를 추가하지 않은 상태라면 main or master 하나만 보임, 여러 브랜치가 있다면 현재 위치를 *와 색깔로 표시해줌

git branch 추가브랜치이름  // 새로운 브랜치를 추가함

git branch -m 새이름 // 현재 위치한 브랜치의 이름바꾸기

git checkout -b 추가브랜치 // 새 브랜치를 추가하고 이동함(편리..)
```

- 브랜치를 생성했다고 현재 위치가 새로생성한 곳으로 바뀌는 것은 아님
- 브랜치 생성 후 해당 브랜치의 첫 커밋이 이루어 져야 로컬에서 기존 브랜치와 새 브랜치가 완벽히 분리됨
- `-m` 은 `--move` 와 같은 옵션, 이름 바꿀때 사용함
- 프로젝트 생성후 자동으로 만들어진 브랜치명 `master`를 `main` 바꾸기 위해
  `git branch -M main`을 사용하라고 깃헙 안내가 나옴
- 바꾸는 이유는 master의 인종차별적 어감(?) 때문이라 함
- `-M` 은 `--move --force`와 같은 옵션 -m 으로 변경해도 잘되는듯 한데 깃허브 프로젝트 생성 안내에서는 -M을 쓰라고 한다.. 이유는(?)
- 로컬에서 새 브랜치를 만들고 원격저장소에 `push` 하면 원격저장소에도 브랜치가 생성된다.

<br>

### switch

```
git switch 브랜치이름     // 해당 브랜치로 이동(위치변경)
```

- `commit` 현재 위치한 브랜치에 적용이된다. 적용브랜치를 바꾸고 싶을때 `switch`를 사용
- 기존 `branch`에서 새 `branch`로 이어받은 파일을 수정한 경우 커밋 하기 전에는 `switch`할 수 없다(커밋 먼저 하라는 메세지뜸).
- 아예 새파일은 만든경우 하면 커밋 전이라도 switch 가능
- 이 경우 어느 브랜치에 위치한 채 파일을 생성했는가와 관계없이 해당 새 파일에 대한 commit이 이루어 지는 브랜치에 해당 파일이 최종적으로 위치하게된다.

<br>

### status

```
git status    // 현재 브랜치위치 및 stage 상태(add 되어있는 파일)를 알려줌
```

<br>

### log

```
git log                               // 현재 브랜치의 커밋 로그
git log --oneline                     // 간략히 보기
git log --oneline --all               // 다른 브랜치 커밋까지 모두보기
git log --oneline --graph --branches  // 그림형식으로 모두보기
```

<br>

### 프로젝트 시작하기

```
//1. github 에서 프로젝트 생성 (리드미 없이)
//2. 리액트 앱이라면 npx create-react-app => 기본깃폴더 삭제 후 진행(+리드미 생성 생략)

//3.
git init
echo "# 레포이름" >> README.md      //리드미 파일 생성 명령어
git add .
git commit -m "첫 커밋 메세지"
git remote add origin https://github.com/CSH111/레포이름.git
git remote add origin https://github.com/CSH111/
```
