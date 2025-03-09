---
layout: post
title: Tail Recursion (꼬리 재귀)
categories:
  - tech
tags:
  - recursion
  - 재귀
  - 재귀함수
datetime: 2025-03-02T00:39:00
---
# Tail Recursion == 꼬리 재귀
꼬리 재귀를 알기 위해선 꼬리 호출 (Tail Call) 에 대하여 알아야 한다.

### Tail Call == 꼬리 호출
꼬리 호출은 함수의 마지막 동작으로 함수를 호출하고 즉시 반환하는 함수 호출 방식이다.
아래 꼬리 호출이 존재하지 않는 그리고 존재하는 함수를 순서대로 정의 해보겠다.

**꼬리 호출이 존재하지 않는 함수**
```typescript
'use strict'
function foo(n: number): number {
  if(n <= 0) return 1;

  // 호출된 함수에 추가적인 동작이 존재
  const result = foo(n - 1) - 1;

  return result;
}
```

**꼬리 호출이 존재하는 함수**
```typescript
'use strict'
function foo(n: number): number {
  if(n <= 0) return 1;

  // 호출된 함수를 즉시 반환 함
  return foo(n - 1);
}
```

### Tail Call Optimization == 꼬리 호출 최적화

함수를 즉시 반환하지 않고 추가적인 동작이 있다면 호출된 함수를 결과가 반환되기 전까지 계속해서 참조하고 있어야 하므로 함수 call stack에 stack frame이 계속해서 유지되어야 한다.
이로 인해 재귀 함수의 경우 call stack에 stack frame이 지속적으로 쌓이게 되고 stack overflow가 발생 할 수 있게되며 불필요한 메모리 낭비가 생길 수 있다.

하지만 함수를 즉시 반환하게 된다면 호출된 함수의 frame을 참조 할 필요가 없으므로 call stack에 유지시키지 않아도 무관하다.
이처럼 꼬리 호출이 발생할 때 새로운 stack frame을 추가하지 않고 기존 frame을 재사용하여 성능을 향상시키는 최적화 기법이 꼬리 호출 최적화(Tail Call Optimization)이다.

> ***- Stack Frame == Function Frame***
> Stack Frame은 함수가 호출될 때 생성되는 실행 컨텍스트(Execution Context)이며, 호출 스택(Call Stack)에 저장되는 단위이다.
> 환경에 따라 Function Frame이 Stack에 저장되지 않고 Heap에 저장 될 수 있으므로 반드시 Function Frame과 Stack Frame이 동일하지는 않다.

꼬리 호출 최적화는 모든 언어에서 지원되지는 않는다 아래 지원되는 언어와 지원되지 않는 언어들을 몇가지 정리해두겠다.
ChatGPT가 말해준 목록이므로 정확하지 않을 수 있다.

**- 기본적으로 지원하는 언어**
1.	Scheme
2.	Lisp (일부 구현체, 예: Racket, Common Lisp 일부 구현)
3.	Haskell
4.	F#
5.	OCaml
6.	Erlang
7.	Elixir
8.	Scala
9.	Lua

**- 설정 또는 특정 조건에서 지원하는 언어**
1.	JavaScript (Strict mode 및 일부 엔진에서 가능)
2.	Swift (Swift 5 이상에서 일부 최적화 가능)
3.	Dart (일부 경우 최적화 가능)
4.	Python (PyPy에서 제한적으로 지원)

**- 지원하지 않는 주요 언어**
-  C, C++ (최적화 여부는 컴파일러에 따라 다름)
- Java (JVM이 기본적으로 지원하지 않음)
- C# (일부 경우 가능하나 일반적이지 않음)
-	Go (TCO를 제공하지 않음)
-	Rust (의도적으로 지원하지 않음)

### Tail Recursion == 꼬리 재귀

본론으로 돌아와 꼬리 재귀에 대해 설명해보겠다.

> ***꼬리 재귀란 꼬리 호출 최적화를 지원하는 환경에서 재귀 함수에 자기 자신을 꼬리 호출하여 stack overflow와 메모리 낭비를 없앨 수 있는 함수이다.***

### e.g.,
피보나치 수열 계산 함수를 예시로 꼬리 호출 최적화를 해보겠다.

**- 기본 피보나치 수열 계산 함수**
```typescript
'use strict'
function fibonacci(n: number): number {
  if(n <= 1) return n;

  // 함수 호출 후 추가적인 동작 존재
  return fibonacci(n-1) + fibonacci(n-2);
}
```

**- 꼬리 재귀를 활용한 피보나치 수열 계산 함수**
```typescript
'use strict'
function fibonacci_tail(
  n: number, 
  a: number = 0, 
  b: number = 1
): number {
  if(n === 0) return a;
  if(n === 1) return b;

  // 함수 호출 즉시 반환
  return fibonacci_tail(n-1, b, a + b);
}
```