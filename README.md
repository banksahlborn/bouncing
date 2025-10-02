let balls = [] // list/array
let initialNumberOfBalls = 5

const SPEED = 3
const BALL_SIZE_MIN = 10
const BALL_SIZE_MAX = 50

function setup() {
  createCanvas(600, 600)
  ellipseMode(RADIUS)
  resetAllBalls()
}

function draw() {
  background(220)
  fill("black")
  
  for( let ball of balls ) { // for each loop (loop over every item)
    drawBall(ball)
    updateBall(ball)
    keepInBounds(ball)
  }
  
  // for loop - loop a certain number of times
  // here I am using _nested_ loops
  for( let i = 0; i < balls.length - 1; i++ ) { 
    for( let j = i+1; j < balls.length; j++ ) {
      bounceBalls(balls[i], balls[j])
    }
  }
}

// if the distance between the centers 
//   is less than the sum of their radii
function ballsCollide(ballA, ballB) {
  return dist( ballA.position.x, ballA.position.y, ballB.position.x, ballB.position.y ) <= ballA.radius + ballB.radius
}

function bounceBalls(ballA, ballB) {
  if( ballsCollide(ballA, ballB) ) {
    ballA.velocity.x *= -1;
    ballA.velocity.y *= -1;
    ballB.velocity.x *= -1;
    ballB.velocity.y *= -1;
  }
}


function keepInBounds(ball) {
  if( ball.position.x + ball.radius > width ) {
     ball.velocity.x *= -1; 
  }

  if( ball.position.y + ball.radius > height ) {
    ball.velocity.y *= -1; 
  }

  if( ball.position.x - ball.radius < 0 ) {
    ball.velocity.x *= -1; 
  }

  if( ball.position.y - ball.radius < 0 ) {
    ball.velocity.y *= -1; 
  }
}

function resetAllBalls() {
  balls = [] // create an empty array
  // while loop - loops while a condition is true
  while( balls.length < initialNumberOfBalls ) {
    createBall()
  }
}

function mouseClicked() {
  rotateCreateBall()  
}

function rotateCreateBall() {
  balls.shift() // remove the oldest ball (front of the array)
  createBall() // add a ball to the end of the array
}

function keyPressed() {
  if( key === 'r' ) {
    resetAllBalls()
  }

  if( keyIsDown(DELETE) || keyIsDown(BACKSPACE) ) {
    balls.shift()
  }
  
  if( key === ' ' ) {
    createBall()
  }
}

function updateBall(ball) {
  ball.position.y = ball.position.y + ball.velocity.y;
  ball.position.x = ball.position.x + ball.velocity.x;  
}

function drawBall(ball) { 
  fill(ball.c);
  circle(ball.position.x,ball.position.y,ball.radius);  
}

function createBallAt(position) {
  let newBall = {} // creating an empty object
  
  newBall.radius = random(BALL_SIZE_MIN,BALL_SIZE_MAX)
  newBall.position = position
  
  for( let ball of balls ) {
    if( ballsCollide(ball,newBall) ) {
      return createBall()
    }
  }
    
  newBall.c = color(random(256),random(256),random(256))
    
  newBall.velocity = {
    x: random(-SPEED,SPEED),
    y: random(-SPEED,SPEED)
  }
    
  balls.push(newBall)
}


function createBall() {
  createBallAt({
    x: random(BALL_SIZE_MAX, width-BALL_SIZE_MAX),
    y: random(BALL_SIZE_MAX, height-BALL_SIZE_MAX)
  });
 } 
  drawBall(ball1);
