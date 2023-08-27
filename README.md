# Whiteboard Web Application

This is a simple web application that allows users to draw on a virtual whiteboard using their mouse. It also provides features to delete the drawing and undo the last action.

## Table of Contents

- [Demo](#demo)
- [Screenshots](#screenshots)
- [Features](#features)
- [How it Works](#howitworks)
- [Installation](#installation)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)
- [Author](#author)

## Demo

Check out the live demo of the whiteboard application [here](https://22pankajsahu.github.io/m6weeklytest3/).

## Screenshots

Include relevant screenshots of the application here:

![1 Screenshot 2023-08-27 ](https://github.com/22pankajsahu/m6weeklytest3/assets/135128502/f9d47ed0-fb55-4a41-af70-6b9d0ade9841)
![2 Screenshot 2023-08-27 ](https://github.com/22pankajsahu/m6weeklytest3/assets/135128502/a9be3708-01a6-43b8-89fe-97d82714c201)

## Features

- Draw freely on the virtual whiteboard.
- Delete the entire drawing with the "Delete" button.
- Undo the last drawing action using the "Undo" button.

## How it Works <div id="howitworks"></div>

The whiteboard application is built using HTML, CSS, and JavaScript. Here's a brief overview of how each component contributes to the functionality:

### HTML (index.html)

The HTML file sets up the structure of the web page and includes the following elements:

- The canvas element (`<canvas>`) is used as the drawing area for the whiteboard.
- Two buttons are provided: "Delete" and "Undo", which users can interact with.

```markdown

    <div id="whiteboard" style="width: 800px; height: 600px;">
        <canvas id="canvas" width="800" height="600"></canvas>
    </div>
    <div id="controls">
        <button id="delete">Delete</button>
        <button id="undo">Undo</button>
    </div>

```

### CSS (style tag)

The CSS file provides styling to the different elements of the whiteboard application:

- The whiteboard area (`#whiteboard`) is given a border and background color to create the appearance of a whiteboard.
- The control buttons (`#controls`) are styled with margin, padding, and cursor properties.

```markdown

    body {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
            background-color: #f0f0f0;
        }

        #whiteboard {
            border: 1px solid #000;
            background-color: #fff;
        }

        #controls {
            margin-top: 10px;
        }

        button {
            margin: 5px;
            padding: 8px 12px;
            font-size: 14px;
            cursor: pointer;
        }

```

### JavaScript (script tag)

The JavaScript file provides the interactivity and functionality of the whiteboard application:

1. **Drawing Functionality**
   - The `mousedown` event starts the drawing when the user presses the mouse button.
   - The `mousemove` event is used to track the mouse movement and draw lines on the canvas as the user moves the mouse.
   - The `mouseup` and `mouseout` events stop the drawing when the user releases the mouse button or moves the mouse out of the canvas area.
   - The drawing actions are recorded in the `actions` array as image data using the `ctx.getImageData` method.

2. **Delete Button**
   - The "Delete" button, when clicked, calls the `clearCanvas` function, which clears the entire canvas using the `ctx.clearRect` method. It also resets the `actions` array.

3. **Undo Button**
   - The "Undo" button, when clicked, calls the `undoAction` function, which removes the last recorded action from the `actions` array and restores the canvas to the previous state using the `ctx.putImageData` method.

## JS Functionality

The JavaScript functionality in this application primarily revolves around the Canvas API (`ctx`) and event listeners:

- The Canvas API is used to draw lines on the canvas, set line properties (color, width, cap), and capture image data for undo functionality.
- Event listeners (`mousedown`, `mousemove`, `mouseup`, `mouseout`, `click`) are used to track user interactions (drawing, button clicks) and trigger appropriate functions.

By combining these components, the whiteboard web application allows users to draw, delete their drawings, and undo previous actions.

```
    const canvas = document.getElementById('canvas');
    const ctx = canvas.getContext('2d');
    const deleteButton = document.getElementById('delete');
    const undoButton = document.getElementById('undo');
    
    let drawing = false;
    let lastX = 0;
    let lastY = 0;
    let actions = [];

    canvas.addEventListener('mousedown', startDrawing);
    canvas.addEventListener('mousemove', draw);
    canvas.addEventListener('mouseup', stopDrawing);
    canvas.addEventListener('mouseout', stopDrawing);
    deleteButton.addEventListener('click', clearCanvas);
    undoButton.addEventListener('click', undoAction);
    
    function startDrawing(e) {
        drawing = true;
        [lastX, lastY] = [e.offsetX, e.offsetY];
    }

    function draw(e) {
        if (!drawing) return;
        ctx.strokeStyle = '#000';
        ctx.lineWidth = 2;
        ctx.lineCap = 'round';
        ctx.beginPath();
        ctx.moveTo(lastX, lastY);
        ctx.lineTo(e.offsetX, e.offsetY);
        ctx.stroke();
        [lastX, lastY] = [e.offsetX, e.offsetY];
        actions.push(ctx.getImageData(0, 0, canvas.width, canvas.height));
    }

    function stopDrawing() {
        drawing = false;
    }

    function clearCanvas() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        actions = [];
    }

    function undoAction() {
        if (actions.length > 0) {
            ctx.putImageData(actions.pop(), 0, 0);
        }
    }   
        
```

## Installation

To run the whiteboard application locally, follow these steps:

1. Clone this repository: `https://github.com/22pankajsahu/m6weeklytest3.git`
2. Navigate to the project directory: `cd whiteboard`
3. Open `index.html` in your web browser.

## Usage

1. Open the whiteboard application in your web browser.
2. Use your mouse to draw on the canvas.
3. Click the "Delete" button to clear the canvas.
4. Click the "Undo" button to undo the last drawing action.

## Contributing

Contributions are welcome! Here's how you can contribute:

1. Fork the repository.
2. Create a new branch: `git checkout -b feature/new-feature`
3. Make your changes and commit: `git commit -m "Add new feature"`
4. Push to the branch: `git push origin feature/new-feature`
5. Submit a pull request.

## License

This project is licensed under the [MIT License](LICENSE).

## Author

 Name : [PANKAJ SAHU](https://linkedin.com/in/22pankajsahu-) <br>
 Email: [22pankajsahu@gmail.com](mailto:22pankajsahu@gmail.com) <br>
 GitHub: [22pankajsahu](https://github.com/22pankajsahu)
