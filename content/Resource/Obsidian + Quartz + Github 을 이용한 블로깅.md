---
title: Obsidian + Quartz + Github 을 이용한 블로깅
draft: false
tags:
  - obsidian
  - quartz
---
# Intro

- 지난 몇 년간 개인 블로그를 만드려는 시도를 몇 번이나 하였으나 제대로 사용하지 못하였다. 그 원인을 꼽아 보자면,

	1. 개인적인 노트 공간과 블로그를 위한 공간이 합쳐져있지 않아 블로깅을 위한 글을 별도로 작성해주어야하는 번거로움이 존재
	2. 네이버 블로그, 티스토리는 사용하긴 싫고 github page는 commit, push 절차가 꽤나 귀찮음
- 사실 익숙하지 않은게 가장 큰 문제인데, 최근 obsidian을 사용하면서 개인적인 노트를 관리하면서도 블로그까지 한 방에 관리 할 수 있는 체계를 만들 수 있을 듯 하여 시도해보았다


# 설계

### Requirements
- 관리툴: Obsidian
- 데이터 싱크: Obsidian Sync
- 원격저장소: Github
- 동적사이트 생성기: Quartz


- 아래의 유튜브 영상을 많이 참고하였다
	- [YouTube: How to publish your notes for free with Quartz](https://www.youtube.com/watch?v=6s6DT1yN4dw)



# 세팅법
## Quartz 설치

- [설치 Docs](https://quartz.jzhao.xyz/)
- 아래 명령어를 통해서 Quartz 를 설치한다

```bash
git clone https://github.com/jackyzha0/quartz.git
cd quartz
npm i
npx quartz create
```

## Github Repo 세팅

- [세팅 Docs](https://quartz.jzhao.xyz/setting-up-your-GitHub-repository)
- github repo를 새로 생성한다. 다만, `.gitignore` 와 `license` 는 모두 None으로 설정함
- 아래의 명령어로 원격-로컬 저장소를 연결한다

```bash
# 위에서 클론받은 quartz 폴더 내에서 명령어를 실행해야 함
# list all the repositories that are tracked
git remote -v
 
# if the origin doesn't match your own repository, set your repository as the origin
git remote set-url origin REMOTE-URL
 
# if you don't have upstream as a remote, add it so updates work
git remote add upstream https://github.com/jackyzha0/quartz.git

npx quartz sync --no-pull
```

- 위의 명령어가 성공적으로 수행되었으면, 원격 저장소에 Quartz 폴더 내의 파일들이 push되어있는 것을 확인 할 수 있음


## Github에 Sync하기
- Quartz로 생성한 폴더 내 content 폴더 하위에 콘텐츠를 생성한다
- 그리고 원격저장소에 싱크하기 위해 아래의 명령어를 사용한다

```bash
npx quartz sync
```

- 참고로, 나같은 경우 블로그를 위한 Vault를 별도로 구분하고 싶지 않아 remote 연결이 된 quartz 폴더를 obsidian vault 내로 이동시켜 사용 중이다

## Github Page로 호스팅하기

- [호스팅 Docs](https://quartz.jzhao.xyz/hosting)
- 아래의 명령어로 로컬환경에서 빌드가 가능하고 `http://localhost:8080/` 으로 프리뷰를 할 수 있다
```bash
npx quartz build --serve
```


- 이제 github page 호스팅만 해주면 되는데 아래의 github action yml 문을 quartz 폴더 내의 .github/workflows 하위에 복사해주고 `npx quartz sync` 명령어를 이용해 배포만 해주면 완료
- 결과적으로 지금 보고 있는 이러한 홈페이지를 만들 수 있다



 
