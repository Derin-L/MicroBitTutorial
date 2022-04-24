# 카운터 만들기

## Step 1

``||basic:수 출력||``블록을 가져와 ``||basic:시작하면 실행||`` 안에 넣고, 숫자 5을 표시해보세요.

```blocks
basic.showNumber(0)
```

## Step 2

이번에는 변수를 사용해 보겠습니다.
``||valuable:변수||`` 항목에서 변수 만들기를 선택합니다.
새 변수의 이름을 'number'로 하여 변수를 새로 생성합니다.

`||valuable:number||`이 보이면 제대로 생성이 된겁니다.

## Step 3

``||valuable:number에 0 저장||`` 을 가져와 ``||basic:시작하면 실행||`` 맨 위에 배치를 합니다. 그리고 값을 0에서 5로 바꿉니다.

그리고 ``||basic:수 출력||`` 블럭의 값을 0에서 ``||valuable:number||`` 로 변경합니다.


```blocks
number = 5
basic.showNumber(number)
```

## Step 4

이제 가상 @boardname@ 화면을 확인하고, ``||valuable:number||`` 값을 바꾸어가며 출력해보세요.

## Step 5

숫자가 3, 2, 1을 차례대로 화면에 표시하도록 해보세요.