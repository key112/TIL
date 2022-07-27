# Day03
>2022년 07월 27일

## Git workflow
>협업을 위해 `brach`를 사용함 (master는 사용 안함)
>>- 원격 저장소 소유권이 있는 경우 (Shared repository model)
>>- 원격 저장소 소유권이 없는 경우 (Fork & Pull model)

### 원격 저장소 소유권이 있는 경우 (Shared repository model)
    - 원격 저장소가 자신의 소유거나 collaborator로 등록되어 있는 경우
    - 브랜치를 따로 만들어야됨
    - **Pull Request** 사용

- 소유자의 주소로 클론을 생성
- 브런치 생성해서 작업
- 브랜치를 psuh
- 저장소에 브런치 반영되면 Pull Request를 통해 브랜치를 반영해달라고 요청
- 병합 완료되면 원격저장소에서 완료된 브런치 삭제
- 각자 브런치에서 마스터로 이동
- 원격저장소에서 pull로 업데이트
- 각자 쓰던 브런치 삭제
- 위 반복

### 원격 저장소 소유권이 없는 경우 (Fork & Pull model)
    - 오픈소스같이 자기소유가 아닌 원격 저장소 사용
    - 원격 저장소를 내 원격저장소에 복제(fork라고함)
    - 기능완성후 psuh는 내 원격저장소에!!
    - Pull Request를 통해 원격 저장소에 반영

- fork를 통해 내 원격저장소에 복제
- 내 원격저장소 주소로 clone받음
- 원래 주소로 동기화 (upstream)
- 브랜치 생성후 작업
- 작업 완료후 내 원격 저장소로 push
- Pull Request를 통해 원래 원격저장소에 반영해달라고 요청
- 요청 완료후 마스터 병합되면 내 원격저장소 브런치 삭제
- 원래 원격저장소에서 pull로 업데이트
- 반복

## reset, revert

### reset
> 말그대로 리셋
> git reset [옵션] <커밋 ID> 형태

- soft
  - staging area로 돌려놓음 (commit 하기 전 상태)
  - 바로 커밋가능

- mixed
  - ***reset의 기본값***
  - working directory로 돌려놓음(add 하기 전 상태)
  - unstage 된 상태

- hard 
   - commit된 파일들(tracked 파일들)은 모두 working directory에서 삭제
   - Untracked 파일은 Untracked로 남음
   - 혹시나 이미 삭제한 커밋으로 다시 돌아가고 싶다면? → ***git reflog***를 사용합니다

### revert
>git reset은 쉽게 과거로 돌아갈 수 있다는 장점이 있지만, 커밋 내역이 사라진다는 단점이 있습니다.

- git revert <커밋 아이디> 형태
- git reset은 커밋 내역을 삭제하는 반면, git revert는 `새로 커밋을 쌓는다`는 차이가 있습니다
 ![이미지](https://hphk-edu.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fb064d541-aa3e-48a1-ae07-2c85aed68d40%2FUntitled.png?table=block&id=6733af45-9a6f-4159-9808-7a72e630b279&spaceId=f7ab64f0-6613-4035-b609-06b6865d9b61&width=2000&userId=&cache=v2)


  **주의사항**

 - git reset과 비슷하다는 이유로 다음 사항이 혼동될 수 있습니다.

- git reset --hard 5sd2f42라고 작성하면 5sd2f42라는 커밋으로 돌아간다는 뜻입니다
- git revert 5sd2f42라고 작성하면 5sd2f42라는 커밋을 되돌린다는 뜻입니다


## Undoing(되돌리기)
>git status에 나와있음
### git restore
- git restore <파일 이름>형식
- Git의 추적이 되고 있는, 즉 버전 관리가 되고 있는 파일만 되돌리기가 가능합니다

    한 번 git restore를 통해 수정을 취소하면, 해당 내용을 복원할 수 없으니 주의 바랍니다!

### git rm --cached, git restore --staged
>git add를 통해서 파일을 Staging Area에 올렸을때 다시 Unstage상태로 되돌리기

- **git rm --cashed**는 commit이 하나도없을때 **git restore --staged**는 commit이 하나이상 있을때

### git commit --amend
1. Staging Area에 새로 올라온 내용이 없다면, 단순히 `직전 커밋의 메시지만 수정`합니다
(즉, 커밋하자마자 바로 이 명령어을 실행하는 경우)
2. Staging Area에 새로 올라온 내용이 있다면, 직전 커밋 내역에 같이 묶어서 재 커밋 됩니다






