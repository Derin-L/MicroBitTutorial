# 돌아가는 화살표

## Step 1

``||basic:LED 출력||``블록을 가져와 ``||basic:무한반복 실행||`` 안에 넣고, 왼쪽 화살표 모양을 만들어보세요.

```blocks
basic.forever(function() {
    basic.showLeds(`
            . . # . .
            . # . . .
            # # # # #
            . # . . .
            . . # . .`);
})
```

## Step 2

기존에 만들었던 왼쪽 화살표 ``||basic:LED 출력||`` 블록 아래에 위쪽 화살표 ``||basic:LED 출력||`` 블록을 추가합니다.

```blocks
basic.forever(function() {
    basic.showLeds(`
            . . # . .
            . # . . .
            # # # # #
            . # . . .
            . . # . .`);
    basic.showLeds(`
            . . # . .
            . # # # .
            # . # . #
            . . # . .
            . . # . .`);
})
```

## Step 3

계속해서 오른쪽 화살표, 아래쪽 화살표를 차례로 추가합니다.

## Step 4

이제 가상 @boardname@ 화면을 확인합시다. 화면의 화살표가 돌아가면 완성입니다.