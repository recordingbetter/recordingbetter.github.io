---
title: TDD - Test Driven Development
slug: TDD - Test Driven Development
layout: post
categories: Python
---


- 개발시, 테스트를 먼저 만들고 그 테스트에 맞게 개발을 진행하는 방법

1. 테스트를 추가
2. 모든 테스트를 실행하고 새로 추가한 것이 실패하는지 확인
3. 코드를 수정
4. 모든 테스트가 성공하는지 확인
5. 코드에서 중복된 내용을 제거

## 순서

1. requirement 파악 : 간단한 요구사항을 적어본다.
2. 요구사항을 만족한다는 test 코드 작성
3. 테스트 실행
4. 코드 작성 (스텁 : 가짜코드)
5. 테스트 실행
6. 코드 수정
7. 테스트 실행
8. 테스트가 통과할때까지 반복

