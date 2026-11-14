```
from turtle import Turtle, Screen
from paddle import Paddle
from ball import Ball
from scoreboard import Scoreboard
import time


screen = Screen()
screen.setup(width=800, height=600)
screen.bgcolor("black")
screen.title("Pong")
screen.tracer(0)

pads = Paddle((350,0))
pad_2 = Paddle((-350,0))
ball = Ball()
scoreboard = Scoreboard()

screen.listen()

screen.onkeypress(pads.up,"Up")
screen.onkeypress(pads.down,"Down")
screen.onkeypress(pad_2.up,"w")
screen.onkeypress(pad_2.down,"s")

game_is_on=True
while game_is_on:
    time.sleep(ball.move_speed)
    screen.update()
    ball.move()

    if ball.ycor() > 280 or ball.ycor() < -280:
        ball.bounce_y()
        
    if (ball.distance(pads) < 60 and ball.xcor() > 320) or (ball.distance(pad_2) < 60 and ball.xcor() < -320):
        ball.bounce_x()

    #right wall 
    if ball.xcor() > 380:
        scoreboard.l_point()
        ball.ball_reset()

    #left wall 
    if ball.xcor() < -380:
        scoreboard.r_point()
        ball.ball_reset()

    # if l_score == 5 or r_score == 5:
    #     game_is_on = False
    #     self.write("Game Over")


screen.exitonclick()
```

