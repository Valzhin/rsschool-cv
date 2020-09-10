# Valzhyna Lialkova #

## Contact Info ##

**_phone_** : +375(25)9010985

**_mail_**: <emilia.blek@yandex.ru>

## Summary ##

I'm interested in working as a front-end developer, because this profession will allow me to realize my desire for new knowledge, constant development and pumping of my brain. It is important for me that the work isn't simple and monotonous and it allows me to realize all my ambitions, and my diligence and perfectionism are adequately rewarded.

## Skills ##

* HTML

* CSS

* JavaScript

* some Git

* some jQuery

## Code examples ##

```javascript
    <!DOCTYPE html>
    <html>
    <head>
	    <meta charset="UTF-8">
	    <title>Snake</title>
    </head>
    <body>
    <canvas id="canvas" width="600" height="600"></canvas>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/2.2.0/jquery.min.js"></script>

    <script>
    
      var canvas = document.getElementById("canvas");
      var ctx = canvas.getContext("2d");
  
      var width = canvas.width;
      var height = canvas.height;
  
      var blockSize = 10;
      var widthInBlocks = width / blockSize;
      var heightInBlocks = height / blockSize;
  
      var score = 0;
  
      var drawBorder = function () {
        ctx.fillStyle = "Gray";
	      ctx.fillRect(0, 0, width, blockSize);
	      ctx.fillRect(0, height - blockSize, width, blockSize);
	      ctx.fillRect(0, 0, blockSize, height);
	      ctx.fillRect(width - blockSize, 0, blockSize, height);
      };
	
      var drawScore = function () {
        ctx.font = "20px Courier";
	      ctx.fillStyle = "Black";
	      ctx.textAlign = "left";
	      ctx.textBaseline = "top";
	      ctx.fillText("Счёт: " + score, blockSize, blockSize);
      };
  
      var gameOver = function () {
        clearInterval(intervald);
	      ctx.font = "60px Courier";
	      ctx.fillStyle = "Black";
	      ctx.textAlign = "center";
	      ctx.textBaseline = "middle";
	      ctx.fillText("Конец игры", width / 2, height / 2);
      };
  
      var circle = function (x, y, radius, fillCircle) {
        ctx.beginPath();
	      ctx.arc(x, y, radius, 0, Math.PI * 2, false);
	     if (fillCircle) {
	      ctx.fill();
	     } else {
	      ctx.stroke();
	     }
      };
  
      var Block = function (col, row) {
        this.col = col;
        this.row = row;
      };
  
      Block.prototype.drawSquare = function (color) {
        var x = this.col * blockSize;
	      var y = this.row * blockSize;
	      ctx.fillStyle = color;
	      ctx.fillRect(x, y, blockSize, blockSize);
      };
  
      Block.prototype.drawCircle = function (color) {
        var centerX = this.col * blockSize + blockSize / 2;
	      var centerY = this.row * blockSize + blockSize / 2;
        ctx.fillStyle = color;
	      circle(centerX, centerY, blockSize / 2, true);
      };
  
      Block.prototype.equal = function (otherBlock) {
        return this.col === otherBlock.col && this.row === otherBlock.row;
      };
  
      var Snake = function () {
        this.segments = [
	      new Block(7, 5),
	      new Block(6, 5),
	      new Block(5, 5)
        ];
        this.direction = "right";
	      this.nextDirection = "right";
      };
  
      Snake.prototype.draw = function () {
        for (var i = 0; i < this.segments.length; i++) {
	      this.segments[i].drawSquare("Blue");
        }
      };
      Snake.prototype.move = function () {
        var head = this.segments[0];
        var newHead;
	    this.direction = this.nextDirection;
	    if (this.direction === "right") {
	      newHead = new Block(head.col + 1, head.row);
	    } else if (this.direction === "down") {
	      newHead = new Block(head.col, head.row + 1);
	    } else if (this.direction === "left") {
	      newHead = new Block(head.col - 1, head.row);
	    } else if (this.direction === "up") {
	      newHead = new Block(head.col, head.row - 1);
	    }
	    if (this.checkCollision(newHead)) {
	      gameOver();
	      return;
	    }
	    this.segments.unshift(newHead);
	    if (newHead.equal(apple.position)) {
	      score++;
	      apple.move();
	    } else {
	      this.segments.pop();
	    }
      };
      Snake.prototype.checkCollision = function (head) {
        var leftCollision = (head.col === 0);
	    var topCollision = (head.row === 0);
	    var rightCollision = (head.col === widthInBlocks - 1);
	    var bottomCollision = (head.row === heightInBlocks -1);
	    var wallCollision = leftCollision || topCollision || rightCollision || bottomCollision;
	    var selfCollision = false;
	    for (var i = 0; i < this.segments.length; i++) {
	      if (head.equal(this.segments[i])) {
	        selfCollision = true;
	      }
	    }
	    return wallCollision || selfCollision;
      };
  
    
      Snake.prototype.setDirection = function (newDirection) {
        if (this.direction === "up" && newDirection === "down") {
	      return;
	    } else if (this.direction === "right" && newDirection === "left") {
	      return;
	    } else if (this.direction === "down" && newDirection === "up") {
	      return;
	    } else if (this.direction === "left" && newDirection === "right") {
	      return;
	    }
	    this.nextDirection = newDirection;
      };
  
      var Apple = function () {
        this.position = new Block(10, 10);
      };
  
      Apple.prototype.draw = function() {
        this.position.drawCircle("LimeGreen");
      };
  
      Apple.prototype.move = function () {
        var randomCol = Math.floor(Math.random() * (heightInBlocks - 2)) + 1;
	      var randomRow = Math.floor(Math.random() * (heightInBlocks - 2)) + 1;
	      this.position = new Block(randomCol, randomRow);
      };
  
      var snake = new Snake();
      var apple = new Apple();
  
      var intervald = setInterval(function () {
        ctx.clearRect(0, 0, width, height);
	      drawScore();
	      snake.move();
	      snake.draw();
	      apple.draw();
	      drawBorder();
      }, 100);
  
       var direction = {
         37: "left",
	       38: "up",
	       39: "right",
	      40: "down"
      };
  
      $("body").keydown(function (event) {
        var newDirection = direction[event.keyCode];
	    if (newDirection !== undefined) {
	      snake.setDirection(newDirection);
	    }
      });

    </script>	
    </body>
    </html>
```

## Experience ##

So far, my experience has been completing tasks in HTML, CSS, and JavaScript in various free online courses and from tutorials, since I started learning front-end three months ago.

## Education ##

I have an incomplete higher education in history, which helped me to understand that I'm not a humanitarian :)
At the moment I'm taking courses on front-end from RS-school.

## English ##

English is at ==A2== level, but I try to improve my level with the help of online courses.

