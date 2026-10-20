# spiderman-clock-
python coded spiderman clock 

import turtle
import time

# 1. Setup the Screen
screen = turtle.Screen()
screen.title("Spider Clock")
screen.bgcolor("red")
screen.setup(width=600, height=600)
screen.tracer(0) # Turns off automatic animation for instant drawing

# 2. Create drawing pens
pen = turtle.Turtle()
pen.hideturtle()
pen.speed(0)

hands_pen = turtle.Turtle()
hands_pen.hideturtle()
hands_pen.speed(0)

def draw_spider_web_and_numbers():
    pen.clear()
    pen.color("black")
    pen.pensize(1)
    
    # Draw web rings
    for radius in range(40, 220, 40):
        pen.penup()
        pen.goto(0, -radius)
        pen.pendown()
        pen.circle(radius, steps=12) # 12-sided polygon for web effect
        
    # Draw web threads & clock numbers
    for i in range(12):
        angle = i * 30
        
        # Threads
        pen.penup()
        pen.goto(0, 0)
        pen.setheading(90 - angle)
        pen.pendown()
        pen.forward(200)
        
        # Numbers
        pen.penup()
        pen.goto(0, 0)
        pen.setheading(90 - angle)
        pen.forward(230)
        number = 12 if i == 0 else i
        pen.write(str(number), align="center", font=("Arial", 16, "bold"))

def draw_spider_body():
    pen.color("black")
    
    # Spider Abdomen
    pen.penup()
    pen.goto(0, -12)
    pen.begin_fill()
    pen.circle(12)
    pen.end_fill()
    
    # Spider Head
    pen.goto(0, 5)
    pen.begin_fill()
    pen.circle(7)
    pen.end_fill()
    
    # Static short legs
    for i in range(8):
        pen.penup()
        pen.goto(0, 0)
        pen.setheading(45 * i)
        pen.forward(12)
        pen.pendown()
        pen.pensize(2)
        pen.forward(15)

def draw_hand(length, angle, width, color):
    hands_pen.penup()
    hands_pen.goto(0, 0)
    hands_pen.color(color)
    hands_pen.setheading(90 - angle)
    hands_pen.pensize(width)
    hands_pen.pendown()
    hands_pen.forward(length)

def update_clock():
    hands_pen.clear()
    
    # Get current local time
    current_time = time.localtime()
    hours = current_time.tm_hour % 12
    minutes = current_time.tm_min
    seconds = current_time.tm_sec
    
    # Calculate angles for hands
    hour_angle = (hours * 30) + (minutes * 0.5)
    minute_angle = (minutes * 6) + (seconds * 0.1)
    second_angle = seconds * 6
    
    # Draw Hands (acting as the long spider legs)
    draw_hand(100, hour_angle, 6, "black") # Hour hand
    draw_hand(150, minute_angle, 4, "black") # Minute hand
    draw_hand(180, second_angle, 2, "black") # Second hand
    
    screen.update()
    
    # Call this function again after 1000ms (1 second)
    screen.ontimer(update_clock, 1000)

# 3. Initialize and run
draw_spider_web_and_numbers()
draw_spider_body()
update_clock()

# Keep the window open
turtle.done()
