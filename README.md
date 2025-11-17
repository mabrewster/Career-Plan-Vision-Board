# Career-Plan-Vision-Board
Upload an image and include a caption or statement to match each portion of your career plan to create your Career Plan Vision Board. 
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Career Plan Vision Board</title>
<style>
    body {
        font-family: Arial, sans-serif;
        background-color: #ffffff;
        color: #333;
        margin: 0;
        padding: 0;
    }
    header {
        background-color: #004aad;
        color: #fff;
        padding: 15px;
        text-align: center;
        font-size: 1.5em;
    }
    .container {
        max-width: 800px;
        margin: 20px auto;
        padding: 20px;
        border: 2px solid #004aad;
        border-radius: 8px;
        background-color: #f9f9f9;
    }
    .step {
        display: none;
    }
    .step.active {
        display: block;
    }
    .buttons {
        margin-top: 20px;
        display: flex;
        justify-content: space-between;
    }
    button {
        padding: 10px 15px;
        font-size: 1em;
        border: none;
        border-radius: 5px;
        cursor: pointer;
    }
    .next-btn {
        background-color: #004aad;
        color: #fff;
    }
    .prev-btn {
        background-color: #ffcc00;
        color: #333;
    }
    .help-btn {
        background-color: #ffcc00;
        color: #333;
        float: right;
        margin-top: -40px;
    }
    input[type="file"], textarea {
        width: 100%;
        margin-top: 10px;
    }
    img.preview {
        max-width: 100%;
        margin-top: 10px;
        border: 1px solid #ccc;
        border-radius: 5px;
    }
    /* Help Modal */
    .modal {
        display: none;
        position: fixed;
        top: 0; left: 0;
        width: 100%; height: 100%;
        background: rgba(0,0,0,0.6);
        justify-content: center;
        align-items: center;
    }
    .modal-content {
        background: #fff;
        padding: 20px;
        border-radius: 8px;
        max-width: 500px;
        text-align: center;
    }
    .close {
        float: right;
        cursor: pointer;
        font-size: 1.2em;
        color: #004aad;
    }
</style>
</head>
<body>
<header>Career Plan Vision Board</header>
<div class="container">
    <!-- Help Button -->
    <button class="help-btn" onclick="openHelp()">? Help</button>

    <!-- Steps -->
    <div class="step active" id="step1">
        <h2>Dream Career Image</h2>
        <p>Upload an image that represents your dream career. Add a caption/statement explaining why you chose this image.</p>
        <input type="file" accept="image/*" onchange="previewImage(event, 'preview1')">
        <img id="preview1" class="preview">
        <textarea id="caption1" placeholder="Write your caption here..."></textarea>
    </div>

    <div class="step" id="step2">
        <h2>Skills & Strengths</h2>
        <p>Upload an image that represents your strengths or skills. Add a caption/statement that lists your 1 strength and 2 skills.</p>
        <input type="file" accept="image/*" onchange="previewImage(event, 'preview2')">
        <img id="preview2" class="preview">
        <textarea id="caption2" placeholder="Write your caption here..."></textarea>
    </div>

    <div class="step" id="step3">
        <h2>Education & Training</h2>
        <p>Upload an image that represents the education or training you’ll need. Add a caption/statement explaining your plan.</p>
        <input type="file" accept="image/*" onchange="previewImage(event, 'preview3')">
        <img id="preview3" class="preview">
        <textarea id="caption3" placeholder="Write your caption here..."></textarea>
    </div>

    <div class="step" id="step4">
        <h2>Lifestyle Goals</h2>
        <p>Upload an image that represents the lifestyle you want. Add a caption explaining why this matters to you.</p>
        <input type="file" accept="image/*" onchange="previewImage(event, 'preview4')">
        <img id="preview4" class="preview">
        <textarea id="caption4" placeholder="Write your caption here..."></textarea>
    </div>

    <div class="step" id="step5">
        <h2>Why is this career a good fit?</h2>
        <p>Write a short explanation of why your dream career is a good fit for you.</p>
        <textarea id="caption5" placeholder="Write your explanation here..."></textarea>
        <button onclick="downloadPDF()" style="margin-top:20px;background:#004aad;color:#fff;">Download as PDF</button>
    </div>

    <!-- Navigation -->
    <div class="buttons">
        <button class="prev-btn" onclick="prevStep()">Previous</button>
        <button class="next-btn" onclick="nextStep()">Next</button>
    </div>
</div>

<!-- Help Modal -->
<div class="modal" id="helpModal">
    <div class="modal-content">
        <span class="close" onclick="closeHelp()">&times;</span>
        <h3>How to Complete Your Vision Board</h3>
        <p>1. Upload an image for each section.<br>
           2. Add a caption or explanation.<br>
           3. Navigate using Next/Previous.<br>
           4. On the last page, click "Download as PDF" to save your work.</p>
    </div>
</div>

https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js</script>
https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js</script>
<script>
let currentStep = 1;
const totalSteps = 5;

function showStep(step) {
    document.querySelectorAll('.step').forEach((el, index) => {
        el.classList.toggle('active', index === step - 1);
    });
}

function nextStep() {
    if (currentStep < totalSteps) {
        currentStep++;
        showStep(currentStep);
    }
}

function prevStep() {
    if (currentStep > 1) {
        currentStep--;
        showStep(currentStep);
    }
}

function previewImage(event, id) {
    const img = document.getElementById(id);
    img.src = URL.createObjectURL(event.target.files[0]);
}

function openHelp() {
    document.getElementById('helpModal').style.display = 'flex';
}

function closeHelp() {
    document.getElementById('helpModal').style.display = 'none';
}

async function downloadPDF() {
    const { jsPDF } = window.jspdf;
    const pdf = new jsPDF();
    const steps = document.querySelectorAll('.step');
    for (let i = 0; i < steps.length; i++) {
        steps[i].classList.add('active');
        await html2canvas(steps[i]).then(canvas => {
            const imgData = canvas.toDataURL('image/png');
            const imgWidth = 190;
            const imgHeight = (canvas.height * imgWidth) / canvas.width;
            if (i > 0) pdf.addPage();
            pdf.addImage(imgData, 'PNG', 10, 10, imgWidth, imgHeight);
        });
        steps[i].classList.remove('active');
    }
    pdf.save('Career_Vision_Board.pdf');
}
</script>
</body>
</html>
