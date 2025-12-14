<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>instagram: @pythonlearnerr</title>

<style>
    body {
        margin: 0;
        height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
        background: linear-gradient(135deg, #ffdee9, #b5fffc);
        font-family: Arial, sans-serif;
    }

    .container {
        width: 90vw;
        max-width: 400px;
        height: 90vw;
        max-height: 400px;
        background: white;
        border-radius: 18px;
        box-shadow: 0 10px 25px rgba(0,0,0,0.25);
        position: relative;
        text-align: center;
        padding-top: 30px;
        overflow: hidden;
    }

    h2 {
        font-size: 1.5rem;
        margin-bottom: 35px;
    }

    button {
        padding: 12px 28px;
        font-size: 1rem;
        border: none;
        border-radius: 25px;
        cursor: pointer;
    }

    #yes {
        background-color: #4CAF50;
        color: white;
    }

    #no {
        background-color: #f44336;
        color: white;
        position: absolute;
        left: 50%;
        top: 65%;
        transform: translate(-50%, -50%);
        touch-action: none;
    }

    /* Popup */
    .popup {
        display: none;
        position: fixed;
        inset: 0;
        background: rgba(0,0,0,0.5);
        justify-content: center;
        align-items: center;
        z-index: 100;
    }

    .popup-box {
        background: white;
        padding: 22px;
        border-radius: 18px;
        width: 80%;
        max-width: 300px;
        text-align: center;
    }

    .popup-box p {
        font-size: 1.1rem;
    }

    .popup-box button {
        margin-top: 18px;
        background: #4CAF50;
        color: white;
        width: 100%;
    }
</style>
</head>

<body>

<div class="container" id="container">
    <h2>Are you pig? 🐷</h2>
    <button id="yes" onclick="showPopup()">Yes</button>
    <button id="no">No</button>
</div>

<div class="popup" id="popup">
    <div class="popup-box">
        <p>Thanks for Accepting 🤣</p>
        <button onclick="closePopup()">OK</button>
    </div>
</div>

<script>
    const noBtn = document.getElementById("no");
    const container = document.getElementById("container");

    function vibrate(pattern) {
        if (navigator.vibrate) {
            navigator.vibrate(pattern);
        }
    }

    function moveButton(e) {
        e.preventDefault();

        // Short vibration when NO is touched
        vibrate(120);

        const maxX = container.clientWidth - noBtn.offsetWidth;
        const maxY = container.clientHeight - noBtn.offsetHeight;

        const x = Math.random() * maxX;
        const y = Math.random() * maxY;

        noBtn.style.left = x + "px";
        noBtn.style.top = y + "px";
        noBtn.style.transform = "none";
    }

    // Desktop
    noBtn.addEventListener("mouseover", moveButton);

    // Mobile
    noBtn.addEventListener("touchstart", moveButton);
    noBtn.addEventListener("touchmove", moveButton);

    function showPopup() {
        // Happy vibration pattern
        vibrate([100, 60, 100, 60, 200]);
        document.getElementById("popup").style.display = "flex";
    }

    function closePopup() {
        document.getElementById("popup").style.display = "none";
    }
</script>

</body>
</html>
