###### Graphics Programming - Exercise 8
# Transformations
In this exercise we will look at some transformations using matrices.

## Introduction

1. A matrix looks like the following.
   This is called the identity matrix.
   It has 0's everywhere except for the main diagonal and 1's in the main diagonal.
   Multiplying another matrix by the identity matrix (of the corresponding size) leaves the matrix as it is.
   
   <img src="img/identity.png" height="100px" alt="Identity Matrix"></img>
  
1. Transformations in 2D can be represented as 3x3 matrices. In the matrix below the letters can be replaced by numbers to achieve desired effects such as translating, scaling and rotating, among others.
   <img src="img/transformation.png" height="100px" alt="Transformation Matrix")
  

1. Translation is the name we give to moving an object from one location to another. An object might be a rectangle, circle, triangle or something more complex.
   We replace e in the above matrix with the number we want to translate in the direction of the x axis, and f by that of the y axis.
   If translation is all we want to do, we leave the four other letters as they are in the identity matrix.
   Below is an example of a matrix that will translate objects by (4,6).
   <img src="img/translate.png" height="100px" alt="A translation matrix."></img>
   
1. To use this matrix on a point (x,y), we map (x,y) to a 3x1 matrix, left multiply that by the translation matrix, and then map the product back to a point.
   Below we translate the point (1,1) by the matrix.
   <img src="img/pointtomatrix.png" "Converting a point to matrix."></img>
   <img src="img/translateeg.png" height="100px" alt="A translation matrix example."></img>
   <img src="img/matrixtopoint.png" height="100px" alt= "Converting a matrix to a point."></img>
   

## Exercises
Save each step as a separate source file.

1. Create a blank HTML file with a CSS section and a JavaScript section.

    ```html
    <!DOCTYPE html>
    <html>
      <head>
        <title>Transformations</title>
        <meta charset="UTF-8">
        <style type="text/css"></style>
      </head>
      <body>
        <script type="text/javascript">
        </script>
      </body>
    </html>
    ```

1. Add a cavnas element with an id, and get a context for it.

    ```html
    <canvas id="transcan"></canvas>
    ```
    
    ```js
    var canvas = document.getElementById('transcan');
    var ctx = canvas.getContext('2d');
    ```

1. Create a function for drawing pacman (without the eye, for now) on the canvas.

  ```js
  function drawPacman(size) {
    var size = size || 10;
    ctx.fillStyle = "rgb(230, 230, 0)"
    ctx.beginPath();
    ctx.arc(0, 0, size, Math.PI / 6, 11 * Math.PI / 6);
    ctx.lineTo(0, 0)
    ctx.fill();
  }
  ```

1. Create a function for clearing the canvas. Note the use of save() and restore() on the context.

  ```js
  function clear() {
    ctx.save();
    ctx.setTransform(1, 0, 0, 1, 0, 0);
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    ctx.restore();
  }
  ```
        
1. Create a step function that translates the context by (1,0), and rotates it by π/2 radians every 100 steps.

  ```js
  function step(t) {
    nosteps += 1;
    clear();
    ctx.translate(1, 0);
    if (nosteps % 100 == 0)
      ctx.rotate(Math.PI / 2);
    drawPacman();
    requestAnimationFrame(step);
  }
  ```

1. Set the global variable nosteps to 0, and set an initial translation on the canvas to show pacman fully at the start.

  ```js
  var nosteps = 0;
  ctx.translate(10,10);
  ```
  
1. Start your animation by calling the step() function.

1. Replace the ctx.translate() in step() with a call to ctx.transform().

1. Replace the ctx.rotate() in step() with a call to ctx.transform().

## Advanced exercises.

1. Add an eye to Pacman, and have it translate and rotate correctly with Pacman.

1. Have the text "Rotation" displayed in the centre of the canvas for half a second everytime Pacman rotates, and scale it up in size at each step of the animation.

## Notes

1. [MDN Transformations](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Transformations)