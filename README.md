let ball1, ball2, ball3;

let SPEED = 5;

function setup() {
  createCanvas(500, 600);
  ellipseMode(RADIUS);
  resetAllBalls()
}

function draw() {
  background(11, 3, 252);
  drawBall(ball1);
  updateBall(ball1);
  keepInBounds(ball1);
  drawBall(ball2);
  updateBall(ball2);
  keepInBounds(ball2);
  drawBall(ball3);
  updateBall(ball3);
  keepInBounds(ball3);
  bounceBalls(ball1,ball2);
  bounceBalls(ball2,ball3);
  bounceBalls(ball1,ball3);
}

function bounceBalls(ballA, ballB) {
  // if the distance between the centers is less than the sum of their radii
  if( dist(ballA.x,ballA.y,ballB.x,ballB.y) <= ballA.radius + ballB.radius ) {
    ballA.dx = ballA.dx * -1;
    ballA.dy = ballA.dy * -1;
    ballB.dx = ballB.dx * -1;
    ballB.dy = ballB.dy * -1;
  }
}


function keepInBounds(ball) {
  // ball.x + ball.r > width, then we are off the screen // right
  if( ball.x + ball.radius > width ) {
     ball.dx = ball.dx * -1; // change x direction
  }
  // ball.y + ball.r > height, then we are off the screen // bottom
  if( ball.y + ball.radius > height ) {
    ball.dy = ball.dy * -1; // change y direction
  }
  // ball.x - ball.r < 0, then we are off the screen // left
  if( ball.x - ball.radius < 0 ) {
    ball.dx = ball.dx * -1; // change x direction
  }
  // ball.y - ball.r > 0, then we are off the screen // top
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
  square(ball.x,ball.y,ball.radius);  
}

function createBall() {
  let ball = {} // creating an empty object
  // assigning properties to that object
  ball.c = color(random(256),random(256),random(256));
  ball.radius = random(10,50); 
  ball.x = random(ball.radius, width-ball.radius);
  ball.y = random(ball.radius, height-ball.radius);
  ball.dx = random(-SPEED,SPEED);
  ball.dy = random(-SPEED,SPEED);
  ball.radius = random(10,50);  
  return ball;
}
