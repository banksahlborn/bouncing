let shapes = []; // list/array
let initialNumberOfShapes = 5;

const SPEED = 3;
const BALL_SIZE_MIN = 10;
const BALL_SIZE_MAX = 50;

function setup() {
  createCanvas(600, 600);
  ellipseMode(RADIUS);
  resetAllBalls();
}

function draw() {
  background(220);
  fill("black");

  for (let shape of shapes) {
    // for each loop (loop over every item)
    drawShape(shape);
    updateShape(shape);

    if (shape.shape === "circle") {
      keepCircleInBounds(shape);
    } else if (shape.shape === "square") {
      keepSquareInBounds(shape);
    }

    // for loop - loop a certain number of times
    // here I am using _nested_ loops
    for (let i = 0; i < shapes.length - 1; i++) {
      for (let j = i + 1; j < shapes.length; j++) {
        if (shapes[i].shape === "circle") { // shapes[i] is a circle
          if (shapes[j].shape === "circle") {
            bounceBalls(shapes[i], shapes[j]);
          } else { // i is a circle, j is a square
            bounceCircleSquare(shapes[i], shapes[j]);
          }
        } else { // shapes[i] is a square          
          if (shapes[j].shape === "circle") {
            // j is a circle, i is a square
            bounceCircleSquare(shapes[j], shapes[i]);
          } else {
            bounceSquareSquare(shapes[i], shapes[j]);
          }
        }
      } // end inner (j) for loop
    } // end outer (i) for loop
  }
}

// if the distance between the centers
//   is less than the sum of their radii
function ballsCollide(ballA, ballB) {
  return (
    dist(
      ballA.position.x,
      ballA.position.y,
      ballB.position.x,
      ballB.position.y
    ) <=
    ballA.radius + ballB.radius
  );
}

function bounceBalls(ballA, ballB) {
  if (ballsCollide(ballA, ballB)) {
    ballA.velocity.x *= -1;
    ballA.velocity.y *= -1;
    ballB.velocity.x *= -1;
    ballB.velocity.y *= -1;
  }
}

function circleRect(cx, cy, radius, rx, ry, rw, rh) {

  // temporary variables to set edges for testing
  let testX = cx;
  let testY = cy;

  // which edge is closest?
  if (cx < rx)         testX = rx;      // test left edge
  else if (cx > rx+rw) testX = rx+rw;   // right edge
  if (cy < ry)         testY = ry;      // top edge
  else if (cy > ry+rh) testY = ry+rh;   // bottom edge

  // get distance from closest edges
  let distX = cx-testX;
  let distY = cy-testY;
  let distance = sqrt( (distX*distX) + (distY*distY) );

  // if the distance is less than the radius, collision!
  if (distance <= radius) {
    return true;
  }
  return false;
}

function bounceSquareSquare(squareA, squareB) {
  if (squareSquare(
    squareA.position.x, squareA.position.y, squareA.size, squareA.size,
    squareB.position.x, squareB.position.y, squareB.size, squareB.size
  )) {
    squareA.velocity.x *= -1;
    squareA.velocity.y *= -1;
    squareB.velocity.x *= -1;
    squareB.velocity.y *= -1;
  }
}

function squareSquare(r1x, r1y, r1w, r1h, r2x, r2y, r2w, r2h) {

  // are the sides of one rectangle touching the other?

  if (r1x + r1w >= r2x &&    // r1 right edge past r2 left
      r1x <= r2x + r2w &&    // r1 left edge past r2 right
      r1y + r1h >= r2y &&    // r1 top edge past r2 bottom
      r1y <= r2y + r2h) {    // r1 bottom edge past r2 top
        return true;
  }
  return false;
}



function bounceCircleSquare(circleA, squareB) {
  if( circleRect(circleA.position.x, circleA.position.y, circleA.radius, squareB.position.x, squareB.position.y, squareB.size, squareB.size) ) {
    circleA.velocity.x *= -1;
    circleA.velocity.y *= -1;
    squareB.velocity.x *= -1;
    squareB.velocity.y *= -1;    
  }
  
}

