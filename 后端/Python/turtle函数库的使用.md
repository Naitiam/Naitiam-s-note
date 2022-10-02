画蛇案例

```python
import turtle
def drawSnake (rad, angle, len, neckrad):
    for i in range (len) :
        turtle.circle (rad,angle)
        turtle.circle (-rad,angle)
    turtle.circle (rad, angle/2)
    turtle.fd (rad) #直线移动
    turtle.circle (neckrad+1, 180)
    turtle.fd (rad*2/3)
def main() :
    turtle.setup (1300,800, 0, 0) 
    '''
    turtle.setup()函数,启动一个图形窗口 
    turtle.setup(width, height, startx, starty)
    启动窗口的宽度和高度,窗口左上角在屏幕中的坐标位置
    '''
    pythonsize = 30
    turtle.pensize (pythonsize) #运动轨迹的宽度
    turtle.pencolor ( "blue")
    turtle.seth(-40) #turtle.seth(angle)函数,启动时运动的方向,角度值
    drawSnake (40, 80 , 5, pythonsize/2)
main ()
```

