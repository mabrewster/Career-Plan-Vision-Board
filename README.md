# Career-Plan-Vision-Board
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Career Vision Board</title>
<style>
    body {
        font-family: Arial, sans-serif;
        background: #fff;
        color: #333;
        margin: 0;
        padding: 0;
    }
    .container {
        max-width: 900px;
        margin: auto;
        padding: 20px;
        text-align: center;
    }
    h1 {
        color: #004aad;
    }
    .progress-bar {
        width: 100%;
        background: #ddd;
        height: 20px;
        width: 0%;
        background: #ffd700;
        transition: width 0.3s ease;
    }
    .step {
        display: none;
    }
    .active {
        display: block;
    }
    input[type="text"], textarea {
        width: 80%;
        padding: 10px;
        margin: 10px 0;
        border: 2px solid #004aad;
        border-radius: 5px;
    }
    button {
        background: #ffd700;
        color: #004aad;
        border: none;
        padding: 10px 20px;
        margin: 10px;
        font-size: 16px;
        cursor: pointer;
        border-radius: 5px;
    }
    #vision-board {
        display: none;
        border: 3px solid #004aad;
        padding: 20px;
        margin-top: 20px;
        background: #f9f9f9;
    }
    .collage {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
        gap: 15px;
        margin-top: 20px;
    }
    .collage-item {
        text-align: center;
    }
    .collage-item img {
        width: 150px;
        height: 150px;
        object-fit: cover;
        border-radius: 8px;
        display: block;
        margin: auto;
    }
    .collage-item p {
        margin-top: 8px;
        font-weight: bold;
        color: #004aad;
    }
</style>
</head>
<body>
<div class="container">
    <h1>Career Planning Vision Board</h1>
    <div class="progress-bar"><div class="progress" id="progress"></div></div>
    <div id="steps">
        <!-- Step 1 -->
        <div class="step active" id="step1">
            <h2>Step 1: Upload Your Photo & Caption</h2>
            <input type="file" id="photo1" accept="image/*"><br>
            <input type="text" id="caption1" placeholder="Enter caption for this photo">
            <button onclick="nextStep()">Next</button>
        </div>
        <!-- Step 2 -->
        <div class="step" id="step2">
            <h2>Step 2: Upload Photo & Caption</h2>
            <input type="file" id="photo2" accept="image/*"><br>
            <input type="text" id="caption2" placeholder="Enter caption for this photo">
            <button onclick="prevStep()">Back</button>
            <button onclick="nextStep()">Next</button>
        </div>
        <!-- Step 3 -->
        <div class="step" id="step3">
            <h2>Step 3: Upload Photo & Caption</h2>
            <input type="file" id="photo3" accept="image/*"><br>
            <input type="text" id="caption3" placeholder="Enter caption for this photo">
            <button onclick="prevStep()">Back</button>
            <button onclick="nextStep()">Next</button>
        </div>
        <!-- Step 4 -->
        <div class="step" id="step4">
            <h2>Step 4: Upload Photo & Caption</h2>
            <input type="file" id="photo4" accept="image/*"><br>
            <input type="text" id="caption4" placeholder="Enter caption for this photo">
            <button onclick="prevStep()">Back</button>
            <button onclick="nextStep()">Next</button>
        </div>
        <!-- Step 5 -->
        <div class="step" id="step5">
            <h2>Step 5: Upload Photo & Caption</h2>
            <input type="file" id="photo5" accept="image/*"><br>
            <input type="text" id="caption5" placeholder="Enter caption for this photo">
            <button onclick="prevStep()">Back</button>
            <button onclick="generateBoard()">Finish</button>
        </div>
    </div>

    <!-- Vision Board Display -->
    <div id="vision-board">
        <h2>Your Vision Board</h2>
        <div class="collage" id="images"></div>
        <button onclick="takeScreenshot()">Download Screenshot</button>
        <button onclick="resetBoard()">Start Over</button>
    </div>
</div>

<script/cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js</script>
<script>
let currentStep = 1;
const totalSteps = 5;

function updateProgress() {
    document.getElementById('progress').style.width = ((currentStep-1)/totalSteps)*100 + '%';
}

function nextStep() {
    document.getElementById(`step${currentStep}`).classList.remove('active');
    currentStep++;
    document.getElementById(`step${currentStep}`).classList.add('active');
    updateProgress();
}

function prevStep() {
    document.getElementById(`step${currentStep}`).classList.remove('active');
    currentStep--;
    document.getElementById(`step${currentStep}`).classList.add('active');
    updateProgress();
}

function generateBoard() {
    document.getElementById('steps').style.display = 'none';
    document.getElementById('vision-board').style.display = 'block';

    let imageContainer = document.getElementById('images');
    imageContainer.innerHTML = '';
    for (let i = 1; i <= 5; i++) {
        let fileInput = document.getElementById(`photo${i}`);
        let captionText = document.getElementById(`caption${i}`).value;
        if (fileInput.files[0]) {
            let wrapper = document.createElement('div');
            wrapper.classList.add('collage-item');
            let img = document.createElement('img');
            img.src = URL.createObjectURL(fileInput.files[0]);
            let caption = document.createElement('p');
            caption.innerText = captionText;
            wrapper.appendChild(img);
            wrapper.appendChild(caption);
            imageContainer.appendChild(wrapper);
        }
    }
}

function takeScreenshot() {
    html2canvas(document.querySelector("#vision-board")).then(canvas => {
        let link = document.createElement('a');
        link.download = 'vision-board.png';
        link.href = canvas.toDataURL();
        link.click();
    });
}

function resetBoard() {
    location.reload();
}

updateProgress();
</script>
</body>
</html>
