# bouncing
function draw() {
  background(220);
square(ballx,bally,radius);
  bally=bally -4;   //how much it goes down
  ballx=ballx -6.     //how much it goes to the left
  
}




let ball={};  //object

let ballx, bally, radius,dx,dy;
let c;
let speed=3
function setup() {
  createCanvas(800, 800);
  ellipseMode(RADIUS);
  ball.c=color(random(256),random(256),random(256))
   ballx=random(width/2);
   bally=random(height/2);
   dx=random(-speed,speed);
   dy=random(-speed,speed);
  radius=30;
  
  }