function keepSquareInBounds(square) {
  // x,y is the upper left corner
  // size is the size
  if (square.position.x + square.size > width) {
    square.velocity.x *= -1;
  }

  if (square.position.y + square.size > height) {
    square.velocity.y *= -1;
  }

  if (square.position.x < 0) {
    square.velocity.x *= -1;
  }

  if (square.position.y < 0) {
    square.velocity.y *= -1;
  }
}

function keepCircleInBounds(ball) {
  if (ball.position.x + ball.radius > width) {
    ball.velocity.x *= -1;
  }

  if (ball.position.y + ball.radius > height) {
    ball.velocity.y *= -1;
  }

  if (ball.position.x - ball.radius < 0) {
    ball.velocity.x *= -1;
  }

  if (ball.position.y - ball.radius < 0) {
    ball.velocity.y *= -1;
  }
}

function resetAllBalls() {
  shapes = []; // create an empty array
  // while loop - loops while a condition is true
  while (shapes.length < initialNumberOfShapes) {
    createShape();
  }
}

function mouseClicked() {
  rotateCreateBall();
}

function rotateCreateBall() {
  shapes.shift(); // remove the oldest ball (front of the array)
  createBall(); // add a ball to the end of the array
}

function keyPressed() {
  if (key === "r") {
    resetAllBalls();
  }

  if (keyIsDown(DELETE) || keyIsDown(BACKSPACE)) {
    balls.shift();
  }

  if (key === " ") {
    createShape();
  }
}

function updateShape(shape) {
  shape.position.y = shape.position.y + shape.velocity.y;
  shape.position.x = shape.position.x + shape.velocity.x;
}

function drawShape(shape) {
  fill(shape.c);
  if (shape.shape === "circle") {
    circle(shape.position.x, shape.position.y, shape.radius);
  } else if (shape.shape === "square") {
    square(shape.position.x, shape.position.y, shape.size);
  }
}

function createShape() {
  if (random() > 0.5) {
    createBall();
  } else {
    createSquare();
  }
}

function createBallAt(position) {
  let newBall = {}; // creating an empty object

  newBall.radius = random(BALL_SIZE_MIN, BALL_SIZE_MAX);
  newBall.position = position;

  //for( let shape of shapes ) {
  //  if( shapesCollide(shape,newBall) ) {
  //    return createBall()
  //  }
  //}

  newBall.c = color(random(256), random(256), random(256));

  newBall.velocity = {
    x: random(-SPEED, SPEED),
    y: random(-SPEED, SPEED),
  };

  newBall.shape = "circle";

  shapes.push(newBall);
}

function createBall() {
  return createBallAt({
    x: random(BALL_SIZE_MAX, width - BALL_SIZE_MAX),
    y: random(BALL_SIZE_MAX, height - BALL_SIZE_MAX),
  });
}

function createSquareAt(position) {
  let newSquare = {}; // creating an empty object

  newSquare.size = random(BALL_SIZE_MIN, BALL_SIZE_MAX);
  newSquare.position = position;

  //for( let shape of shapes ) {
  //  if( shapesCollide(shape,newSquare) ) {
  //    return createSquare()
  //  }
  //}

  newSquare.c = color(random(256), random(256), random(256));

  newSquare.velocity = {
    x: random(-SPEED, SPEED),
    y: random(-SPEED, SPEED),
  };

  newSquare.shape = "square";

  shapes.push(newSquare);
}

function createSquare() {
  return createSquareAt({
    x: random(BALL_SIZE_MAX, width - BALL_SIZE_MAX),
    y: random(BALL_SIZE_MAX, height - BALL_SIZE_MAX),
  });
}

function createBall() {
  return createBallAt({
    x: random(BALL_SIZE_MAX, width - BALL_SIZE_MAX),
    y: random(BALL_SIZE_MAX, height - BALL_SIZE_MAX),
  });
}
