# Python小游戏_飞机大战—pygame

## 1.初始化 显示窗口

```python
# 初始化
pygame.init()
screen = pygame.display.set_mode((800, 600))#显示窗口
pygame.display.set_caption('打飞机')#名字
icon = pygame.image.load('ufo.png')#图标
pygame.display.set_icon(icon)
bgImg = pygame.image.load('bg.png')
```



## 2.主循环

+ 背景一定要写在主循环中，否则有重影

```python
running = True
while running:
    screen.blit(bgImg, (0, 0))
    for event in pygame.event.get():
        if event.type == pygame.QUIT:#退出
            running = False
            
    pygame.display.update()#显示图像的需写在这个之前
```

## 3.显示玩家

```python
# 玩家
playerImg = pygame.image.load('player.png')
playerX = 400
playerY = 500
playerStep = 0

#主循环中
screen.blit(playerImg, (playerX, playerY))
```



## 4.移动玩家

```python
for event in pygame.event.get():
    if event.type == pygame.QUIT:
        running = False
# 键盘
    if event.type == pygame.KEYDOWN:
        if event.key == pygame.K_RIGHT:#左右移动
            playerStep = 5
        elif event.key == pygame.K_LEFT:
            playerStep = -5
        elif event.key == pygame.K_SPACE:#发射子弹
            bullets.append(Bullet())


# 松开时不动
    if event.type == pygame.KEYUP:
        playerStep = 0
```

## 5.控制出界

```python
def move_player():
    global playerX
    playerX += playerStep
    # 控制出界
    if playerX > 736:
        playerX = 736
    if playerX < 0:
        playerX = 0
```

## 6.敌人

```python
number_of_enemy = 6
enemies = []
enemyImg = pygame.image.load('enemy.png')
class Enemy():#创建敌人类
    def __init__(self):
        self.enemyImg = pygame.image.load('enemy.png')
        self.x = random.randint(200, 600)#随机位置
        self.y = random.randint(50, 250)
        self.step = random.randint(1, 2)
    def reset(self):
        self.x = random.randint(200, 600)#被击中后
        self.y = random.randint(50, 250)
for i in range(number_of_enemy):#添加多个敌人
    enemies.append(Enemy())


def show_enemy():#画敌人
    global enemyX, enemyStep,enemyY,is_over
    for e in enemies:
        screen.blit(enemyImg, (e.x, e.y))
        e.x += e.step
        if (e.x < 0  or e.x > 736):
            e.step *= -1
            e.y += 20
        if e.y > 450:#游戏失败
            is_over = True
            enemies.clear()
```



## 7.子弹

```python
bullets = []
class Bullet():
    def __init__(self):
        self.img = pygame.image.load('bullet.png')
        self.x = playerX + 15
        self.y = playerY + 10
        self.step = 5
    def hit(self):#击中判断
        global score
        for e in enemies:
            if(distance(e.x, e.y, self.x, self.y) < 30):
                bullets.remove(self)
                e.reset()#重置敌人
                score += 1
def show_bullet():#画子弹
    for b in bullets:
        screen.blit(b.img, (b.x, b.y))
        b.hit()
        b.y -= 3
        if b.y < 0:
            bullets.remove(b)
```

## 8.射中检测

```python
def distance(ex,ey,bx,by):#计算距离
    a = bx - ex
    b = by - ey
    return math.sqrt(a*a + b*b)
```

