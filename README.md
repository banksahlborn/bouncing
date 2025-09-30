SKIP TO PLAY SKETCH
Autosave enabled.


File
Edit
Sketch
Help
English
Hello, Banksahlborn!



Auto-refresh

Honored croissant

Public
p5.js 1.11.10


sketch.js
Saved: just now
1
let balls = [] // list/array
2
let initialNumberOfBalls = 4
3
​
4
const SPEED = 5 //(5) - (6) ITS SUBTRACTION but how do you get it as a range 
5
const BALL_SIZE_MIN = 15
6
const BALL_SIZE_MAX = 55
7
​
8
function setup() {
9
  createCanvas(600, 600)
10
  ellipseMode(RADIUS)
11
  resetAllBalls()
12
}
13
​
14
function draw() {
15
  background(11, 3, 252)
16
  fill("black")
17
  
18
  for( let ball of balls ) { // for each loop (loop over every item)
19
    drawBall(ball)
20
    updateBall(ball)
21
    keepInBounds(ball)
22
  }
23
  
24
  // for loop - loop a certain number of times
25
  // here I am using _nested_ loops
26
  for( let i = 0; i < balls.length - 1; i++ ) { 
27
    for( let j = i+1; j < balls.length; j++ ) {
28
      bounceBalls(balls[i], balls[j])
29
    }
30
  }
31
}
32
​
33
// if the distance between the centers 
34
//   is less than the sum of their radi
35
function ballsCollide(ballA, ballB) {
36
  return dist( ballA.position.x, ballA.position.y, ballB.position.x, ballB.position.y ) <= ballA.radius + ballB.radius
37
}
38
​
39
function bounceBalls(ballA, ballB) {
40
  if( ballsCollide(ballA, ballB) ) {
41
    ballA.velocity.x *= -1;
42
    ballA.velocity.y *= -1;
43
    ballB.velocity.x *= -1;
44
    ballB.velocity.y *= -1;
45
  }
46
}
47
​
48
​
49
function keepInBounds(ball) {
50
  if( ball.position.x + ball.radius > width ) {
51
     ball.velocity.x *= -1; 
52
  }
53
​
54
  if( ball.position.y + ball.radius > height ) {
There are no lint messages
Current lineline 136
Console
Clear

​
Preview

Complete your gift to make an impact
Donate
