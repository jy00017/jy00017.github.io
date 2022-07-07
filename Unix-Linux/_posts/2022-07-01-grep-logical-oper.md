# grep 명령에서 AND, OR, NOT 조건 사용

## grep 명령어
텍스트 검색 명령어

## AND 조건
### 파이프 라인을 2개 사용하는 방법
```
$ cat test_file | grep pattern1 | grep pattern2
```
### E 옵션 사용 방법
```
cat test_file | grep -E 'pattern1.*pattern2'
```

## OR 조건

## NOT 조건