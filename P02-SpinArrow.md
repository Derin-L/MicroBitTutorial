# 돌아가는 화살표

## Step 1

``||basic:화살표 출력||``블록을 가져와 ``||basic:코드 실행 무한반복 실행||`` 안에 넣고,
값을 ArrowNames.North을 ArrowNames.WEST으로 변경하여 왼쪽 화살표를 만들어보세요.

```python
def on_forever():
    basic.show_arrow(ArrowNames.WEST)
basic.forever(on_forever)
```

## Step 2

기존에 만들었던 ``||basic:화살표 출력||`` 블록 아래에 ``||basic:화살표 출력||`` 블록을 추가합니다.

```python
def on_forever():
    basic.show_arrow(ArrowNames.WEST)
    basic.show_arrow(ArrowNames.NORTH)
basic.forever(on_forever)
```

## Step 3

계속해서 오른쪽 화살표(동쪽), 아래쪽 화살표(남쪽)를 차례로 추가합니다.

```python
def on_forever():
    basic.show_arrow(ArrowNames.WEST)
    basic.show_arrow(ArrowNames.NORTH)
    basic.show_arrow(ArrowNames.EAST)
    basic.show_arrow(ArrowNames.SOUTH)
basic.forever(on_forever)
```

## Step 4

이제 가상 @boardname@ 화면을 확인합시다. 화면의 화살표가 돌아가면 완성입니다.

## Step 5

🗨 실습

대각선 화살표를 추가하여 화살표가 조금 더 자연스럽게 돌아가도록 해봅시다.