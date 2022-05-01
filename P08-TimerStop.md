# 타이밍 맞춰 버튼 누르기

## Step 1 @unplugged

화면의 게이지가 최대치에 도달하는 순간 버튼을 누르는 게임을 만들어 봅시다.

![Timer Stop](https://raw.githubusercontent.com/Derin-L/MicroBitTutorial/master/img/TimerStop1.gif)

## Step 2
게임을 시작하자마자 관련된 수치를 조정해주세요. ``||game:라이프를 1으로 설정||``, ``||game:점수를 0으로 설정||``

라이프가 0이 되면 게임이 종료되며, 점수를 화면에 보여주게 되어 있습니다.

```python
game.set_life(1)
game.set_score(0)
```

## Step 3

순서대로 게이지가 1칸씩 증가하다가 게이지가 가득차면 처음부터 시작하도록 만들어보세요.

``||basic:무한반복 실행||``을 이용하며 전체를 반복하게 하고,
``||loops:반복(for)||``와 ``||logic:만약(if)||``를 활용해 게이지를 구현하세요.

```python
def on_forever():
    for index in range(4):
        if index == 0:
            # 0칸 게이지 그리기
        elif index == 1:
            # 1칸 게이지 그리기
        elif index == 2:
            # 2칸 게이지 그리기
        else:
            # 3칸 게이지 그리기
        
        if input.button_is_pressed(Button.AB):
            if index == 5:
                basic.show_icon(IconNames.YES)
                game.add_score(1)
            else:
                basic.show_icon(IconNames.NO)
                game.remove_life(1)
            break
basic.forever(on_forever)
```

## Step 4

버튼 입력을 받아봅시다. 이번에는 ``||logic:만약(if)||``과 ``||input:A+B 눌림 상태||``를 이용하세요.

```python
def on_forever():
    for index in range(4):
        # 게이지 그리기
        if input.button_is_pressed(Button.AB):
            # 버튼이 눌렸습니다.
basic.forever(on_forever)
```

## Step 5

버튼이 눌렸을 떄, 게이지가 가득 차있다면 ✓모양을 출력하고 아니면 X 모양을 출력하세요.

```python
def on_forever():
    for index in range(4):
        # 게이지 그리기
        if input.button_is_pressed(Button.AB):
            if index == 3:
                basic.show_icon(IconNames.YES)
            else:
                basic.show_icon(IconNames.NO)
basic.forever(on_forever)
```

## Step 6

게이지가 가득 차있을 때 버튼을 누르는데 성공했다면 ``||game:점수를 1만큼 변경||``을 이용해 점수를 1 증가시키고,
실패했다면  ``||game:라이프를 1만큼 감소||``을 이용해 라이프를 1 감소시키세요.

```python
def on_forever():
    for index in range(4):
        # 게이지 그리기
        if input.button_is_pressed(Button.AB):
            if index == 5:
                basic.show_icon(IconNames.YES)
                game.add_score(1)
            else:
                basic.show_icon(IconNames.NO)
                game.remove_life(1)
basic.forever(on_forever)
```

## Step 7

버튼을 누르면 성공과는 상관없이 게이지를 처음부터 시작해야합니다.
``||loops:반복 실행 중단(break)||``을 이용하여 버튼을 누르면 마지막 단계에서 반복을 종료하세요.

```python
def on_forever():
    for index in range(4):
        # 게이지 그리기
        if input.button_is_pressed(Button.AB):
            if index == 5:
                basic.show_icon(IconNames.YES)
                game.add_score(1)
            else:
                basic.show_icon(IconNames.NO)
                game.remove_life(1)
            break
basic.forever(on_forever)
```

## Step 8

이제 가상 @boardname@ 화면을 확인하고, 게임 설정을 바꾸어가며 플레이해보세요.

## Step 9 @unplugged

🗨 실습

게이지를 3단계에서 5단계로 바꾸어 게임을 만들어보세요.

![Timer Stop](https://raw.githubusercontent.com/Derin-L/MicroBitTutorial/master/img/TimerStop2.gif)