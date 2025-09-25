# Encapsulate-your-moving-shape-into-an-object-and-boundary-checking

let ball1, ball2, ball3;

let SPEED = 3;

function setup() {
  createCanvas(600, 600);
  ellipseMode(RADIUS);
  resetAllBalls()
}

function draw() {
  background(220);
  drawBall(ball1);
  updateBall(ball1);
 keepInBounds(ball1)
  drawBall(ball2);
  keepInBounds(ball2)
  updateBall(ball2);
  drawBall(ball3);
  updateBall(ball3);
  keepInBounds(ball3)
}

//function bounceballs(ballA, ballB){}
//if distance between the center is less than the sum of their radi
//if(dist(ballA.x,ballA.y,ballB.x,ballB.y)
  
  
  function keepInBounds(ball) {
  
  if( ball.x + ball.radius > width ) {
     ball.dx = ball.dx * -1; // change x direction
  }
  
  if( ball.y + ball.radius > height ) {
    ball.dy = ball.dy * -1; // change y direction
  }
  
  if( ball.x - ball.radius < 0 ) {
    ball.dx = ball.dx * -1; // change x direction
  }
  
  if( ball.y - ball.radius < 0 ) {
    ball.dy = ball.dy * -1; // change y direction
  }
 
}

function resetAllBalls() {
  ball1 = createBall()
  ball2 = createBall()
  ball3 = createBall()  
}

function mouseClicked() {
  resetAllBalls()
}

function updateBall(ball) {
  ball.y = ball.y + ball.dy;
  ball.x = ball.x + ball.dx;  
}

function drawBall(ball) { // implicit declaration of the variable (parameter) ball
  fill(ball.c);
  circle(ball.x,ball.y,ball.radius);  
}

function createBall() {
  let ball = {} // creating an empty object
  // assigning properties to that object
  ball.c = color(random(256),random(256),random(256))
  ball.x = width/2;
  ball.y = height/2;
  ball.dx = random(-SPEED,SPEED);
  ball.dy = random(-SPEED,SPEED);
  ball.radius = random(10,50);  
  return ball;
}
