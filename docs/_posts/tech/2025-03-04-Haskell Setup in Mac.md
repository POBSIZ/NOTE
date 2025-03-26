---
layout: post
title: Haskell Setup in Mac
categories:
  - tech
tags:
  - haskell
  - setup
datetime: 2025-03-07T00:39:00
---
# Haskell 세팅 완전 정복 in Mac

## 작업 환경

- **OS**: macOS 14.2 23C64 arm64
- **Host**: Mac14,2
- **CPU**: Apple M2
- **GPU**: Apple M2
- **Memory**: 16384MiB

## 1. GHCup (Glassgow-Haskell-Compiler-up) 설치

GHCup은 GHC, Cabal, Stack 및 HLS(Haskell-Language-Server)를 쉽게 관리할 수 있도록 도와주는 도구이다.

**GHC 설치 명령어**

```shell
> curl --proto '=https' --tlsv1.2 -sSf https://get-ghcup.haskell.org | sh

Welcome to Haskell!

This script can download and install the following binaries:
  * ghcup - The Haskell toolchain installer
  * ghc   - The Glasgow Haskell Compiler
  * cabal - The Cabal build tool for managing Haskell software
  * stack - A cross-platform program for developing Haskell projects (similar to cabal)
  * hls   - (optional) A language server for developers to integrate with their editor/IDE

ghcup installs only into the following directory,
which can be removed anytime:
  /Users/[username]/.ghcup

Press ENTER to proceed or ctrl-c to abort.
Note that this script can be re-run at any given time.

#Enter
-------------------------------------------------------------------------------

GHCup provides different binary distribution "channels". These are collections of tools
and may differ in purpose and philosophy. First, we select the base channel.

[S] Skip  [D] Default (GHCup maintained)  [V] Vanilla (Upstream maintained)  [?] Help (default is "Skip").

# D 입력 후 Enter
-------------------------------------------------------------------------------

Do you also want to enable the pre-releases channel, getting acces to.
alpha, betas and release candidates?

[N] No  [Y] Yes  [?] Help (default is "N").

# Enter (기본 값 "N" 사용)
-------------------------------------------------------------------------------

Do you also want to enable the cross channel, getting acces to
experimental GHCJS, WASM, etc.?

[N] No  [Y] Yes  [?] Help (default is "N").

# Enter (기본 값 "N" 사용)
-------------------------------------------------------------------------------

Detected zsh shell on your system...
Do you want ghcup to automatically add the required PATH variable to "/Users/[유저명]/.zshrc"?

[P] Yes, prepend  [A] Yes, append  [N] No  [?] Help (default is "P").

# zsh 사용 시 위와 같이 뜸 (기본 값 "P" 사용)
-------------------------------------------------------------------------------

Do you want to install haskell-language-server (HLS)?
HLS is a language-server that provides IDE-like functionality
and can integrate with different editors, such as Vim, Emacs, VS Code, Atom, ...
Also see https://haskell-language-server.readthedocs.io/en/stable/

[Y] Yes  [N] No  [?] Help (default is "N").

# Y 입력 후 Enter
-------------------------------------------------------------------------------

Do you want to enable better integration of stack with GHCup?
This means that stack won't install its own GHC versions, but uses GHCup's.
For more information see:
  https://docs.haskellstack.org/en/stable/configure/customisation_scripts/#ghc-installation-customisation
If you want to keep stacks vanilla behavior, answer 'No'.

[Y] Yes  [N] No  [?] Help (default is "Y").

# Enter (기본 값 "Y" 사용)
# 향상된 Stack 라이브러리 관리 프로그램 설치 여부
-------------------------------------------------------------------------------

System requirements 
  Note: On OS X, in the course of running ghcup you will be given a dialog box to install the command line tools. Accept and the requirements will be installed for you. You will then need to run the command again.
On Darwin M1 you might also need a working llvm installed (e.g. via brew) and have the toolchain exposed in PATH.
Press ENTER to proceed or ctrl-c to abort.
Installation may take a while.

# OS X 환경의 경우 위와 같은 문구가 뜰 수 있음
# Xcode CLI 를 설치하는 것이므로 Enter 하여 설치
# 시간이 조금 걸릴 수 있음
# Xcode CLI 를 설치하는 이유는 ghcup(Haskell GHC 설치/관리 도구)을 실행할 때, Haskell 관련 패키지를 빌드하거나 설정하는 과정에서 C/C++ 컴파일러 같은 기본 도구가 필요하기 때문

===============================================================================

OK! /Users/pobsiz/.zshrc has been modified. Restart your terminal for the changes to take effect,
or type ". /Users/[유저명]/.ghcup/env" to apply them in your current terminal session.

===============================================================================

All done!

To start a simple repl, run:
  ghci

To start a new haskell project in the current directory, run:
  cabal init --interactive

To install other GHC versions and tools, run:
  ghcup tui

If you are new to Haskell, check out https://www.haskell.org/ghcup/steps/

# 설치가 모두 완료되었다.
# ". /Users/[유저명]/.ghcup/env" 해당 부분의 명령어를 본인의 터미널에서 복사하여 터미널에 바로 입력하면 위 명령어들을 바로 사용가능하다.
# 위 명령어들을 실행해보며 제대로 설치되었는지 확인 해보면 좋다.
# ghci 환경에 들어갔을 때 ":q" 를 입력하면 벗어날 수 있다.
```

