# 수업 내용 정리
## clone & pull
- `git clone` 명령어를 사용하면 원격 저장소를 통째로 복제해서 내 컴퓨터에 옮길 수 있음.
- 원격 저장소의 변경 사항을 가져와서, 로컬 저장소를 업데이트하는 명령어 `git pull <저장소 이름> <브랜치 이름>`

## Branch 1
>나뭇가지처럼 여러 갈래로 작업 공간을 나누어 독립적으로 작업할 수 있도록 도와주는 Git의 도구

```bash
# 브랜치 목록 확인
$ git branch

# 원격 저장소의 브랜치 목록 확인
$ git branch -r

# 새로운 브랜치 생성
$ git branch <브랜치 이름>

# 특정 커밋 기준으로 브랜치 생성
$ git branch <브랜치 이름> <커밋 ID>

# 특정 브랜치 삭제
$ git branch -d <브랜치 이름> # 병합된 브랜치만 삭제 가능
$ git branch -D <브랜치 이름> # (주의) 강제 삭제 (병합되지 않은 브랜치도 삭제 가능)

# 브랜치 목록 확인
$ git branch

# 원격 저장소의 브랜치 목록 확인
$ git branch -r

# 새로운 브랜치 생성
$ git branch <브랜치 이름>

# 특정 커밋 기준으로 브랜치 생성
$ git branch <브랜치 이름> <커밋 ID>

# 특정 브랜치 삭제
$ git branch -d <브랜치 이름> # 병합된 브랜치만 삭제 가능
$ git branch -D <브랜치 이름> # (주의) 강제 삭제 (병합되지 않은 브랜치도 삭제 가능
```

## Branch 2(Merge)
```bash
# 1. 현재 branch1과 branch2가 있고, HEAD가 가리키는 곳은 branch1 입니다.
$ git branch
* branch1
  branch2

# 2. branch2를 branch1에 합치려면?
$ git merge branch2

# 3. branch1을 branch2에 합치려면?
$ git switch branch2
$ git merge branch1
```

## Workflow
1. 원격 저장소 소유권이 있는 경우 (Shared repository model)
>원격 저장소가 자신의 소유이거나 collaborator로 등록되어 있는 경우

``` bash
$ git clone 원격저장소url

$ git switch -c 브랜치 이름

$ git push origin 브랜치 이름

#  pr보낸 후 병합된 파일 다운

$ git pull origin master
 * 이 때 마스터 브랜치에서 해야 함!
```

2. 원격 저장소 소유권이 없는 경우 (Fork & Pull model)
> 자신의 소유가 아닌 원격 저장소인 경우

``` bash
- 원격 저장소에서 fork 후

$ git clone https://github.com/edukyle/kakao_clone.git

# 원본 원격 저장소에 대한 이름은 upstream으로 붙이는 것이 일종의 관례

$ git remote add upstream [url]

$ git switch -c [브랜치 이름]

$ git push origin [브랜치 이름]

- PR 보내고 병합되면

$ git pull upstream master
$ git branch -d [브랜치 이름]

```

