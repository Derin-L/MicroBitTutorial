# 운석충돌!

## Step 1 @unplugged
위에서 떨어지는 운석이 땅에 닿기 전에 미사일로 부셔버리는 게임을 만들어봅시다.
A 또는 B버튼을 이용하여 플레이어를 움직이고, AB버튼을 동시에 눌러 미사일을 발사하세요.

![Thumbnail](https://raw.githubusercontent.com/Derin-L/MicroBitTutorial/master/img/Meteor.gif)

## Step 2
게임에 관한 수치를 조정해주세요.

``||basic:시작하면 실행||``에
``||game:라이프를 0으로 설정||``, ``||game:점수를 0으로 설정||``을 이용하여,
라이프를 3으로 설정하고 점수를 0으로 설정하세요.

```blocks
game.setLife(3)
game.setScore(0)
```

## Step 3
게임 설정이 완료되면 플레이어를 만들어보도록 하겠습니다.

``||basic:시작하면 실행||``에
``||valuable:플레이어||`` 변수를 추가하고
``||game:스프라이트 x좌표 2 y좌표 2||``를 저장하여 플레이어를 만들어주세요.
단, 플레이어의 처음 위치는 x=2, y=4(가운데 아래)로 설정하세요.

```blocks
game.setLife(3)
game.setScore(0)
플레이어 = game.createSprite(2, 4)
```

## Step 4
이번에는 플레이어가 이동하도록 하겠습니다.

A버튼을 누르면 플레이어가 왼쪽으로 한칸 이동하도록 하세요.
``||input:A 누르면 실행||``과 
``||game:sprite의 x좌표를 1만큼 변경||``을 이용하세요.

```blocks
input.onButtonPressed(Button.A, function () {
    let sprite: game.LedSprite = null
    sprite.change(LedSpriteProperty.X, -1)
})
```

## Step 5
B버튼을 누르면 플레이어가 오른쪽으로 한칸 이동하도록 하세요.
``||input:A 누르면 실행||``과 
``||game:sprite의 x좌표를 1만큼 변경||``을 이용하세요.

```blocks
input.onButtonPressed(Button.B, function () {
    let sprite: game.LedSprite = null
    sprite.change(LedSpriteProperty.X, 1)
})
```

## Step 6
플레이어가 완성되었습니다!

가상 @boardname@ 화면을 확인하고, 플레이어가 제대로 움직이는지 확인하세요!

## Step 7
이번에는 미사일을 만들어보겠습니다.

``||basic:시작하면 실행||``에
``||valuable:미사일||`` 변수를 추가하고
``||game:스프라이트 x좌표 2 y좌표 2||``를 저장하여 미사일을 만들어주세요.
단, 미사일의 처음 위치는 플레이어와 같은 위치인 x=2, y=4(가운데 아래)로 설정하세요.

```blocks
game.setLife(3)
game.setScore(0)
플레이어 = game.createSprite(2, 4)
미사일 = game.createSprite(2, 4)
```

## Step 8
미사일을 이전 단계에서 만들었지만,
플레이어가 발사 버튼을 누를 때까지 미사일을 사용하지 않습니다.

``||game:sprite 삭제||``를 이용해 미사일을 만들자마자 삭제하세요.

```blocks
game.setLife(3)
game.setScore(0)
플레이어 = game.createSprite(2, 4)
let 미사일 = game.createSprite(2, 4)
미사일.delete()
```

## Step 9
A버튼과 B버튼을 동시에 누르면 플레이어 미사일을 발사하도록 해보겠습니다.

``||input:A 누르면 실행||``을 이용하고,
다시한번 미사일에 ``||game:스프라이트 x좌표 2 y좌표 2||``를 저장하여 미사일을 만들어주세요.
단, 미사일의 처음 위치는 ``||game:sprite의 x좌표||``를 이용해 플레이어의 위치로 설정하세요.

```blocks
let 미사일: game.LedSprite = null
input.onButtonPressed(Button.AB, function () {
    let 플레이어: game.LedSprite = null
    미사일 = game.createSprite(플레이어.get(LedSpriteProperty.X), 4)
})
```

## Step 10
미사일 변수 하나만으로는 하나의 미사일만 다룰 수 있습니다.

그렇기 때문에, 미사일이 화면에서 삭제되었을 경우에만 미사일을 생성하세요.
``||logic:만약(if)||``과 ``||game:sprite 삭제됨||``을 사용하면 됩니다.

```blocks
let 미사일: game.LedSprite = null
input.onButtonPressed(Button.AB, function () {
    if (미사일.isDeleted()) {
        let 플레이어: game.LedSprite = null
        미사일 = game.createSprite(플레이어.get(LedSpriteProperty.X), 4)
    }
})
```

## Step 11
미사일은 위로 움직여야 합니다. 

``||basic:무한반복 실행||``에
``||game:sprite의 x좌표를 1만큼 변경||``을 이용하여,
미사일이 매번 한 칸씩 위로 이동하도록 하세요.

```blocks
basic.forever(function () {
    let 미사일: game.LedSprite = null
    미사일.change(LedSpriteProperty.Y, -1)
})
```

## Step 12
이전 단계의 코드는 제대로 동작하지 않을 수 있습니다.
왜냐하면 미사일이 없을 때에도, 이동하라는 명령을 내리고 있기 때문이죠.

``||logic:만약(if)||``과 ``||game:sprite 삭제됨||``, ``||logic:반대로(not)||``을 이용해서
미사일이 삭제되지 않았을 때만 이동하도록 이전 코드를 수정하세요.

```blocks
basic.forever(function () {
    let 미사일: game.LedSprite = null
    if (!(미사일.isDeleted())) {
        미사일.change(LedSpriteProperty.Y, -1)
    }
})
```

## Step 13
미사일이 이동하다가 맨 위에 도착하면 화면에서 삭제 해야합니다.

미사일이 이동하기 전, 미사일의 y좌표가 0이면 미사일을 삭제하세요.
``||logic:만약(if)||``, ``||game:sprite의 x좌표||`` 그리고 ``||game:sprite 삭제||``를 사용하세요.

```blocks
basic.forever(function () {
    let 미사일: game.LedSprite = null
    if (!(미사일.isDeleted())) {
        if (미사일.get(LedSpriteProperty.Y) == 0) {
            미사일.delete()
        }
        미사일.change(LedSpriteProperty.Y, -1)
    }
})

```

## Step 14
미사일이 완성되었습니다!

가상 @boardname@ 화면을 확인하고, 플레이어가 미사일을 제대로 발사하는지 확인하세요!

## Step 15
이번에는 운석을 만들어 보겠습니다.

``||basic:시작하면 실행||``에
``||valuable:운석||`` 변수를 추가하고
``||game:스프라이트 x좌표 2 y좌표 2||``를 저장하여 운석을 만들어주세요.
단, 운석의 위치는 ``||math:0부터 10까지의 정수 랜덤값||``을 이용하여
x좌표는 0부터 4사이의 임의의 값, y좌표는 0으로 하세요.

```blocks
game.setLife(3)
game.setScore(0)
플레이어 = game.createSprite(2, 4)
let 미사일 = game.createSprite(2, 4)
미사일.delete()
let 운석 = game.createSprite(randint(0, 4), 0)
```

## Step 16
운석을 깜박이에 만들어서 플레이어랑 다르게 보이도록 만들겠습니다.

``||game:sprite의 x좌표를 0으로 설정||``을 이용해서
운석의 깜박임 속도를 10으로 바꾸세요.

```blocks
game.setLife(3)
game.setScore(0)
플레이어 = game.createSprite(2, 4)
let 미사일 = game.createSprite(2, 4)
미사일.delete()
let 운석 = game.createSprite(randint(0, 4), 0)
운석.set(LedSpriteProperty.Blink, 10)
```

## Step 17
이번에는 운석이 천천히 내려오도록 만들겠습니다.

``||basic:무한반복 실행||``을 이용하면 운석이 너무 빨리 내려옵니다.
``||loop:500ms 마다||``를 이용하면 특정 시간 간격마다 반복되도록 만들 수 있습니다.
``||loop:500ms 마다||``와 ``||game:sprite의 x좌표를 1만큼 변경||``를 이용해서
1초마다 운석이 한 칸씩 내려오도록 하세요.

```blocks
loops.everyInterval(1000, function () {
    let 운석: game.LedSprite = null
    운석.change(LedSpriteProperty.Y, 1)
})
```

## Step 18
운석이 끝까지 내려오게 된다면 플레이어는 라이프를 1개 잃어야합니다.

``||logic:만약(if)||``, ``||game:sprite의 x좌표||`` 그리고 ``||game:라이프를 0만큼 감소||``를 사용하여
운석의 y좌표가 4가 되면 라이프를 1 감소하도록 만드세요.

```blocks
loops.everyInterval(1000, function () {
    let 운석: game.LedSprite = null
    운석.change(LedSpriteProperty.Y, 1)
    if (운석.get(LedSpriteProperty.Y) == 4) {
        game.removeLife(1)
    }
})
```

## Step 19
운석이 끝까지 내려오고나면 다시 운석이 만들어져야 합니다.
하지만 운석을 지웠다가 새로만드는 것보다는 운석을 다시 맨 위로 옮기는 방법이 간단합니다.

``||game:sprite의 x좌표를 0로 설정||``, ``||math:0부터 10까지의 정수 랜덤값||``을
이용하여 운석이 땅에 닿았을 경우 운석의 위치를 맨 위의 임의의 위치로 이동시키세요.

```blocks
loops.everyInterval(1000, function () {
    let 운석: game.LedSprite = null
    운석.change(LedSpriteProperty.Y, 1)
    if (운석.get(LedSpriteProperty.Y) == 4) {
        game.removeLife(1)
        운석.set(LedSpriteProperty.X, randint(0, 4))
        운석.set(LedSpriteProperty.Y, 0)
    }
})
```

## Step 20
마지막으로 미사일이 운석을 없애도록 만들어 보겠습니다.
이 코드는 미사일이 이동하게 만드는 코드에 이어서 작성해야 합니다.

미사일이 이동한 이후, ``||logic:만약(if)||``과 ``||game:sprite가   에 닿았나?||``를
이용하여 운석과 미사일이 닿았는지 확인합니다.

```blocks
basic.forever(function () {
    let 미사일: game.LedSprite = null
    let 운석: game.LedSprite = null
    if (!(미사일.isDeleted())) {
        if (미사일.get(LedSpriteProperty.Y) == 0) {
            미사일.delete()
        }
        미사일.change(LedSpriteProperty.Y, -1)
        if (운석.isTouching(미사일)) {
        }
    }
})
```

## Step 21
미사일이 운석에 닿았다면 운석을 없애야합니다.
이번에도 운석을 없애지 않고 처음 위치로 이동 시키겠습니다.

``||game:sprite의 x좌표를 0로 설정||``, ``||math:0부터 10까지의 정수 랜덤값||``을
이용하여 미사일과 운석이 닿았을 경우 운석의 위치를 맨 위의 임의의 위치로 이동시키세요.

그리고 ``||game:점수를 1만큼 변경||``를 이용하여 운석이 미사일에 제거될 때마다
점수를 1 증가시키세요.

```blocks
basic.forever(function () {
    let 미사일: game.LedSprite = null
    let 운석: game.LedSprite = null
    if (!(미사일.isDeleted())) {
        if (미사일.get(LedSpriteProperty.Y) == 0) {
            미사일.delete()
        }
        미사일.change(LedSpriteProperty.Y, -1)
        if (운석.isTouching(미사일)) {
            운석.set(LedSpriteProperty.X, randint(0, 4))
            운석.set(LedSpriteProperty.Y, 0)
            game.addScore(1)
        }
    }
})
```

## Step 22
이제 가상 @boardname@ 화면을 확인하고, 게임을 플레이해보세요.

## Step 23 @unplugged
🗨 실습1

운석을 얻을 때마다 운석의 속도가 점점 빨라지게 만들어보세요.

## Step 24 @unplugged
🗨 실습2

운석이 1개가 아니고 동시에 2개가 화면에 나오도록 만들어보세요.