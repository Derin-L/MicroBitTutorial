# 카운터 만들기

## Step 1

B버튼을 누르면 숫자가 1씩 증가하는 카운터를 만들어봅시다.

## Step 2

``||valuable:변수||`` 항목에서 변수 만들기를 선택합니다. 
이름을 'number'로 하여 변수를 새로 생성합니다.

``||valuable:number에 0 저장||`` 을 가져와 ``||basic:시작하면 실행||`` 에 배치를 합니다.

```blocks
number = 0
```

## Step 3

``||basic:수 출력||``블록을 가져와 ``||input:B 누르면 실행||`` 안에 배치해보세요.
그리고 ``||basic:수 출력||``의 0을 number로 변경하세요.

```blocks
input.onButtonPressed(Button.B, function () {
    basic.showNumber(number)
})
```

## Step 4

``||valuable:number값 1 증가||`` 을 가져와 ``||input:B 누르면 실행||`` 맨 위에 배치를 합니다.

그리고 ``||basic:수 출력||`` 블럭의 값을 0에서 ``||valuable:number||`` 로 변경합니다.


```blocks
input.onButtonPressed(Button.B, function () {
    number += 1
    basic.showNumber(number)
})
```

## Step 4

이제 가상 @boardname@ 화면을 확인하고, B버튼을 누르면 숫자가 올라가는지 확인하세요.

## Step 5

🗨실습

A버튼을 누르면 숫자가 1씩 내려가도록 만들어보세요.