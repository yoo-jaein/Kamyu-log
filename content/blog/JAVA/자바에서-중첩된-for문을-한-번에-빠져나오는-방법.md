---
title: 자바에서 중첩된 for문을 한 번에 빠져나오는 방법
date: 2020-07-28 15:07:16
category: java
draft: false
---

## 들어가기
자바에서 중첩된 for문을 한 번에 빠져나오는 3가지 방법에 대해 알아본다. 

- 목차
	- [들어가기](#들어가기) 
    - [중첩된 for문](#중첩된-for문) 
    - [방법 1: if문과 flag](#방법-1-if문과-flag)
    - [방법 2: Label을 설정하는 break문](#방법-2-label을-설정하는-break문)
    - [방법 3: goto문](#방법-3-goto문) 
    - [마무리](#마무리) 

## 중첩된 for문

1부터 9까지 계산하는 구구단에서 곱이 72인 계산식을 하나 출력하려고 한다. 구구단을 계산하기 위해 for문을 중첩하여 사용했다.

```java
for(int i=1; i<10; i++) {
    for(int j=1; j<10; j++>) {
        if((i*j) == 72) {
            System.out.println(i + " x " + j + " = " + i*j);
        }
    }
}
```

하지만 이 코드는 하나가 아니라 i*j가 72인 모든 경우가 출력된다. 그래서 하나를 출력하고나면 모든 for문을 종료해줄 필요가 있다. 어떻게 하면 중첩된 for문을 한 번에 종료할 수 있을까?

## 방법 1: if문과 flag

첫 번째로 `flag` 변수를 사용하는 방법이 있다. 반복문의 종료 조건이 만족되는 경우 flag의 값을 바꿔 바깥쪽 반복문까지 종료할 수 있게 해준다.

```java
boolean flag = false;

for(int i=1; i<10; i++) {
    for(int j=1; j<10; j++>) {
        if((i*j) == 72) {
            System.out.println(i + " x " + j + " = " + i*j);
            flag = true;
            break;
        }
    }
    if(flag)
    break;
}
```

## 방법 2: Label을 설정하는 break문

두 번째는 `Label`을 설정하는 방법이다. __반복문에 Label 이름을 붙여 break문에 해당 이름을 명시해주면 된다.__ 나는 바깥쪽 반복문이라는 뜻으로 outer라는 이름을 붙였다.

```java
outer:
for(int i=1; i<10; i++) {
    for(int j=1; j<10; j++>) {
        if((i*j) == 72) {
            System.out.println(i + " x " + j + " = " + i*j);
            break outer;
        }
    }
}
```

## 방법 3: goto문

마지막 goto문의 경우 코드의 가독성이 떨어지기 때문에 자주 사용하지 않는게 좋다고 배웠다. 그래도 참고로 알아두자.

```java
for(int i=1; i<10; i++) {
    for(int j=1; j<10; j++>) {
        if((i*j) == 72) {
            System.out.println(i + " x " + j + " = " + i*j);
            goto label;
        }
    }
}
label:
```

## 마무리
1. 중첩된 for문을 한 번에 종료하려면 `Label`을 사용하는 것이 좋다.