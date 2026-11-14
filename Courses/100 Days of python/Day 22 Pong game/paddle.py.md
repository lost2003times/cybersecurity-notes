```
from turtle import Turtle

class Paddle(Turtle):
    def __init__(self,position):
        super().__init__()
        self.color("white")
        self.shape("square")
        self.shapesize(1,6)
        self.penup()
        self.goto(position)
        self.setheading(90)

    def up(self):
        self.forward(20)

    def down(self):
        self.backward(20)
```

