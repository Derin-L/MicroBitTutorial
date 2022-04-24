# 화살표 그리기

## Step 1

``||basic:화살표 출력||``코드를 가져오세요.

```python
basic.show_arrow(ArrowNames.NORTH)
```

## Step 2

``||input:코드 실행 button 누르면 실행||`` 코드를 편집화면으로 가져옵니다.

그리고 기존에 만들었던 ``||basic:화살표 출력||``코드를 안쪽에 옮겨 작성하고 화살표의 방향을 ArrowNames.WEST로 변경합니다.

```python
def on_button_pressed_a():
    basic.show_arrow(ArrowNames.NORTH)
input.on_button_pressed(Button.A, on_button_pressed_a)
```

## Step 3

다시 ``||input:코드 실행 button 누르면 실행||`` 코드를 편집화면으로 가져옵니다.
Button.A 값을 input:Button.B로 변경합니다.

``||basic:화살표 출력||``코드를 안쪽에 옮겨 작성하고 화살표의 방향을 ArrowNames.EAST로 변경합니다.

```python
def on_button_pressed_b():
    basic.show_arrow(ArrowNames.NORTH)
input.on_button_pressed(Button.B, on_button_pressed_b)
```

## Step 5

이제 가상 @boardname@ 화면을 확인하고, A버튼과 B버튼 번갈아 눌러봅시다.

## Step 6

🗨 실습

A버튼과 B버튼을 동시에 누를 경우, 화살표가 위쪽을 가리키게 만들어보세요.