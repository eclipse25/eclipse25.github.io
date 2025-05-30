---
layout: post
title: "Dart Introduction"
categories: [Dart · Flutter]
tags: [Flutter, Dart]
---

# Dart!

<img src="/assets/img/dart.png" alt="dart" width="500"/>

## Dart는 무엇이고 왜 써야할까?

- Dart는 **Flutter**에서 주로 사용되는 프로그래밍 언어이다.
  - Flutter는 모바일, 데스크탑 등 다양한 플랫폼에서 빠르게 애플리케이션을 개발하기 위한 프레임워크로, Dart 언어가 그 기반이 된다.
- Dart는 클라이언트 사이드 최적화를 목표로 하는 언어이다.
- 모든 플랫폼에서 빠르고 효율적인 애플리케이션 개발을 가능하게 한다.

## Dart의 주요 특징

1. **컴파일러**
   - Dart는 두 가지 주요 컴파일러를 가지고 있다.
     - **Dart Web**: Dart 코드를 JavaScript로 변환하는데 웹 애플리케이션 개발에 유용하다.
     - **Dart Native**: Dart 코드를 다양한 CPU 아키텍처(ARM32, ARM64, x86_64)에 맞게 기계어로 변환한다. 네이티브 애플리케이션 개발에 중요하다.
2. **JIT와 AOT 컴파일**
   - **JIT (Just-in-time) 컴파일**: 개발 과정 중 코드의 결과를 바로 화면에 보여주며, Dart VM을 사용한다. 빠른 개발과 테스트에 유리하다.
   - **AOT (Ahead-of-time) 컴파일**: 개발 완료 후 실제 기계어로 코드를 변환하여 배포한다. 이는 최종 애플리케이션의 성능 향상에 도움이 된다.

### Dart의 장점

- **Null Safety**: 개발자가 실수로 null을 참조하는 것을 방지하여 안전한 코드 작성을 도와준다.
- **JIT와 AOT 컴파일의 혼합 사용 가능**: 개발 중에는 JIT 컴파일을 통해 빠른 피드백을 받을 수 있고, 최종 앱을 컴파일할 때는 AOT 컴파일을 통해 성능을 최적화할 수 있다.
- **Google의 지원**: Dart와 Flutter 모두 구글에서 개발되었다. Dart 언어가 Flutter에 최적화되도록 지속적으로 발전할 수 있다는 것을 의미하는데, Flutter를 위해 Dart 언어 자체가 수정되어 Flutter의 성능이 향상될 수 있다.
