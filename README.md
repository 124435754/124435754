// Get the canvas element
const canvas = document.getElementById('gameCanvas');
const ctx = canvas.getContext('2d');

// Set the canvas dimensions
canvas.width = 400;
canvas.height = 400;

// Define some constants
const BLOCK_SIZE = 20;
const GRID_SIZE = 20;
const COLORS = ['red', 'blue', 'green', 'yellow', 'orange', 'purple'];

// Initialize the game state
let grid = [];
for (let i = 0; i < GRID_SIZE; i++) {
  grid[i] = [];
  for (let j = 0; j < GRID_SIZE; j++) {
    grid[i][j] = 0; // 0 represents an empty block
  }
}

// Function to draw the grid
function drawGrid() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  for (let i = 0; i < GRID_SIZE; i++) {
    for (let j = 0; j < GRID_SIZE; j++) {
      if (grid[i][j]!== 0) {
        ctx.fillStyle = COLORS[grid[i][j] - 1];
        ctx.fillRect(i * BLOCK_SIZE, j * BLOCK_SIZE, BLOCK_SIZE, BLOCK_SIZE);
      }
    }
  }
}

// Function to handle user input (e.g., clicking on a block)
function handleClick(x, y) {
  const blockX = Math.floor(x / BLOCK_SIZE);
  const blockY = Math.floor(y / BLOCK_SIZE);
  if (grid[blockX][blockY] === 0) {
    grid[blockX][blockY] = Math.floor(Math.random() * COLORS.length) + 1;
    drawGrid();
  }
}

// Add an event listener to the canvas
canvas.addEventListener('click', (e) => {
  handleClick(e.offsetX, e.offsetY);
});

// Draw the initial grid
drawGrid();
