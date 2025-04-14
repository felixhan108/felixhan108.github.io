---
title: Shell 한번에 이해하기
version: 0.0.1
latestUpdate: 2025-04-14
description: 회사에선 window를 쓰고 집에서는 mac 을 쓰고 서버는 리눅스를 쓰다보니 내가 지금 어디에서 어떤 명령을 쓰고 있는지 헷갈릴 때가 많습니다. 여기가 지금 'PowerShell'인지 'bash' 인지 'zsh'인지 그리고 어떤 특징이 있는지 비교해 보았습니다.
---

# 🍔Shell 종류

## 🍟cmd

운영체제 배경 - `Windows`
주요 특징 - 전통적인 Windows 명령 셸 (MS-DOS계열)
주요 명령어 스타일 - `dir`,`echo`,`cd`,`copy`

## 🍟PowerShell

운영체제 배경 - `Windows` -> `macOS`,`Linux`(최근지원)
주요 특징 - 객체 기반 셸, .NET 통합
주요 명령어 스타일 - `$env:PATH`

## 🍟bash

운영체제 배경 - `Linux/Unix`
주요 특징 - 가장 널리 사용되는 셸
주요 명령어 스타일 - `ls`,`cd`,`echo`,`export`

## 🍟zsh

운영체제 배경 - `Linux/macOS`
주요 특징 - bash 기반 확장형 셸
주요 명령어 스타일 - bash와 거의 동일

## 🍟sh (Bourne Shell)

운영체제 배경 - `Unix`
주요 특징 - 아주 기본적인 셸 (표준 POSIX), 어디서나 돌아가는 최소 셸
주요 명령어 스타일 - `echo`,`cd`,`export`

# 🍔상황별 추천

| 상황                                   | 추천 셸             |
| -------------------------------------- | ------------------- |
| Windows에서 간단한 명령만 쓸 때        | `cmd`               |
| Windows에서 스크립트 자동화할 때       | `PowerShell`        |
| 리눅스 서버를 주로 다룰 때             | `bash`              |
| 터미널을 편하게, 세련되게 쓰고 싶을 때 | `zsh` + `Oh My Zsh` |
| POSIX 표준 스크립트가 필요할 때        | `sh`                |

# 🍔참고 명령어 비교

| 작업        | cmd       | PowerShell      | bash/zsh     |
| ----------- | --------- | --------------- | ------------ |
| 파일 리스트 | `dir`     | `Get-ChildItem` | `ls`         |
| 환경변수    | `set`     | `$env:PATH`     | `echo $PATH` |
| 현재 경로   | `cd`      | `Get-Location`  | `pwd`        |
| 파일 복사   | `copy`    | `Copy-Item`     | `cp`         |
| 변수 선언   | `set x=1` | `$x = 1`        | `x=1`        |
