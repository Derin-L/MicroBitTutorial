# 방향 맞추기 게임

## Step 1
화살표 방향에 맞추어 버튼을 누르는 게임을 만들어봅시다.


## Step 2

우선 문제를 만들어내도록 하겠습니다.

``||valuable:변수||`` 항목에서 변수 만들기를 선택합니다. 
이름을 **정답**으로 하여 변수를 새로 생성합니다.

## Step 3

``||valuable:정답||``변수를 ``||math:1부터 2까지의 정수 랜덤값||``으로 변경하세요.
``||logic:만약(if) 참(true) 이면(then) 실행||``를 이용하여 ``||valuable:정답||``이 1이면 왼쪽 화살표, 2면 오른쪽 화살표를 출력하세요.

작성 후, 가상 @boardname@ 화면을 확인하면서
**시뮬레이터 재시작**버튼을 눌러 매번 다른 방향을 가르키는 확인하세요.

``` python
정답 = randint(1, 2)
if 정답 == 1:
    basic.show_arrow(ArrowNames.WEST)
elif 정답 == 2:
    basic.show_arrow(ArrowNames.EAST)
```

## Step 4

문제를 만들어내는 부분을 반복하도록 하겠습니다.

``||basic:일시중지 100(ms)||``와 ``||loops:반복(repeat) : 4회||``를 가져와
임의의 화살표를 출력하는 모든 부분를 0.5초마다 9번 반복하세요.

``` python
for index in range(9):
    정답 = randint(1, 2)
    if 정답 == 1:
        basic.show_arrow(ArrowNames.WEST)
    elif 정답 == 2:
        basic.show_arrow(ArrowNames.EAST)
    basic.pause(500)
```

## Step 5

이번엔 정답을 입력받도록 하겠습니다.
A 또는 B 버튼을 누르면 정답을 입력 받지만 문제 당 1번씩만 입력받아야 합니다.
입력을 받았는지 확인하기 위해서 새로운 변수를 사용하겠습니다.

``||valuable:변수||`` 항목에서 변수 만들기를 선택합니다. 
이름을 **입력대기중**으로 하여 변수를 새로 생성합니다.


## Step 6

프로그램을 시작하자 마자 ``||valuable:입력대기중||``을 ``||logic:거짓(false)||``으로 변경합니다.

그리고, 문제를 만들어내기 전에 ``||valuable:입력대기중||``을 ``||logic:참(true)||``으로 변경합니다.

``` python
입력대기중 = False
for index in range(9):
    입력대기중 = True
    정답 = randint(1, 2)
    if 정답 == 1:
        basic.show_arrow(ArrowNames.WEST)
    elif 정답 == 2:
        basic.show_arrow(ArrowNames.EAST)
    basic.pause(500)
```

## Step 7

입력을 1번만 받도록 준비가 되었으니 버튼 입력을 받아보도록 하겠습니다.

``||input:A 누르면 실행||``을 가져와 ``||valuable:입력대기중||``이 ``||logic:참(true)||``일 때,
``||valuable:입력대기중||``을 ``||logic:거짓(false)||``으로 변경하세요.

이 단계는 버튼이 여러 번 눌리지 않도록 해줍니다.

``` python
def on_button_pressed_a():
    global 입력대기중
    if 입력대기중:
        입력대기중 = False

input.on_button_pressed(Button.A, on_button_pressed_a)
```

## Step 8

버튼을 눌렀을 때, 정답을 눌렀는지 확인하고 결과을 보여줍시다. 
``||input:A 누르면 실행||``은 왼쪽 화살표일 경우 정답입니다.

``||input:A 누르면 실행||``에서 ``||valuable:정답||``이 1이면 ``||basic:아이콘 출력||``으로 ✓모양을 출력하고,
아니면 X 모양을 출력하세요.

``` python
def on_button_pressed_a():
    global 입력대기중
    if 입력대기중:
        입력대기중 = False
        if 정답 == 1:
            basic.show_icon(IconNames.YES)
        else:
            basic.show_icon(IconNames.NO)
            
input.on_button_pressed(Button.A, on_button_pressed_a)
```

# Step 9

``||input:B 누르면 실행||``을 이용해 B버튼을 눌렀을 때도 정답을 눌렀는지 확인하고 결과를 출력해봅시다.

# Step 10

정답을 맞출 때마다 점수를 1씩 올리도록 하겠습니다.

``||valuable:변수||`` 항목에서 변수 만들기를 선택합니다. 
이름을 **점수**로 하여 변수를 새로 생성합니다.


## Step 11

프로그램을 시작하자 마자 ``||valuable:점수||``를 0으로 변경합니다.

``` python
점수 = 0
입력대기중 = False
for index in range(9):
    입력대기중 = True
    정답 = randint(1, 2)
    if 정답 == 1:
        basic.show_arrow(ArrowNames.WEST)
    elif 정답 == 2:
        basic.show_arrow(ArrowNames.EAST)
    basic.pause(500)
```

## Step 12

정답을 맞출 때 마다 점수를 1씩 증가시키세요.

``` python
def on_button_pressed_a():
    global 입력대기중, 정답
    if 입력대기중:
        입력대기중 = False
        if 정답 == 1:
            basic.show_icon(IconNames.YES)
            정답 += 1
        else:
            basic.show_icon(IconNames.NO)

input.on_button_pressed(Button.A, on_button_pressed_a)
```

## Step 13

게임이 종료되면 점수를 출력하세요.

```python
게임중 = False
점수 = 0
입력대기중 = False
for index in range(9):
    입력대기중 = True
    정답 = randint(1, 2)
    if 정답 == 1:
        basic.show_arrow(ArrowNames.WEST)
    elif 정답 == 2:
        basic.show_arrow(ArrowNames.EAST)
    basic.pause(500)
basic.show_number(점수)
```


## Step 14

이제 가상 @boardname@ 화면을 확인하고, 게임을 플레이해보세요.

## Step 15

🗨 실습

화살표를 2방향에서 3방향으로 수정합니다.
위쪽 화살표를 A+B버튼을 정답으로 하도록 추가합니다.