# 카운터 만들기

## Step 1

B버튼을 누르면 숫자가 1씩 증가하는 카운터를 만들어봅시다.

## Step 2

``||valuable:item = 0||`` 코드를 가져와서 
'item'변수를 0으로 선언합니다.

```python
item = 0
```

## Step 3

``||basic:수 출력 value||``코드와 ``||input:코드 실행 button 누르면 실행||``를 이용하여
item의 값을 화면에 출력하세요.

```python
def on_button_pressed_b():
    basic.show_number(item)
input.on_button_pressed(Button.B, on_button_pressed_b)
```

## Step 4

 ``||input:코드 실행 button 누르면 실행||``안에서 item의 값을 화면에 출력하기 전에 item을 1 증가시키세요.

🗨 Tip : 밖에서 사용한 변수를 def(함수) 안에서 사용하기 위해서는 global을 붙여야합니다.

```python
def on_button_pressed_b():
    global item
    item += 1
    basic.show_number(item)
input.on_button_pressed(Button.B, on_button_pressed_b)
```

## Step 4

이제 가상 @boardname@ 화면을 확인하고, B버튼을 누르면 숫자가 올라가는지 확인하세요.

## Step 5

🗨 실습

A버튼을 누르면 숫자가 1씩 내려가도록 만들어보세요.