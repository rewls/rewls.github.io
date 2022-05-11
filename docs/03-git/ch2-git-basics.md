---
layout: default
title: Ch2 Git Basics
parent: Git
nav_order: 2
mermaid: true
permalink: /docs/git/ch2-git-basic
---

# Ch2 Git 기초
{: .no_toc }

> [참고](http://git-scm.com/book/ko/v2/Git%EC%9D%98-%EA%B8%B0%EC%B4%88-Git-%EC%A0%80%EC%9E%A5%EC%86%8C-%EB%A7%8C%EB%93%A4%EA%B8%B0s)

<details open markdown="block">
  <summary>
    Toggle
  </summary>

## Table of contents
{: .no_toc .text-delta }

- TOC
{:toc}
</details>

---

## 2.1 Git 저장소 만들기

주로 다음 두 가지 중 한 가지 방법으로 Git 저장소를 쓰기 시작한다.

1. 아직 버전관리를 하지 않는 로컬 디렉토리 하나를 선택해서 Git 저장소를 적용하는 방법

2. 다른 어딘가에서 Git 저장소를 Clone하는 방법

### 기존 디렉토리를 Git 저장소로 만들기

- Git으로 관리하고 싶은 프로젝트의 디렉토리로 이동한다.

```
git init
```

- 디렉토리의 하위에 `📁.git`을 만든다. `📁.git` 디렉토리에는 저장소에 필요한 뼈대 파일(Skeleton)이 들어 있다.

- Git이 파일을 관리하게 하려면 저장소에 파일을 추가하고 커밋해야 한다.

```
git add <file>
git commit -m "<commit message>"
```

### 기존 저장소를 Clone하기

```
git clone <url>
```

- 프로젝트 히스토리를 전부 받아온다.

- 저장소 이름으로 디렉토리를 만들고 그안에 `📁.git` 디렉토리를 만든다.

- 가장 최신 버전을 Checkout 해놓는다.

```
git clone <url> <name>
```

- 디렉토리 이름 지정

## 2.2 수정하고 저장소에 저장하기

- 워킹 디렉토리의 모든 파일은 크게 Tracked(관리대상)와 Untracked(관리대상 아님)으로 나눈다.

- Tracked 파일은 이미 스냅샷에 포함되어 있던 파일이다. Tracked 파일은 또 Unmodified(수정하지 않은) modified(수정한) 그리고 Staged(커밋으로 저장소에 기록할) 상태 중 하나이다.

- 나머지 파일은 모두 Untracked 파일이다.

- 처음 저장소를 Clone 하면 모든 파일은 Tracked이면서 Unmodified 상태이다.

- Modified 상태인 파일을 커밋하기 위해서는 수정한 파일을 Staged 상태로 만들고 Staged 상태의 파일을 커밋한다.

![lifecycle](./img/lifecycle.png)

### 파일의 상태 확인하기

```
git status
```

- 파일이 Tracked 되기 전까지 Git은 저대 그 파일을 커밋하지 않는다.

### 파일을 새로 추적하기

```
git add <file>
```

### Modified 상태의 파일을 Stage 하기

```
git add <file>
```

- 수정한 파일을 Staged 상태로 만든다.

### 파일 상태를 짤막하게 확인하기

```
git status -s
```

- 앞에 붙은 두 글자의 왼쪽에는 Staging Area에서의 상태를, 오른쪽에는 Working Tree에서의 상태를 표시한다.

- `??`: 아직 추적하지 않은 파일

- `A`: Staged 상태로 추가한 파일 중 새로 생성한 파일

- `M`: Staged 상태로 추가한 파일 중 수정한 파일

### 파일 무시하기

- 어떤 파일은 Git이 관리할 필요가 없다. 보통 로그 파일이나 빌드 시스템이 자동으로 생성한 파일이 그렇다.

- `📝.gitignore` 파일을 만들고 그 안에 무시할 파일 패턴을 적는다.

- `📝gitignore` 파일에 입력하는 패턴은 아래 규칙을 따른다.

	- 아무것도 없는 라인이나 `#`으로 시작하는 라인은 무시한다.

	- 표준 Glob 패턴을 사용한다. 이는 프로젝트 전체에 적용된다.

	- 슬래시(`/`)로 시작하면 하위 디렉토리에 적용되지(Recursivity) 않는다.

	- 느낌표(`!`)로 시작하는 패턴의 파일은 무시하지 않는다.

- Glob 패턴

	- 정규표현식을 단순하게 만든 것

	- 애스터리스크(`*`)는 문자가 하나도 없거나 하나 이상을 의미

	- 대괄호(`[]`)는 대괄호 안에 있는 문자 중 하나를 의미

	- 물음표(`?`)는 문자 하나를 의미

	- 대괄호 안의 캐릭터 사이 하이픈(`-`)을 사용하면 그 캐릭터 사이에 있는 문자 하나를 의미

	- 애스터리스크 2개를 사용하여 디렉토리 안의 디렉토리까지 지정할 수 있다.
		- `a/**/z` 패턴은 `a/z`, `a/b/z`, `a/b/c/z` 디렉토리에 사용할 수 있다.

##### 예

```
# 확장자가 .o나 .a인 파일 무시
*.[oa]

# ~로 끝나는 모든 파일 무시
*~

# 확장자가 .a인 파일 무시
*.a

# 윗 라인에서 확장자가 .a인 파일은 무시하게 했지만 lib.a는 무시하지 않음
!lib.a

# 현재 디렉토리에 있는 TODO파일은 무시하고 subdir/TODO처럼 하위디렉토리에 있는 파일은 무시하지 않음
/TODO

# build/ 디렉토리에 있는 모든 파일은 무시
build/

# doc/notes.txt 파일은 무시하고 doc/server/arch.txt 파일은 무시하지 않음
doc/*.txt

# doc 디렉토리 아래의 모든 .pdf 파일을 무시
doc/**/*.pdf
```

> 힌트
>
> Github은 다양한 프로젝트에서 자주 사용하는 `📝.gitignore` 예제를 관리하고 있다.
>
> [gitignore](https://github.com/github/gitignore)

> 노트
>
> `📝.gitignore` 파일이 위치한 디렉토리와 그 하위 디렉토리에 적용된다.
>
> 여러 개의 `.📝gitignore` 파일을 둘 수 있다.

### Staged와 Unstaged 상태의 변경 내용을 보기

```
git diff
```

- 워킹 디렉토리에 있는 것과 Staging Area에 있는 것을 비교

```
git diff <--staged or --cached>
```

- 저장소에 커밋한 것과 Staging Area에 있는 것을 비교

- `git diff` 명령은 마지막으로 커밋한 후에 수정한 것들 전부를 보여주지 않는다.

> 노트
>
> 외부 도구로 비교하기
>
> `git difftool`을 사용해서 Diff 도구로 비교할 수 있다.

### 변경사항 커밋하기

```
git commit
```

- 자동으로 생성되는 커밋 메시지의 첫 라인은 비어 있고 둘째 라인부터 `git status` 명령의 결과가 채워진다.

- `-v` 옵션을 추가하면 편집기에 diff 메시지도 추가된다.

- 내용을 저장하고 편집기를 종료하면 Git은 입력된 내용(#로 시작하는 내용을 제외한)으로 새 커밋을 만든다.

- `-m` 옵션을 사용하면 메시지를 인라인으로 첨부할 수도 있다.

### Staging Area 생략하기

- `git commit`에 `-a` 옵션을 추가하면 Git은 Tracked 상태의 파일을 자동으로 Staging Area에 넣는다.

### 파일 삭제하기

```
git rm
```

- Git에서 파일을 제거하려면 Staging Area에서 삭제한 후에 커밋해야 한다.

```
git rm
```

- Staging Area에서 뿐만 아니라 워킹 디렉토리에서도 파일도 삭제한다.

- 커밋하면 파일은 삭제되고 Git은 이 파일을 더는 추적하지 않는다.

- 이미 파일을 수정했거나 Staging Area에 추가했다면 `-f` 옵션을 주어 강제로 삭제해야 한다.

- `--cached` 옵션을 사용하면 Staging Area에서만 제거하고 워킹 디렉토리에 있는 파일을 지우지 않고 남겨둘 수 있다.

- file-glob 패턴을 사용하여 여러 개의 파일이나 디렉토리를 한꺼번에 삭제할 수도 있다.

	- `*`앞에 `\`을 사용한다. 파일명 확장 기능은 쉘에만 있는 것이 아니라 Git자체에도 있기 때문에 필요하다.

### 파일 이름 변경하기

```
git mv <file_from> <file_to>
```

- 아래의 명령어를 수행한 것과 똑같다.

```
mv <file_from> <file_to>
git rm <file_from>
git add <file_to>
```

## 2.3 커밋 히스토리 조회하기

```
git log
```

- 저장소의 커밋 히스토리를 시간순으로 보여준다.

- 각 커밋의 SHA-1 checksum, 저자 이름, 저자 이메일, 커밋한 날짜, 커밋 메시지를 보여준다.

### `git log` 주요 옵션

| 옵션              | 설명                                                                                                                                              |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| `-p`              | 각 커밋에 적용된 패치를 보여준다.(커밋의 diff 결과를 보여준다.)                                                                                   |
| `--stat`          | 각 커밋에서 수정된 파일의 통계정보를 보여준다.                                                                                                    |
| `--shortstat`     | `--stat` 옵션 명령의 결과 중에서 수정한 파일, 추가된 라인, 삭제된 라인만 보여준다.                                                               |
| `--name-only`     | 커밋 정보 중에서 수정된 파일의 목록만 보여준다.                                                                                                   |
| `--name-status`   | 수정된 파일의 목록을 보여줄 뿐만 아니라 파일을 추가한 것인지 수정한 것인지, 삭제한 것인지도 보여준다.                                             |
| `--abbrev-commit` | 40자 SHA-1 checksum의 처음 몇 자만 보여준다.                                                                                                      |
| `--relative-date` | 상대적인 시간을 보여준다.                                                                                                                         |
| `--graph`         | 브랜치와 머지 히스토리를 보여주는 아스키 그래프로 보여준다.                                                                                       |
| `--pretty`        | 히스토리 내용을 보여줄 때 형식을 선택할 수 있다.                                                                                                  |
| `--pretty`        | 지정한 형식으로 히스토리를 보여준다. `oneline`, `short`, `full`, `fuller`, `format`이 있다. `format`은 원하는 형식으로 출력하고자 할 때 사용한다. |
| `--online`        | `--pretty=oneline --abbrev-commit`을 사용한 것과 같다.                                                                                            |

```
git config --global alias.l log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%ci) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative --all
```

##### `git log --pretty=format` 유용한 옵션

| 옵션  | 설명                               |
|-------|------------------------------------|
| `%H`  | 커밋 해시                          |
| `%h`  | 짧은 길이 커밋 해시                |
| `%T`  | 트리 해시                          |
| `%t`  | 짧은 길이 트리 해시                |
| `%P`  | 부모 해시                          |
| `%p`  | 짧은 길이 부모 해시                |
| `%an` | 저자 이름                          |
| `%ae` | 저자 메일                          |
| `%ad` | 저자 시각(형식은 --date=옵션 참고) |
| `%ar` | 저자 상대적 시각                   |
| `%cn` | 저자 상대적 시각                   |
| `%cn` | 커미터 메일                        |
| `%cd` | 커미터 시각                        |
| `%cr` | 커미터 상대적 시각                 |
| `%s`  | 요약                               |

- 저자(Author)는 원래 작업을 수행한 원작자이고 커미터(Committer)는 마지막으로 이 작업을 적용한(저장소에 포함시킨) 사람이다.

### 조회 제한조건

##### `git log` 조회 범위를 제한하는 옵션

|옵션|설명|
|-|-|
|`-(n)`|최근 n개의 커밋만 조회한다.|
|`--since`, `--after`|명시한 날짜 이후의 커밋만 조회한다.|
|`--util`, `--before`|명시한 날짜 이전의 커밋만 조회한다.|
|`--author`|입력한 저자의 커밋만 보여준다.|
|`--committer`|입력한 커미터의 커밋만 보여준다.|
|`--grep`|커밋 메시지 안의 텍스트를 검색한다.|
|`-S`|커밋 변경(추가/삭제) 내용 안의 텍스트를 검색한다.|

```
git log --since=2.weeks
```

- 다양한 형식을 지원한다. "2022-03-27", "2 tears 1 day 3 minutes ago"와 같이 사용할 수 있다.

> 노트
>
> `--author`와 `--grep` 옵션을 함께 사용하여 모두 만족하는 커밋을 찾으려면 `--all-match` 옵션도 반드시 함께 사용해야 한다.

```
git log -- path1 path2
```

- 파일 경로로 검색

- 명령어 끝 부분엥 쓴다.
