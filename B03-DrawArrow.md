# 화살표 그리기

## Step 1

``||basic:LED 출력||``블록을 가져와 ``||basic:시작하면 실행||`` 안에 넣고, 왼쪽 화살표 모양을 만들어보세요.

```blocks
basic.showLeds(`
        . . # . .
        . # . . .
        # # # # #
        . # . . .
        . . # . .`);
```

## Step 2

``||input:A 누르면 실행||`` 블록을 코드 편집화면으로 가져옵니다.

그리고 기존에 만들었던 왼쪽 화살표 ``||basic:LED 출력||``블록을 옮겨 넣습니다.

```blocks
input.onButtonPressed(Button.A, function() {
    basic.showLeds(`
            . . # . .
            . # . . .
            # # # # #
            . # . . .
            . . # . .`);
})
```

## Step 3

또 다시 ``||input:A 누르면 실행||`` 블록을 코드 편집화면으로 가져옵니다.
``||input:A||``의 값을 ``||input:B||``로 변경합니다.

그리고 ``||basic:LED 출력||``블록을 안에 넣고, 오른쪽 화살표 모양을 만들어보세요.

## Step 5

이제 가상 @boardname@ 화면을 확인하고, A버튼과 B버튼 번갈아 눌러봅시다.