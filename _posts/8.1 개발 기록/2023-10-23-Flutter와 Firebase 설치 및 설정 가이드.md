---
layout: post
title: "[Flutter] Flutter와 Firebase 설치 · 환경설정"
categories: [8.1 개발 기록]
tags: [Flutter, Dart, Firebase]
---

<img src="/assets/img/flutterfirebase.png" alt="dart" width="500"/>

## 0. Chocolatey 설치

- Flutter를 설치하기 위해 필요하다.
- PowerShell을 관리자 권한으로 실행한다.
- `Get-ExecutionPolicy` 명령어를 입력한다.
  - `Restricted`가 반환될 경우 `Set-ExecutionPolicy AllSigned` 또는 `Set-ExecutionPolicy Bypass -Scope Process` 명령어를 입력한다.
  - `Bypass`가 반환될 경우 다음 단계로 진행한다.
- 아래 명령줄을 입력하여 Chocolatey를 설치한다.
  ` Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))`
- 설치 후 `choco` 명령어 입력으로 잘 설치되었는지 확인한다.

## 1. Flutter 설치

- 관리자 권한으로 연 PowerShell에 `choco install flutter`를 입력한다.
- 설치 후 `flutter` 명령어 입력으로 잘 설치되었는지 확인한다.

## 2. 안드로이드 스튜디오 설치

- JAVA 8 이상이 필요하므로 설치가 안되어있다면 설치하고 환경 변수를 설정한다.
- [Flutter 공식 문서](https://docs.flutter.dev/get-started/install/windows#android-setup)를 따라서 안드로이드 스튜디오를 설치한다.
- 안드로이드 스튜디오 메인화면 하단 'More Actions'에서 'SDK Manager'로 들어가 'SDK Tools' 탭에서 'Android SDK Command-line Tools (latest)'를 설치한다.
- 'Device Manager'를 찾아 기기를 생성하고 설정한다. (프로젝트가 이미 생성된 경우 설정이 자동으로 진행될 수 있다. 기본 모델: Pixel 3a API, 릴리스 버전: ABI x86_64 설정을 추천한다.)
- 설치와 설정이 완료되면 `flutter doctor --android-licenses` 명령어를 실행한다.

## 3. 설치 점검

- IDE 콘솔이나 PowerShell에서 `flutter doctor` 입력하여 설치 상태를 점검한다.
  - dart를 먼저 설치했다면 dart 삭제하고 flutter를 설치한다.
- 문제 발생 시 다음 단계를 따른다:
  - `Android sdkmanager not found. Update to the latest Android SDK and ensure that the cmdline-tools are installed to resolve this.`: 안드로이드 스튜디오에서 SDK Manager를 실행,
    좌측의 System Settings 에서 Android SDK를 선택, SDK Tools를 선택, Hide Obsolete Packages 체크 해제
  - `Unable to find bundled Java version`: 안드로이드 스튜디오 설치 위치(C:\Program Files\Android\Android Studio일 확률이 높음)의 `jbr` 폴더 내용을 `jre` 폴더에 복사한다.
  - `Windows 10 SDK` 가 없다고 뜨는 경우: [Visual Studio 2022](https://visualstudio.microsoft.com/ko/downloads/) 해당 사이트에서 Visual Studio 2022 무료 다운로드를 설치, 데스크톱 및 모바일에서 C++를 이용한 데스크톱 개발을 선택 후 설치한다.
  - `Unable to confirm if installed Windows version is 10 or greater`: `flutter channel master` 명령어로 채널 변경 후 `flutter upgrade`로 업그레이드한다.
  - `Unable to find git in your PATH`: 관리자 권한 cmd에서 `git config --global --add safe.directory '*'` 입력한다.
- flutter doctor 입력 시 No issues found!이면 완료된다.
- Powershell 종료 후 다시 해보면 될 수도 있다.

## 4. VSCode 설정

- 프로젝트 생성: 콘솔에 `flutter create [프로젝트 이름]`을 입력한다.
- VSCode 확장 기능 설치: vscode extension에서 Dart extension, Flutter extension을 설치한다.
- 오른쪽 하단 {} Dart에 마우스를 올려놓고, (hover) Dart DevTools 누른다. device에서 안드로이드 에뮬레이터 선택한다.
- 코딩할 때 (const로 인한) 파란줄 없애기: 왼쪽하단 톱니바퀴, Command Palatte 열기 → `open user settings`입력, `settings.json`파일 열기 → `"editor.codeActionsOnSave": { "source.fixAll": true }`을 파일 안에 입력한다. (const를 자동으로 붙여주는 기능이지만 const가 붙은 후 코드를 고쳤을 때 자동으로 떼어 주지는 않기 때문에 const를 지워주지 않으면 에러가 날 수 있음)

## 5. Firebase 연결

- [Firebase CLI 설치 가이드](https://firebase.google.com/docs/cli?hl=ko#install-cli-windows)를 따라 Firebase CLI를 설치한다.
  - 독립실행형 바이너리 말고 (독립실행형 바이너리의 경우 설치가 제대로 진행되지 않을 확률이 높다.) node.js를 사용하는 npm 버전을 다운로드한다.
  - node.js가 설치되어 있지 않다면 시키는대로 먼저 설치한다. 그러나 앞에서 choco잘 설치 했다면 추가로 설치를 선택하지 말 것 (멀쩡한 flutter가 돌아가지 않아서 choco를 다시 설치해야 할 수 있다.)
- 프로젝트 디렉터리에서 `npm install -g firebase-tools`명령어를 입력하면 CLI 설치가 끝난다.
- `firebase login:ci` 또는 `firebase login`으로 파이어베이스 계정을 연결한다.
  - 물론 firebase 회원가입부터 해야 한다.
- `firebase init`을 실행한다.
- [Flutter에 Firebase 설정하기](https://firebase.google.com 링크를 참조해서 마무리한다.

> dart pub global activate flutterfire_cli<br>
> flutterfire configure<br>
> flutter pub add firebase_core<br>
> flutterfire configure<br>
