---
layout: post
title: Haskell Tip
categories:
  - tech
tags:
  - haskell
  - tip
datetime: 2025-03-07T00:39:00
updated_at: 2025-03-27T02:32:00
---
# Haskell Tip 목록

## VSCode Stack Project HLS 무한 Processing 증상 해결 방법

VSCode 에서 Haskell Stack 프로젝트를 열 경우 HLS 가 정상 작동을 하지 않아 Formatter, Syntax Highlighter, Compiler 가 제대로 동작하지 않는 경우가 있다. 이럴 경우 대부분 Stack 프로젝트를 빌드 하지 않았을 경우 일 것이다. 프로젝트를 빌드 후 hls 를 재시작 해보면 정상 작동 할 것이다.

**Stack 프로젝트 빌드 명령어**

```shell
stack build
```

**VSCode HLS 재시작 방법**

Mac의 경우 Cmd + Shift + P
Window의 경우 Ctrl + Shift + P
를 눌러 커맨드 팔레트를 연 후 아래와 같이 입력하여 엔터를 입력하면 된다.

```shell
Haskell: Restart Haskell LSP server
```

