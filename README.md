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
        if (shapes[i].shape === "circle") {
          if (shapes[j].shape === "circle") {
            bounceBalls(shapes[i], shapes[j]);
          } else {
            if (shapes[j].shape === "circle") {
            }
            if (shapes[i].shape === "square") {
              bounceCircleSquare(shapes[i], shapes[j]);
            }
          }
        } else {
          // shapes[i] is a square
          if (shapes[j].shape === "circle") {
            bounceCircleSquare(shapes[j], shapes[i]);
          } else {
            bounceSquareSquare(shapes[i], shapes[j]);
            if (shapes[i].shape === "square") {
            }
            if (shapes[j].shape === "square") {
            }
          }
        }
      }
    }
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

function bounceSquareSquare(squareA, squareB) {}

function bounceCircleSquare(circleA, squareB) {}

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