## 2. VSCode 설정

IDE는 Visual Studio Code 사용을 추천한다.
대강 Haskell 사용자들의 IDE 사용 현황을 보니 emacs, vim, nvim, intelliJ 등이 있는것 같은데

emacs, vim, nvim 얘네들은 쓰던 사람들은 편하게 쓸 수 있지만 처음 쓰는 사람들은 진입 장벽이 있을 것 같기에 비추천 한다.

intelliJ 에서는 plugin을 개인이 만든게 있는것 같은데 현재(25.03.05) github에서 archive 처리 된걸 보아하니 업데이트가 안되고 있는 것 같다...

VSCode의 Haskell Extension은 업데이트도 꾸준히 되고 있고 (현재 기준 25.03.01 가장 최근 업데이트) 설정이 편리해서 추천한다.

사실 중요 기능은 Extension이 아닌 HLS(Haskell Language Server)에서 제공 하는것이므로 HLS를 지원하는 IDE라면 모두 사용 가능하다.

## HLS (Haskell-Language-Server) 확인

우선 내가 사용하는 GHC의 버전을 확인해야 한다.
버전 확인 명령어는 아래와 같다.

```shell
> ghc --version

The Glorious Glasgow Haskell Compilation System, version 9.10.1
```

버전 확인 결과 9.10.1을 사용 중인것을 확인 할 수 있다.
HLS가 9.10.1 버전에 대응 되는게 있는지 확인하는 방법은 아래와 같다.

```shell
# haskell-language-server-[GHC 버전] --probe-tools
> haskell-language-server-9.10.1 --probe-tools

haskell-language-server version: 2.9.0.1 (GHC: 9.10.1) (PATH: /Users/[username]/.ghcup/hls/2.9.0.1/lib/haskell-language-server-2.9.0.1/bin/haskell-language-server-9.10.1)
Tool versions found on the $PATH
cabal:          3.12.1.0
stack:          3.3.1
ghc:            9.10.1
```

위와 같이 나온다면 HLS도 잘 설치 되어 있는것이다.
만약 GHC 버전과 HLS의 버전이 다르다면 GHC의 버전을 HLS의 버전에 맞추면 된다.
아마 그럴 일은 없을 것이지만 GHC의 버전을 수정하는 명령어는 아래와 같다.

```shell
# ghcup set ghc [버전]
> ghcup set ghc 9.10.1
```

## Extension 설치

VSCode Extension Tab에 들어가서 "Haskell" 검색 후 Haskell에서 배포한 공식 Extension을 설치하면 된다.

## VSCode Extension 설정

Command + Shift + P 를 입력하여 명령어 팔레트를 연 후
"Preferences: Open User Settings (JSON)" 라고 입력 후 Enter
설정 JSON 파일이 열리면 JSON 내부에 아래 내용을 붙여넣으면 된다.

```json
"haskell.serverExecutablePath": "/Users/[유저명]/.ghcup/bin/haskell-language-server-wrapper"
```

```js
// JSON
{
  // ...
  // ! Haskell 설정
  "haskell.serverExecutablePath": "/Users/[username]/.ghcup/bin/haskell-language-server-wrapper",
  "haskell.plugin.semanticTokens.globalOn": true,
  "editor.semanticTokenColorCustomizations": {
    "enabled": true
  }
}
```

위 설정을 입력하고 저장을 한 뒤 다시 명령 팔레트를 열어 (Command + Shift + P) 아래와 같이 입력 한 후 Enter (HLS 재시작)

```plaintext
Haskell: Restart Haskell LSP server
```

이제 ".hs" 확장자 파일을 만든 뒤 즐겁게 Haskell 을 사용하면 된다!