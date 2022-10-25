# git, github을 이용한 협업

## pull

```
git pull 저장소명 브랜치명 //pull = merge + fetch

// 이전 push시 -u 옵션 설정했다면 pull 로만 입력 가능
```

- 동료와 같은 브랜치에서 작업한다면 나의 로컬 브랜치와 원격 저장소 브랜치가 일치 해야만 `push` 할 수 있다.
- 예) 누군가 github에 `push`를 진행해서 나의 로컬과 github이 일치하지 않으면 `push` 할 수 없다.
- `git pull`을 이용해 내 로컬을 최신화 한 후 push를 진행 할 수 있다.

<br>

## 동료의 브랜치를 로컬로 가져오기

```
// 1.
git remote update
    // 내 로컬에 저장되어 있는 원격저장소의 브랜치리스트 최신화

// 2.
git branch -r
    // 원격 저장소의 브랜치 목록 표시.
    // 내 로컬브랜치와 이름중복 확인 후 그렇다면 로컬수정

// 3.
git switch 동료브랜치명
    //혹은
git checkout 동료브랜치명
    // 로컬에 없지만 원격에 존재하는 이름으로 이동시
    해당 원격 브랜치를
    // 로컬로 가져온다.

```

<br>

## git-hub pull request

- 깃헙의 풀리퀘스트 기능은 동료에게 나의 코드를 검증요청 하는 기능이다. 주로 자신의 브랜치를 메인으로 머지 하기 전 실행한다.

- draft pull request는 최종 머지 버전이 아니지만 검증받고 싶을 때 이용

- 리뷰어를 설정할 수 있다.

- 보통 머지 권한이 있는 시니어의 승인 후 머지 하게된다.