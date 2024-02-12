---
toc: false
comments: false
layout: default
---

<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Gray Boxes</title>
<style>
    body {
        margin: 0;
        padding: 0;
        height: 100vh;
        background-image: url('https://wallpapers.com/images/hd/plain-black-background-02fh7564l8qq4m6d.jpg');
        background-size: cover; /* Cover the entire background */
        background-position: center; /* Center the background image */
        display: flex;
        flex-direction: column; /* Change to column layout */
        justify-content: center; /* Center content vertically */
        align-items: center; /* Center content horizontally */
        margin-top: 5px;
    }
    .container {
        display: grid;
        grid-template-columns: repeat(7, 75px); /* Adjust box width */
        grid-template-rows: repeat(7, 75px); /* Adjust box height */
        gap: 5px; /* Smaller gap between boxes */
    }
    .whitebox {
        position: relative;
        background-color: white; /* Light gray */
        width: 75px; /* Adjust box width */
        height: 75px; /* Adjust box height */
        font-size: 20px; /* Make font size bigger */
        color: black; /* Set text color to black */
    }
    .number {
        position: absolute;
        top: 5px;
        left: 5px;
    }
    .letter {
        display: flex;
        justify-content: center;
        align-items: center;
        width: 100%;
        height: 100%;
    }
    .blackbox {
        background-color: black; /* Light gray */
        width: 75px; /* Adjust box width */
        height: 75px; /* Adjust box height */
    }
    #game-container {
        display: flex;
        flex-direction: column;
        align-items: center;
        margin-top: 20px; /* Adjust the top margin as needed */
    }
</style>
</head>
<body>

<div id="game-container">
    <div class="container">
        <!-- 81 white and black boxes -->
        <div class="whitebox"><span class="number">1</span><span class="letter">S</span></div>
        <div class="whitebox"><span class="number"></span><span class="letter">A</span></div>
        <div class="whitebox"><span class="number">2</span><span class="letter">F</span></div>
        <div class="whitebox"><span class="number"></span><span class="letter">E</span></div>
        <div class="whitebox"><span class="number">3</span><span class="letter">R</span></div>
        <div class="blackbox"></div>
        <div class="whitebox"><span class="number">4</span><span class="letter">A</span></div>
        <div class="whitebox"><span class="number"></span><span class="letter">E</span></div>
        <div class="blackbox"></div>
        <div class="whitebox"><span class="number"></span><span class="letter">L</span></div>
        <div class="blackbox"></div>
        <div class="whitebox"><span class="number">5</span><span class="letter">O</span></div>
        <div class="whitebox"><span class="number"></span><span class="letter">L</span></div>
        <div class="whitebox"><span class="number"></span><span class="letter">D</span></div>
        <div class="whitebox"><span class="number">6</span><span class="letter">A</span></div>
        <div class="whitebox"><span class="number"></span><span class="letter">M</span></div>
        <div class="whitebox"><span class="number"></span><span class="letter">U</span></div>
        <div class="whitebox"><span class="number"></span><span class="letter">S</span></div>
        <div class="whitebox"><span class="number"></span><span class="letter">E</span></div>
        <div class="blackbox"></div>
        <div class="whitebox"><span class="number"></span><span class="letter">O</span></div>
        <div class="whitebox"><span class="number"></span><span class="letter"></span></div>
        <div class="blackbox"></div>
        <div class="blackbox"></div>
        <div class="whitebox"><span class="number"></span><span class="letter"></span></div>
        <div class="blackbox"></div>
        <div class="blackbox"></div>
        <div class="whitebox"><span class="number"></span><span class="letter"></span></div>
        <div class="whitebox"><span class="number"></span><span class="letter"></span></div>
        <div class="blackbox"><span class="number"></span><span class="letter"></span></div>
        <div class="whitebox"><span class="number"></span><span class="letter"></span></div>
        <div class="whitebox"><span class="number"></span><span class="letter"></span></div>
        <div class="whitebox"><span class="number"></span><span class="letter"></span></div>
        <div class="whitebox"><span class="number"></span><span class="letter"></span></div>
        <div class="whitebox"><span class="number"></span><span class="letter"></span></div>
        <div class="whitebox"><span class="number"></span><span class="letter"></span></div>
        <div class="whitebox"><span class="number"></span><span class="letter"></span></div>
        <div class="whitebox"><span class="number"></span><span class="letter"></span></div>
        <div class="blackbox"></div>
        <div class="whitebox"><span class="number"></span><span class="letter"></span></div>
        <div class="blackbox"><span class="number"></span><span class="letter"></span></div>
        <div class="whitebox"><span class="number"></span><span class="letter"></span></div>
        <div class="whitebox"><span class="number"></span><span class="letter"></span></div>    
        <div class="blackbox"><span class="number"></span><span class="letter"></span></div>
        <div class="whitebox"><span class="number"></span><span class="letter"></span></div>
        <div class="whitebox"><span class="number"></span><span class="letter"></span></div>
        <div class="whitebox"><span class="number"></span><span class="letter"></span></div>
        <div class="whitebox"><span class="number"></span><span class="letter"></span></div>
        <div class="whitebox"><span class="number"></span><span class="letter"></span></div>    
    </div>
</div>

</body>
</html>
