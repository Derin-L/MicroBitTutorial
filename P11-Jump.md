# 인터넷 안 될 때, 그 게임

## Step 1 @unplugged
점프를 하여 앞에서 다가오는 장애물을 피하는 게임을 만들어봅시다.

![Thumbnail](https://raw.githubusercontent.com/Derin-L/MicroBitTutorial/master/img/Jump.gif)

## Step 2
게임에 관한 수치를 조정해주세요.

``||basic:시작하면 실행||``에
``||game:라이프를 0으로 설정||``, ``||game:점수를 0으로 설정||``을 이용하여,
라이프를 5으로 설정하고 점수를 0으로 설정하세요.

```python
game.set_life(5)
game.set_score(0)
```

## Step 3
게임 설정이 완료되면 플레이어를 만들어보도록 하겠습니다.

``||basic:시작하면 실행||``에
``||valuable:플레이어||`` 변수를 추가하고
``||game:스프라이트 x좌표 2 y좌표 2||``를 저장하여 플레이어를 만들어주세요.
단, 플레이어의 처음 위치는 x=1, y=4로 설정하세요.

``||valuable:플레이어에 0 저장||``을 이용하세요.

```python
플레이어: game.LedSprite = None
game.set_life(5)
game.set_score(0)
플레이어 = game.create_sprite(1, 4)
```

## Step 4
이번에는 플레이어가 점프하도록 하겠습니다.

A버튼과 B버튼을 동시에 누르면 플레이어가 위쪽으로 두칸 이동하도록 하세요.
``||input:A 누르면 실행||``과 
``||game:sprite의 x좌표를 1만큼 변경||``을 이용하세요.

```python
def on_button_pressed_ab():
    플레이어.change(LedSpriteProperty.Y, -2)
input.on_button_pressed(Button.AB, on_button_pressed_ab)

```

## Step 5
플레이어가 점프를 하고나면 땅으로 내려와야합니다.
플레이어의 y좌표를 매번 1씩 증가시키세요.

``||basic:무한반복 실행||``과 
``||game:sprite의 x좌표를 1만큼 변경||``을 이용하세요.

```python
def on_forever():
    플레이어.change(LedSpriteProperty.Y, 1)
basic.forever(on_forever)
```

## Step 6
지금까지 작업한 코드를 실행하여 A버튼과 B버튼을 동시에 연타해봅시다.
플레이어가 꼭대기까지 올라가게 됩니다.
이것을 방지하기 위해 플레이어가 땅에 닿았을 때만 점프하도록 만들어봅시다.

``||logic:만약(if)||``과 ``||game:sprite가 벽에 닿았나?||``를 사용하면 됩니다.

```python
def on_button_pressed_ab():
    if 플레이어.is_touching_edge():
        플레이어.change(LedSpriteProperty.Y, -2)
input.on_button_pressed(Button.AB, on_button_pressed_ab)
```

## Step 7
플레이어가 점프하고나서 너무 빨리 떨어지지 않나요?
점프하고나서 얼마간의 시간동안 플레이어가 떠있도록 만들어줍시다.

``||valuable:점프지속시간||`` 변수를 추가하고
점프하는 순간에 ``||valuable:점프지속시간에 0 저장||``을 이용하여 점프지속시간을 20으로 변경해주세요.

```python
global 점프지속시간 = 0

def on_button_pressed_ab():
    if 플레이어.is_touching_edge():
        플레이어.change(LedSpriteProperty.Y, -2)
        점프지속시간 = 20
input.on_button_pressed(Button.AB, on_button_pressed_ab)
```

## Step 8
기존에 작성했던 플레이어가 땅으로 내려오는 코드를 수정하도록 합시다.

``||valuable:점프지속시간||``이 0보다 작은경우에만 플레이어가 떨어지도록하고
``||valuable:점프지속시간||``이 0 이상일 경우에는 ``||valuable:점프지속시간||``을 1 줄여주세요.

``||valuable:점프지속시간값 1 증가||``을 이용하면 됩니다.

```python
def on_forever():
    if 점프지속시간 < 0:
        플레이어.change(LedSpriteProperty.Y, 1)
    else:
        점프지속시간 += -1
basic.forever(on_forever)
```

## Step 9
플레이어가 완성되었습니다!

가상 @boardname@ 화면을 확인하고, 플레이어가 제대로 움직이는지 확인하세요!

## Step 10
이번에는 장애물을 만들어보겠습니다.

``||function:함수||`` 탭에서 [함수 만들기...]를 선택하세요.
그리고 ``||function:장애물추가||``이름으로 함수를 생성하세요.

```python
def 장애물추가():
```

## Step 11
``||function:장애물추가||``에
``||valuable:장애물||`` 변수를 추가하고
``||game:스프라이트 x좌표 2 y좌표 2||``를 저장하여 장애물을 만들어주세요.

단, 장애물의 위치는 ``||valuable:플레이어에 0 저장||``을 이용하여 x=4, y=4(가운데 오른쪽)로 설정하세요.
그리고 ``||game:sprite의 x좌표를 0로 설정||``을 이용하여 장애물의 깜박임 속도를 10으로 지정하세요.


```python
def 장애물추가():
    global 장애물
    장애물 = game.create_sprite(4, 4)
    장애물.set(LedSpriteProperty.BLINK, 10)
```

## Step 12
게임을 시작하자말자 장애물을 생성하세요.

```python
점프지속시간 = 0
game.set_life(5)
game.set_score(0)
플레이어 = game.create_sprite(1, 4)
장애물추가()
```

## Step 13
화면의 장애물이 움직이도록 만들어봅시다.

200ms(0.2초)마다 장애물이 삭제되지 않았다면 장애물의 x좌표가 -1씩 변경되도록 하세요.
``||loop:500ms 마다||``, ``||logic:만약(if)||``, ``||game:sprite 삭제됨||``과 ``||game:sprite의 x좌표를 0로 설정||`를 사용하세요.

```python
def on_every_obj_interval():
    if not (장애물.is_deleted()):
        장애물.change(LedSpriteProperty.X, -1)
loops.every_interval(200, on_every_obj_interval)
```

## Step 14
장애물이 이동하기 전에 장애물이 왼쪽 끝(x좌표 = 0)에 도달했다면 장애물을 삭제하세요.

``||logic:만약(if)||``, ``||game:sprite의 x좌표||``와 ``||game:sprite 삭제||``을 사용하면 됩니다.

```python
def on_every_obj_interval():
    if not (장애물.is_deleted()):
        if 장애물.get(LedSpriteProperty.X) == 0:
            장애물.delete()
        장애물.change(LedSpriteProperty.X, -1)
loops.every_interval(200, on_every_obj_interval)
```

## Step 15
장애물이 이동하기 전에 장애물이 플레이어에 닿았다면 장애물을 삭제하세요.

``||logic:만약(if)||``, ``||game:sprite가  에 닿았나?||``와 ``||game:sprite 삭제||``을 사용하면 됩니다.

```python
def on_every_obj_interval():
    if not (장애물.is_deleted()):
        if 장애물.is_touching(플레이어):
            장애물.delete()
        if 장애물.get(LedSpriteProperty.X) == 0:
            장애물.delete()
        장애물.change(LedSpriteProperty.X, -1)
loops.every_interval(200, on_every_obj_interval)
```

## Step 16
장애물이 플레이어에 닿아서 사라졌다면 라이플를 1 감소시키고,
장애물이 왼쪽 끝에 닿아서 사라졌다면 점수를 1 증가시키세요.

``||game:라이프를 0만큼 감소||``와 ``||game:점수를 1만큼 변경||``을 사용하세요.

```python
def on_every_obj_interval():
    if not (장애물.is_deleted()):
        if 장애물.is_touching(플레이어):
            장애물.delete()
            game.remove_life(1)
        if 장애물.get(LedSpriteProperty.X) == 0:
            장애물.delete()
            game.add_score(1)
        장애물.change(LedSpriteProperty.X, -1)
loops.every_interval(200, on_every_obj_interval)
```

## Step 17
1000ms(1초)에서 3000ms(3초)사이의 임의의 시간마다 장애물이 삭제되지 않았다면
장애물을 추가하세요.

``||math:0부터 10까지의 정수 랜덤값||``, ``||loop:500ms 마다||``, ``||logic:만약(if)||``, ``||game:sprite 삭제됨||``과
이전에 만든 ``||function:장애물추가||``를 사용하세요.

```python
def on_every_interval():
    if 장애물.is_deleted():
        장애물추가()
loops.every_interval(randint(1000, 3000), on_every_interval)
```

## Step 18
이제 가상 @boardname@ 화면을 확인하고, 게임을 플레이해보세요.

## Step 19 @unplugged
🗨 실습

A버튼을 누를때마다 장애물의 이동속도가 느려지게하고 B버튼을 누를때마다 장애물의 이동속도가 빨라지게 만들어보세요.