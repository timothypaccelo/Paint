<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Paint Application</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css"></link>
    <style>
        #canvas {
            border: 1px solid #000;
        }
    </style>
</head>
<body class="bg-gray-100 flex flex-col items-center justify-center min-h-screen">
    <div class="bg-white p-4 rounded shadow-md w-full max-w-4xl">
          <h1 class="text-2xl font-bold mb-4 text-center">Paint Application</h1>
        <div class="flex justify-between items-center mb-4">
            <div class="flex space-x-2">
                <script type="text/javascript">
	atOptions = {
		'key' : '7d4176d136644cfba14163b2341da453',
		'format' : 'iframe',
		'height' : 60,
		'width' : 468,
		'params' : {}
	};
</script>
<script type="text/javascript" src="//www.highperformanceformat.com/7d4176d136644cfba14163b2341da453/invoke.js"></script>
                <input type="color" id="colorPicker" class="border rounded p-1">
                <select id="brushSize" class="border rounded p-1">
                    <option value="2">2px</option>
                    <option value="4">4px</option>
                    <option value="6">6px</option>
                    <option value="8">8px</option>
                    <option value="10">10px</option>
                </select>
                <button id="erase" class="bg-gray-500
                text-white px-4 py-2 rounded"><i class="fas fa-eraser"></i></button>
            </div>
            <div>
                <script type="text/javascript">
	atOptions = {
		'key' : '6d96ea590ab4de884787b6c34a6cef06',
		'format' : 'iframe',
		'height' : 250,
		'width' : 300,
		'params' : {}
	};
</script>
<script type="text/javascript" src="//www.highperformanceformat.com/6d96ea590ab4de884787b6c34a6cef06/invoke.js"></script>
            </div>
        </div>
        <div class="flex justify-center">
            <canvas id="canvas" width="800" height="600" class="bg-white"></canvas>
        </div>
    </div>


<script>
        const canvas = document.getElementById('canvas');
        const ctx = canvas.getContext('2d');
        const clearButton = document.getElementById('clear');
        const colorPicker = document.getElementById('colorPicker');
        const brushSize = document.getElementById('brushSize');
        const saveButton = document.getElementById('save');
        const eraseButton = document.getElementById('erase');

         let painting = false;
        let color = '#000000';
        let lineWidth = 2;
        let erasing = false;

    canvas.addEventListener('mousedown', startPosition);
        canvas.addEventListener('mouseup', endPosition);
        canvas.addEventListener('mousemove', draw);

      canvas.addEventListener('touchstart', startTouch, false);
        canvas.addEventListener('touchend', endTouch, false);
        canvas.addEventListener('touchmove', drawTouch, false);

       clearButton.addEventListener('click', clearCanvas);
        colorPicker.addEventListener('input', changeColor);
        brushSize.addEventListener('change', changeBrushSize);
        saveButton.addEventListener('click', saveCanvas);
        eraseButton.addEventListener('click', toggleEraser);

       function startPosition(e) {
            painting = true;
            draw(e);
        }

        function endPosition() {
            painting = false;
            ctx.beginPath();
        }

        function draw(e) {
            if (!painting) return;

            const rect = canvas.getBoundingClientRect();
            const x = e.clientX - rect.left;
            const y = e.clientY - rect.top;

            ctx.lineWidth = lineWidth;
            ctx.lineCap = 'round';
            ctx.strokeStyle = erasing ? '#FFFFFF' : color;

            ctx.lineTo(x, y);
            ctx.stroke();
            ctx.beginPath();
            ctx.moveTo(x, y);
        }

        function startTouch(e) {
            e.preventDefault();
            painting = true;
            drawTouch(e);
        }

        function endTouch(e) {
            e.preventDefault();
            painting = false;
            ctx.beginPath();
        }

        function drawTouch(e) {
            e.preventDefault();
            if (!painting) return;

            const rect = canvas.getBoundingClientRect();
            const touch = e.touches[0];
            const x = touch.clientX - rect.left;
            const y = touch.clientY - rect.top;

           ctx.lineWidth = lineWidth;
            ctx.lineCap = 'round';
            ctx.strokeStyle = erasing ? '#FFFFFF' : color;

            ctx.lineTo(x, y);
            ctx.stroke();
            ctx.beginPath();
            ctx.moveTo(x, y);
        }

        function clearCanvas() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
        }

        function changeColor(e) {
            color = e.target.value;
            erasing = false;
        }

        function changeBrushSize(e) {
            lineWidth = e.target.value;
        }

        function toggleEraser() {
            erasing = !erasing;
        }
       
       function saveCanvas() {
            const link = document.createElement('a');
            link.download = 'painting.png';
            link.href = canvas.toDataURL();
            link.click();
        }
    </script>
</body>
</html>
        
