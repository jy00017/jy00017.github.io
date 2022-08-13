---
title:  "명령에서 AND, OR, NOT 조건 적용"
date: 2022-07-10
categories: ['Unix-Linux']
tags: ['grep']
---

# grep 명령에서 AND, OR, NOT 조건 적용

## grep 명령어
텍스트 검색 명령어

## AND 조건
2가지 옵션이 존재

### 파이프 라인을 2개 사용하는 방법
**$ cat file_name | grep pattern1 | grep pattern2**

#### 예제
목적: hello와 !가 패턴이 모두 포함된 문자열 추출

커맨드:    
```
# 1. test_file 내용을 읽어드림
# 2. 대소문자 무시하고 hello 매치하는 문장 추출
# 3. 2번에서 추출된 내용 중 !가 들어간 내용을 표시

[root@MyLinux /]# cat test_file | grep -i hello | grep -i !
```
출력:
```
Hello World!
```

### E(정규 표현식) 옵션 사용 방법
**$ cat file_name | grep -E 'pattern1.\*pattern2'**

상세:
* -E 옵션: pattern을 확장 정규 표현(Extended Regex)으로 해석
* grep예서 사용하는 정규 표현식(더 존재 필요시 찾음 요망)

|메타문자열|설명|
|-----|--|
|.|임의의 문자1개|
|*|앞에 오는 문자의 개수가 0 ~ 무한

#### 예제
목적: hello와 !가 패턴이 모두 포함된 문자열 추출

커맨드:
```
# 1. test_file의 내용을 읽어드린다
# 2. Hello.*!: Hello로 시작해서 !로 끝나는 모든 문자 검색(Hello!도 검색함)
# (.*: 임의의 문자 0개또는 무한대 매치)
cat test_file | grep -E 'Hello.*!'
```
출력:
```
Hello World!
```

## OR 조건
2가지 옵션이 존재
### e 옵션 사용 방법
**$ cat file_name | grep -e pattern1 -e pattern2**

상세:
* -e 옵션: 매칭할 패턴, 한 번에 2개 이상의 특정 문자열로 검색할 때 사용

#### 예제
목적: !와 foo가 매칭된문자열 검색

커맨드:
```
# -e 옵션을 여러개 사용하여 검색(!포함, foo포함)
[root@MyLinux /]# cat test_file | grep -e ! -e foo
```
출력:
```
HelloWorld!
foo
```
### E(정규 표현식) 옵션 사용 방법
**$ cat file_name | grep -E 'pattern1|pattern2'**

상세: 
* -E 옵션: pattern을 확장 정규 표현(Extended Regex)으로 해석

#### 예제
목적: !와 foo가 매칭된문자열 검색

커맨드:
```
[root@MyLinux /]# cat test_file | grep -E 'foo|!'
```
출력:
```
HelloWorld!
foo
```

## NOT 조건
### v 옵션 사용 방법
**$ cat file_name | grep -v pattern1**

* -v 옵션: 패턴이 일치하는 문자열 제외(일치하지 않는 문자열만 표시)

#### 예제
* 목적: !가 제외된 문자열만 추출

```
# 1. test_file을 읽어들임
#2. !가 포함된 문자열 제외(\는 !에 대한 escape 문자)
[root@MyLinux /]# cat test_file | grep -v "\!"
```
출력
```
Hello
```
## 참고
[데이터 엔지니어링, [Linux] grep 명령어에서 AND, OR, NOT 조건 사용하기, (참고날짜:2022.07.10)](https://hbase.tistory.com/22)