---
title: "batch 인수에서 \"=\"(equal) 표시 보존하는 방법"
date: 2022-07-10
categories: ['unclassified label']
tags: ['batch']
---

# 목적
batch 파일에 인자 전달 시, **=** 기호를 유지하고자 함

## 테스트 케이스
e.g., 호출
**test.bat /name="hankey" /age="18"**

## 예상
```
args1: name="hankey"
args2: /age="18"
```
## 실제
```
args1: /name
args2: hankey
```

# 원인
batch 파일에서는 등호(=), 세미클론(;), 콤마(,), 스페이스와 탭까지 구분 문자열로 사용

# 우회방법
## 필수
**인수를 전달 시, 전체 범위에 대해서 ""(쌍따옴표)로 감싸준다**

e.g., test.bat "/name="hankey"" "/age="18""

### 결과
```
args1: "/name="hankey""
args2: "/age="18""
```
## 옵션
인자를 감싸고 있는 쌍다옴표를 제거하는 방법
* 인자를 받는 배치파일에 ~를 추가함

c.g.,
```
@echo off

echo args1: %1
echo args2: %2
```
# 참고
[Preserving "=" (equal) characters in batch file parameters(참고날짜:2023.02.08)](https://stackoverflow.com/questions/20572424/preserving-equal-characters-in-batch-file-parameters)

