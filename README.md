import turtle
wn = turtle.Screen()
wn.title("Pong by Jaroslav Franc")
wn.bgcolor("black")
wn.setup(width=800, height=600)
wn.tracer(0)
#Score
score_a = 0
score_b = 0
#Palka A
palka_a = turtle.Turtle()
palka_a.speed(0)
palka_a.shape("square")
palka_a.color("white")
palka_a.shapesize(stretch_wid=5, stretch_len=1)
palka_a.penup()
palka_a.goto(-350, 0)
#Palka B
palka_b = turtle.Turtle()
palka_b.speed(0)
palka_b.shape("square")
palka_b.color("white")
palka_b.shapesize(stretch_wid=5, stretch_len=1)
palka_b.penup()
palka_b.goto(350, 0)
#Balon
balon = turtle.Turtle()
balon.speed(0)
balon.shape("square")
balon.color("white")
balon.penup()
balon.goto(0, 0)
balon.dx = 0.1
balon.dy = -0.1
#Pero
pero = turtle.Turtle()
pero.speed(0)
pero.color("white")
pero.penup()
pero.hideturtle()
pero.goto(0, 260)
pero.write("Hrac Tata: 0  Hrac Amlka: 0", align= "center", font= ("Courier", 24, "normal"))
#Funkce
def palka_a_up():
    y = palka_a.ycor()
    y += 20
    palka_a.sety(y)
def palka_a_down():
    y = palka_a.ycor()
    y -= 20
    palka_a.sety(y)
def palka_b_up():
    y = palka_b.ycor()
    y += 20
    palka_b.sety(y)
def palka_b_down():
    y = palka_b.ycor()
    y -= 20
    palka_b.sety(y)
#Klavesnice
wn.listen()
wn.onkeypress(palka_a_up, "w")
wn.onkeypress(palka_a_down, "s")
wn.onkeypress(palka_b_up, "Up")
wn.onkeypress(palka_b_down, "Down")
#Main game loop
while True:
    wn.update()
    #Pohyb balonu
    balon.setx(balon.xcor() + balon.dx)
    balon.sety(balon.ycor() + balon.dy)
    #Kontrola hranic
    if balon.ycor() > 290:
        balon.sety(290)
        balon.dy *= -1
    if balon.ycor() < -290:
        balon.sety(-290)
        balon.dy *= -1
    if balon.xcor() > 390:
        balon.goto(0, 0)
        balon.dx *= -1
        score_a += 1
        pero.clear()
        pero.write("Hrac Tata: {}  Hrac Amalka: {}".format(score_a, score_b), align="center", font=("Courier", 24, "normal"))
    if balon.xcor() < -390:
        balon.goto(0, 0)
        balon.dx *= -1
        score_b  += 1
        pero.clear()
        pero.write("Hrac Tata: {}  Hrac Amalka: {}".format(score_a, score_b), align="center", font=("Courier", 24, "normal"))
    #Kolize palky a balonu
    if (balon.xcor() > 340 and balon.xcor() < 350) and (balon.ycor() < palka_b.ycor() + 40 and balon.ycor() > palka_b.ycor() -40):
        balon.setx(340)
        balon.dx *= -1
    if (balon.xcor() < -340 and balon.xcor() > -350) and (balon.ycor() < palka_a.ycor() + 40 and balon.ycor() > palka_a.ycor() -40):
        balon.setx(-340)
        balon.dx *= -1
