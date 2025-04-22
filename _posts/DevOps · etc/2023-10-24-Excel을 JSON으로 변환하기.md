---
layout: post
title: "엑셀(Excel)파일을 JSON으로 변환하기"
categories: [DevOps · etc]
tags: [Python]
---


> 2023년 학교에서 다른 사람들과 같이 하는 프로젝트라는 걸 처음 해봤을 때, 플러터에서 프론트엔드밖에 할 줄 몰랐는데, 그때는 이런것도 다 엄청 멋있어보였다. 그래서 백엔드 팀원들이 한번 해보라고 줬던 파일을 가지고 있다가 정리해뒀었다. 지금은 AI가 발전해서 이런건 GPT로 1분이면 할 수 있지만, 이런 것도 내 역사인것 같아서 남겨둔다.

## 엑셀(Excel)파일을 JSON으로 변환하기

1. (구글 스프레드 시트로 작업한 데이터베이스 파일을 엑셀로 내보내거나) 엑셀파일을 저장한다.

2. 다음 파일을 다운받는다.
   [ExceltoJson.py (0.01MB)](/assets/file/ExcelToJson.py)

   파일 내용이 300줄이 넘어가기 때문에 미리보기만 올리자면 다음과 같다.

   ```python
   import pandas as pd
   `import numpy as np
   import math
   import argparse
   parser = argparse.ArgumentParser(description="A simple program that converts xlsx files to json files.",
                                    epilog = '''
      # MODE 0 : opentime, closetime, breaktime are seperate values.
         [OPENTIME],[CLOSETIME],[BREAKSTART-BREAKEND]

      # MODE 1 : opentime, closetime, breaktime are in a list.
         [OPENTIME,CLOSETIME,BREAKSTART-BREAKEND]

      # MODE 2 : opentime, closetime, breaktime are in a list.
         [OPENTIME,CLOSETIME,[BREAKSTART,BREAKEND]]

      # MODE 3 : opentime, closetime, breaktime are in a list, breaktime is broken into two parts.
         [OPENTIME,CLOSETIME,BREAKSTART,BREAKEND]
      ''',
                                    formatter_class=argparse.RawTextHelpFormatter)

   NO_OF_TAGS = 17
   VERSION = 1.3
   ```

3. 이 파일과 엑셀파일을 같은 폴더에 위치시킨 후 이 위치에서 powershell을 연다.

   - 파이썬과 pandas가 설치되어 있어야 한다.
   - 판다스가 설치되어 있지 않다면 pip install pandas 명령어를 통해 설치한다.

4. `python ExcelToJson.py -f food_jason -o food_jason -v -m 3 -s FoodList_mk2 --drop-null` 명령어를 실행한다.

   - `ImportError: Missing optional dependency 'openpyxl'.` 오류가 생긴다면 `pip install openpyxl` 명령어로 설치한다.
   - 오류가 없다면 `python ExcelToJson.py -f food_jason -o food_jason -v -m 3 -s FoodList_mk2 --drop-null` 명령어를 실행했을 때 위치한 폴더에 json파일이 만들어진다.

5. 파이어베이스 storage에 업로드하면 끝난다.
   - (해당 포스트는 flutter-firebase 프로젝트를 진행하는 맥락에서 쓰여졌다.)
   - 이름이 같은 파일이 있을때 그냥 업로드 해도 자동으로 덮어씌워진다.
