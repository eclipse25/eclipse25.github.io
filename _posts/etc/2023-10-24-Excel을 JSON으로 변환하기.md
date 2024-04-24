---
layout: post
title: "[etc] 엑셀(Excel)파일을 JSON으로 변환하기"
categories: [etc]
tags: []
---

1. (구글 스프레드 시트로 작업한 데이터베이스 파일을 엑셀로 내보내거나) 엑셀파일을 저장한다.

2. 다음 파일을 다운받는다.(안전한 파일이지만 다른 곳에서 받아도 된다.)
   [ExceltoJson.py (0.01MB)](/assets/file/ExcelToJson.py)

3. 이 파일과 엑셀파일을 같은 폴더에 위치시킨 후 이 위치에서 powershell을 연다.

   - 파이썬과 pandas가 설치되어 있어야 한다.
   - 판다스가 설치되어 있지 않다면 pip install pandas 명령어를 통해 설치한다.

4. `python ExcelToJson.py -f food_jason -o food_jason -v -m 3 -s FoodList_mk2 --drop-null` 명령어를 실행한다.

   - `ImportError: Missing optional dependency 'openpyxl'.` 오류가 생긴다면 `pip install openpyxl` 명령어로 설치한다.
   - 오류가 없다면 `python ExcelToJson.py -f food_jason -o food_jason -v -m 3 -s FoodList_mk2 --drop-null` 명령어를 실행했을 때 위치한 폴더에 json파일이 만들어진다.

5. 파이어베이스 storage에 업로드하면 끝난다.
   - (해당 포스트는 flutter-firebase 프로젝트를 진행하는 맥락에서 쓰여졌다.)
   - 이름이 같은 파일이 있을때 그냥 업로드 해도 자동으로 덮어씌워진다.
