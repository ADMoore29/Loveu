<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Happy 16 Months, My Love!</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f0e4d7; 
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
      text-align: center;
      color: #4a3728;
    }
    h1 {
      font-size: 24px;
      margin-bottom: 10px;
    }
    #gameArea {
      position: relative;
      width: 90%;
      max-width: 400px;
      height: 300px;
      background-color: #d4c2a7;
      border-radius: 10px;
      overflow: hidden;
    }
    #capybara {
      position: absolute;
      width: 50px;
      cursor: pointer;
      transition: all 0.2s;
    }
    #score {
      font-size: 18px;
      margin: 10px 0;
    }
    #winScreen, #messageScreen, #finalScreen, #responseScreen, #readResponseScreen {
      display: none;
      margin-top: 20px;
      background-color: #fff;
      padding: 15px;
      border-radius: 10px;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
      max-width: 90%;
    }
    button {
      background-color: #8bc34a;
      color: white;
      padding: 10px 20px;
      border: none;
      border-radius: 5px;
      font-size: 16px;
      margin: 5px;
      cursor: pointer;
    }
    button:hover {
      background-color: #689f38;
    }
    p {
      font-size: 14px;
      line-height: 1.5;
    }
    #movingCapybara {
      position: absolute;
      width: 60px;
      animation: moveCapybara 5s linear infinite;
    }
    @keyframes moveCapybara {
      0% { left: -60px; top: 50%; }
      100% { left: 100%; top: 50%; }
    }
    textarea {
      width: 100%;
      height: 100px;
      margin: 10px 0;
      padding: 5px;
      border-radius: 5px;
      border: 1px solid #ccc;
    }
    #responseLink {
      word-break: break-all;
      color: #4a3728;
      font-size: 12px;
    }
  </style>
</head>
<body>
  <h1>Happy 16 Months, My Love! 🦫</h1>
  <p>Play to catch the capybara for a special message!</p>
  <div id="gameArea">
    <img id="capybara" src="https://i.postimg.cc/HkVx1nvV/IMG-20250417-112226.jpg" alt="Capybara">
  </div>
  <p id="score">Score: 0/5</p>
  <div id="winScreen">
    <h2>Congratulations, you won!</h2>
    <button onclick="showMessage()">See Your Message</button>
  </div>
  <div id="messageScreen">
    <p>My Love,<br><br>
    Happy Sweet 16 Months to us.<br>
    Sixteen months of laughter, love, and growing through it all.<br>
    You’ve been my calm in the chaos,<br>
    My favorite hello, and my safest place to land.<br>
    When you gave me that box of chocolates,<br>
    It wasn’t just a gift.<br>
    It was your heart, quietly reminding me<br>
    That I’m loved in all the little ways that matter most.<br>
    You love me softly, truly, and without trying too hard.<br>
    And I hope you feel that from me too,<br>
    In every smile, every hug, every quiet “I’m here.”<br>
    Here’s to more months, more memories,<br>
    And a love that still feels like magic.<br><br>
    Yours, always</p>
    <button onclick="showFinalScreen()">See Your Surprise!</button>
  </div>
  <div id="finalScreen">
    <h2>I love you always 🥰</h2>
    <div style="position: relative; width: 100%; height: 100px;">
      <img id="movingCapybara" src="https://i.postimg.cc/HkVx1nvV/IMG-20250417-112226.jpg" alt="Moving Capybara">
    </div>
    <button onclick="showResponseScreen()">Write a Message for Me!</button>
  </div>
  <div id="responseScreen">
    <h2>Write Your Message 💕</h2>
    <p>Type a sweet message for me to read later!</p>
    <textarea id="responseText" placeholder="Type your message here..."></textarea>
    <button onclick="saveResponse()">Save and Copy Link</button>
    <p id="responseLink"></p>
  </div>
  <div id="readResponseScreen">
    <h2>Your Message to Me 💌</h2>
    <p id="savedResponse">No message yet.</p>
    <button onclick="goBack()">Back to Start</button>
  </div>
  <script>
    let score = 0;
    const capybara = document.getElementById('capybara');
    const scoreDisplay = document.getElementById('score');
    const gameArea = document.getElementById('gameArea');
    const winScreen = document.getElementById('winScreen');

    function moveCapybara() {
      const maxX = gameArea.offsetWidth - capybara.offsetWidth;
      const maxY = gameArea.offsetHeight - capybara.offsetHeight;
      const newX = Math.random() * maxX;
      const newY = Math.random() * maxY;
      capybara.style.left = newX + 'px';
      capybara.style.top = newY + 'px';
    }

    capybara.addEventListener('click', () => {
      score++;
      scoreDisplay.textContent = `Score: ${score}/5`;
      moveCapybara();
      if (score >= 5) {
        gameArea.style.display = 'none';
        scoreDisplay.style.display = 'none';
        winScreen.style.display = 'block';
      }
    });

    setInterval(moveCapybara, 1000);
    moveCapybara();

    function showMessage() {
      winScreen.style.display = 'none';
      document.getElementById('messageScreen').style.display = 'block';
    }

    function showFinalScreen() {
      document.getElementById('messageScreen').style.display = 'none';
      document.getElementById('finalScreen').style.display = 'block';
    }

    function showResponseScreen() {
      document.getElementById('finalScreen').style.display = 'none';
      document.getElementById('responseScreen').style.display = 'block';
    }

    function saveResponse() {
      const responseText = document.getElementById('responseText').value;
      if (responseText.trim() === '') {
        alert('Please write a message before saving!');
        return;
      }
      localStorage.setItem('anniversaryResponse', responseText);
      const encodedResponse = encodeURIComponent(responseText);
      const responseLink = `${window.location.href}?response=${encodedResponse}`;
      document.getElementById('responseLink').innerText = 'Copy this link and send it to me: ' + responseLink;
      alert('Message saved! Please copy the link and send it to me via Messenger so I can read your response.');
    }

    function showResponseScreenFromURL() {
      const urlParams = new URLSearchParams(window.location.search);
      const response = urlParams.get('response');
      if (response) {
        document.getElementById('savedResponse').innerText = decodeURIComponent(response);
        document.getElementById('gameArea').style.display = 'none';
        document.getElementById('score').style.display = 'none';
        document.getElementById('winScreen').style.display = 'none';
        document.getElementById('messageScreen').style.display = 'none';
        document.getElementById('finalScreen').style.display = 'none';
        document.getElementById('responseScreen').style.display = 'none';
        document.getElementById('readResponseScreen').style.display = 'block';
      } else if (localStorage.getItem('anniversaryResponse')) {
        document.getElementById('savedResponse').innerText = localStorage.getItem('anniversaryResponse');
        document.getElementById('gameArea').style.display = 'none';
        document.getElementById('score').style.display = 'none';
        document.getElementById('winScreen').style.display = 'none';
        document.getElementById('messageScreen').style.display = 'none';
        document.getElementById('finalScreen').style.display = 'none';
        document.getElementById('responseScreen').style.display = 'none';
        document.getElementById('readResponseScreen').style.display = 'block';
      }
    }

    function goBack() {
      window.location.href = window.location.pathname;
    }

    // Check if there's a response in the URL or localStorage on page load
    window.onload = function() {
      showResponseScreenFromURL();
    };
  </script>
</body>
</html>
