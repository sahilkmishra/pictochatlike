<script >
	// logic goes here
/*const paintCanvas = document.querySelector( '.js-paint' );
const context = paintCanvas.getContext( '2d' );
context.lineCap = 'round';

const colorPicker = document.querySelector( '.js-color-picker');

    //on:mouseout={stopDrawing}
colorPicker.addEventListener( 'change', event => {
} );

const lineWidthRange = document.querySelector( '.js-line-range' );
const lineWidthLabel = document.querySelector( '.js-range-value' );

lineWidthRange.addEventListener( 'input', event => {
    const width = event.target.value;
    lineWidthLabel.innerHTML = width;
    context.lineWidth = width;
} );

let x = 0, y = 0;
let isMouseDown = false;


paintCanvas.addEventListener( 'mousedown', startDrawing );
paintCanvas.addEventListener( 'mousemove', drawLine );
paintCanvas.addEventListener( 'mouseup', stopDrawing );
paintCanvas.addEventListener( 'mouseout', stopDrawing );*/
//let context = paintCanvas.getContext( '2d' );
//context.lineCap = 'round';
import { getContext, onMount } from 'svelte';
let paintCanvas;
let context;
onMount(() => {
 context = paintCanvas.getContext("2d");
context.lineCap = 'round';
	});
let x = 0, y = 0;
let isMouseDown = false;
let width=1;

function lineWidthChange(event) {
    width = event.target.value;
    context.lineWidth = width;
}
function changeColor(event) {
    context.strokeStyle = event.target.value; 
}
function stopDrawing(event) { isMouseDown = false; }
function startDrawing(event) {
   isMouseDown = true;
   x = event.offsetX;
   y = event.offsetY;
}
function drawLine(event) {
    if ( isMouseDown ) {
        let newX = event.offsetX;
        let newY = event.offsetY;
        context.beginPath();
        context.moveTo( x, y );
        context.lineTo( newX, newY );
        context.stroke();
        //[x, y] = [newX, newY];
        x = newX;
        y = newY;
    }
}
</script>

<!-- markup (zero or more items) goes here -->
<input type="color"  class="js-color-picker  color-picker" on:change={changeColor}>
<input type="range" class="js-line-range" min="1" max="72" value="1" on:input={lineWidthChange}>
<label class="js-range-value">{width}</label>Px
  <canvas 
    class="canvas" 
  id="draw" width="480" height="320" 
  style="background-color:white;"
    on:mousedown={startDrawing}
    on:mouseup={stopDrawing}
    on:mousemove={drawLine} 
  bind:this={paintCanvas}
>
  </canvas>

<style>
.paint-canvas {
  border: 1px black solid;
  display: block;
  margin: 1rem;
}

.color-picker {
  margin: 1rem 1rem 0 1rem;
}
</style>
