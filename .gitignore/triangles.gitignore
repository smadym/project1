// Random color picker
var r, g, b

//Saves all the lines
var lines = [];

//False is the default setting for this variable
var drawing = false;

//Variable to decide when to start new shape
var new1 = 0;

//Variable to store current and previous mouse values
var current;
var last;

function setup() {
	// Makes canvas size at 600x600
	createCanvas(600,600);

	// Creates vector shape based on x & y starting position
	current = createVector(0,0);
	last = createVector(0,0);

}

function draw() {
	// Color the background and will eventually be used
	// to help clear out the background and refresh canvas
	background(176,244,230);

// Value for random colors within a range
	r = random(255);
	g = random(255);
	b = random(255);

	// Record time to draw a new circle/drawing
	if (millis() > new1 && drawing) {

		// Record the x & y value of the mouse position
		// plus some random movement
		current.x = mouseX+random(50);
		current.y = mouseY+random(50);

		// Base the speed on the movement of the mouse
		// Creating new variable
		// Here the sub subtracts from the shape of the vector
		var move = p5.Vector.sub(current, last);
		// Multiply the vector to change location across the screen
		move.mult(0.15);

		// Adds new shapes and randomize
		lines[lines.length - 1].add(current, move);
		new1 = millis() + random(150);

		// Store x & y values
		last.x = current.x;
		last.y = current.y;

	}
//For loop to update and display
for(var i = 0; i < lines.length; i++){
	lines[i].update();
	lines[i].display();
}
}


//Start the drawing with a mouse press to meet all the parameters below
function mousePressed(){
	next = 0;
	drawing = true;
	last.x = mouseX;
	last.y = mouseY;
	lines.push(new Line());
}


//Stop the drawing when mouse is released
function mouseReleased(){
	drawing = false;
}

//Function to create particle system
function Line(){
	this.circles = [];
	this.color = (r,g,b);
}

//Working with particle system deciding its location, color and movement
Line.prototype.add = function(position, move){
	this.circles.push(new Circle(position, move, this.color));
}

//Display and update particle system
Line.prototype.update = function(){
	for (var i = 0; i < this.circles.length; i++){
		this.circles[i].update();
	}
}

//Decides when particles will appear and dissapear
Line.prototype.display = function(){
for (var i = this.circles.length - 1; i >= 0; i--){
	if (this.circles[i].life <= 0) {
		this.circles.splice(i, 1); 

	} else {
		this.circles[i].display(this.circles[i+1]);
	}
	}
}

//Passing through parameters of postion, movement, disappearance and color
function Circle(position, move, color) {
this.position = createVector(position.x, position.y);
this.speed = createVector(move.x, move.y);
this.move2 = random();
this.life = 200;
}

Circle.prototype.update = function(){
	this.position.add(this.speed);
	this.speed.mult(this.move2);
	this.life--;
}

//I'm still really playing around here figuring out the lines and such
Circle.prototype.display = function(word) {
	strokeWeight(2);
	stroke(0, this.life);
	fill(r, g, b, this.life/4);
	star(this.position.x, this.position.y, 10, 10, 1.5);
	noStroke() //remove to add lines
	if(word){
		line(this.position.x, this.position.y, word.position.x, word.position.y);
	}
}
//Altered star shape made into a function and called out above
  function star(x, y, radius1, radius2, npoints) { //Determines the properties of the star itself {
  angle = TWO_PI / npoints; //Determines the number of points
  halfAngle = angle/2.0; //Evens out the inner angles of where the star meets
  beginShape();
  for (a = 0; a < TWO_PI; a += angle) //Determines the angle at which the brush will paint 
  {
    // Sets the outer verticies of the star
    sx = x + cos(a) * radius2;
    sy = y + sin(a) * radius2;
    vertex(sx, sy); 

    // Sets the inner verticies of the star
    sx = x + cos(a+halfAngle) * radius1;
    sy = y + sin(a+halfAngle) * radius1;
    vertex(sx, sy);
  }
  endShape(CLOSE);
}
