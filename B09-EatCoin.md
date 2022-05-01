# 코인 모으기

## Step 1 @unplugged
플레이어가 화면을 돌아다니며 반짝이는 코인을 모으는 게임을 만들어봅시다.
플레이어가 벽을 넘어가면 라이프가 줄어들고 라이프가 없어지면 게임오버입니다.

![Timer Stop](https://raw.githubusercontent.com/Derin-L/MicroBitTutorial/master/img/EatCoin.gif)

## Step 2
게임을 시작하자마자 관련된 수치를 조정해주세요. ``||game:라이프를 3으로 설정||``, ``||game:점수를 0으로 설정||``

```blocks
game.setLife(0)
game.setScore(0)
```

## Step 3
게임 설정이 완료되면 플레이어를 만들어보도록 하겠습니다.

``||valuable:플레이어||`` 변수를 추가하고 ``||game:스프라이트 x좌표 2 y좌표 2||``를 저장하세요.

```blocks
game.setLife(0)
game.setScore(0)
플레이어 = game.createSprite(2, 2)
```

## Step 4
이번에는 플레이어가 주기적으로 이동하도록 하겠습니다.

게임에서 사용하는 스프라이트는 각각 이동방향을 가지고 있습니다.
``||game:플레이어를 1만큼 이동||``을 이용하면 플레이어가 이동하게 됩니다.
``||loops:1000ms 마다||``와 ``||game:플레이어를 1만큼 이동||``을 이용해 플레이어가 1초마다 1칸씩 이동하도록 만드세요.

```blocks
let 플레이어: game.LedSprite = null
loops.everyInterval(1000, function () {
    플레이어.move(1)
})
```

## Step 5
플레이어의 이동방향은 ``||game:플레이어의 이동방향을 오른쪽방향으로 45(°) 회전||``을 이용하여 조절 할 수 있습니다.

A버튼을 눌렀을 때, 플레이어의 이동방향을 왼쪽으로 90도 회전하도록 만들어주세요.

```blocks
let 플레이어: game.LedSprite = null
input.onButtonPressed(Button.A, function () {
    플레이어.turn(Direction.Left, 90)
})
```

## Step 6
B버튼을 눌렀을 때, 플레이어의 이동방향을 오른쪽으로 90도 회전하도록 만들어주세요.

## Step 7
이번엔 플레이어가 벽을 넘어가면 라이프가 감소하도록 만들어 보겠습니다.

플레이어가 벽에 닿으면 더 이상 이동하지 않습니다.
그 점을 이용하여 플레이어의 위치가 이전과 동일하면 벽을 넘어갔다고 할 수 있습니다.

## Step 8
플레이어가 이동하기 전에 위치를 저장하겠습니다.

``||valuable:이전x좌표||``, ``||valuable:이전y좌표||``변수를 추가하고
이동하기 전의 위치를 ``||game:플레이어x좌표||``, ``||game:플레이어y좌표||``로부터 가져와 저장합니다.

```blocks
let 이전x좌표 = 0
let 이전y좌표 = 0
let 플레이어: game.LedSprite = null
loops.everyInterval(1000, function () {
    이전x좌표 = 플레이어.get(LedSpriteProperty.X)
    이전y좌표 = 플레이어.get(LedSpriteProperty.Y)
    플레이어.move(1)
})
```

## Step 9
플레이어가 이동한 후에도 위치가 ``||valuable:이전x좌표||``, ``||valuable:이전y좌표||``와 같다면
벽에 막혀 이동하지 못한 것이기 때문에 ``||game:라이프를 1만큼 감소||``를 이용해 라이프를 1 감소시킵니다.

이때, x좌표와 y좌표가 모두 같아야하기 때문에 ``||logic:그리고(and)||``를 사용합니다.

```blocks
let 이전x좌표 = 0
let 이전y좌표 = 0
let 플레이어: game.LedSprite = null
loops.everyInterval(1000, function () {
    이전x좌표 = 플레이어.get(LedSpriteProperty.X)
    이전y좌표 = 플레이어.get(LedSpriteProperty.Y)
    플레이어.move(1)
    if (이전x좌표 == 플레이어.get(LedSpriteProperty.X) && 이전y좌표 == 플레이어.get(LedSpriteProperty.Y)) {
        game.removeLife(1)
    }
})
```

## Step 10
라이프를 1 감소시킨 뒤, 플레이어 위치를 다시 처음으로 돌립니다.

``||game:플레이어의 x좌표를 0으로 설정||``을 이용하여 플레이어의 x좌표와 y좌표 모두 2로 설정합니다.

```blocks
let 이전x좌표 = 0
let 이전y좌표 = 0
let 플레이어: game.LedSprite = null
loops.everyInterval(1000, function () {
    이전x좌표 = 플레이어.get(LedSpriteProperty.X)
    이전y좌표 = 플레이어.get(LedSpriteProperty.Y)
    플레이어.move(1)
    if (이전x좌표 == 플레이어.get(LedSpriteProperty.X) && 이전y좌표 == 플레이어.get(LedSpriteProperty.Y)) {
        game.removeLife(1)
        플레이어.set(LedSpriteProperty.X, 2)
        플레이어.set(LedSpriteProperty.Y, 2)
    }
})
```

## Step 11
이번에는 플레이어가 닿으면 점수를 얻는 코인을 만들어보겠습니다.

플레이어와 같은 방식으로 만들어줍니다.
``||valuable:코인||`` 변수를 추가하고 ``||game:스프라이트 x좌표 2 y좌표 2||``를 저장하세요.
코인의 생성 위치는 x좌표, y좌표 모두 0~4사이의 임의의 수를 가지도록 ``||math:0부터 10까지의 정수 랜덤값||``을 적절히 사용하세요.

```blocks
'플레이어 생성'
코인 = game.createSprite(randint(0, 4), randint(0, 4))
```

## Step 12
현재 플레이어와 코인이 구분되지 않습니다.

``||game:코인의 x좌표를 0으로 설정||``을 이용하여 코인의 깜박임 속도를 10으로 설정하세요.

```blocks
'플레이어 생성'
let 코인 = game.createSprite(randint(0, 4), randint(0, 4))
코인.set(LedSpriteProperty.Blink, 10)
```

## Step 13
이제 플레이어가 코인을 얻도록 만들어봅시다.

``||logic:만약(if)||``, ``||game:sprite가   에 닿았나?||``를 이용하여 플레이어가 코인에 닿았는지 확인합시다.

```blocks
let 플레이어: game.LedSprite = null
let 코인: game.LedSprite = null
loops.everyInterval(1000, function () {
    '플레이어 이동'
    if (플레이어.isTouching(코인)) {
    }
})
```

## Step 14

플레이어가 코인을 얻으면 점수를 1 올리고, 코인을 다른 곳으로 이동시키겠습니다.

플레이어가 코인에 닿으면 ``||game:점수를 1만큼 변경||``을 이용해 점수를 1 증가시키고,
``||game:sprite의 x좌표를 0으로 설정||``을 이용해 코인의 위치를 x좌표, y좌표 모두 0~4사이의 임의의 수로 이동시킵니다.

```blocks
let 코인: game.LedSprite = null
loops.everyInterval(1000, function () {
    '플레이어 이동'
    if (플레이어.isTouching(코인)) {
        game.addScore(1)
        코인.set(LedSpriteProperty.X, randint(0, 4))
        코인.set(LedSpriteProperty.Y, randint(0, 4))
    }
})
```

## Step 15
이제 가상 @boardname@ 화면을 확인하고, 게임 설정을 바꾸어가며 플레이해보세요.

## Step 16 @unplugged
🗨 실습

코인을 얻을 때마다 플레이어가 점점 빨라지게 만들어보세요.