---
title: Write-Output VS Write-Host
date: 2022-08-13
categories: ['PowerShell']
tags: ['PowerShell', "Write-Outputr 공백(NewLine) 제거"]
---

# 환경
* OS: Windows 10
* PSVersion(Powershell Version): 5.1.19041.1645

# 목적
* Write-Output을 이용하여 파일에 글을 작성하는데 NewLine이 삽입되는것을 피하기 위해서 조사
* Write-Host에는 -NoNewLine이란 옵션이 존재하지만 PipeLine 입력값을 사용하지 못하기 때문에 파일에 쓸수 없엇음
* Write-Output에는 -NoNewLine이란 **옵션 없음**

# 공통점
* 결과를 Console 화면에 보여줄 때 사용할 수 있다

# 차이점

|    | Write-Output | Write-Host |
|----|--------------|------------|
|PipeLine입력값 사용|가능|불가능|
|custom 컬러 설정 가능 여부|불가능|텍스토와 배경색 지정 가능|
|특징| |디스플레이 전용 출력|

# Write-Output의 공백(NewLine)을 제거하는 방법
## out-string과 trim이용
**Object를 string으로 변환 후 trim을 통해 공백 제거**

1) 비교

[AS-IS]
![ncluding_New_Line](/PowerShell/resource/Including_New_Line.png)

[TO-BE]
![Removing_New_Line](/PowerShell/resource/Removing_New_Line.png)

2) 코드
```
(Get-Service | Where-Object { ($_.Status -eq "Running")
 -and ($_.DisplayName -match 'windows') } | Out-String).Trim()
```

# Write-Host로 공백없는 파일 생성 또는 초기화 가능\
1) 코드 및 주석
```
# 빈 값에 파일이 생성됨
# Write-Output "" > "test.txt" 시는 공백이지만 줄바꿈이 생김
Write-Host -NoNewline "" > "test.txt"

# 입력값을 지원하지 않기 떄문에 test.txt 파일에 "Hello World"에 내용이 작성되지 않음
Write-Host "Hello World" > "test.txt"
```

