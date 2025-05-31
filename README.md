<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>MKS AI Chatbot</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(to right, #ffecd2, #fcb69f);
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }
    .chat-container {
      background: white;
      padding: 20px;
      width: 400px;
      max-height: 80vh;
      border-radius: 10px;
      box-shadow: 0 0 20px rgba(0,0,0,0.2);
      overflow-y: auto;
    }
    .message {
      margin: 10px 0;
    }
    .user {
      text-align: right;
      color: #2e8b57;
    }
    .bot {
      text-align: left;
      color: #555;
    }
    input {
      width: 80%;
      padding: 10px;
      margin-top: 10px;
      border-radius: 5px;
      border: 1px solid #ccc;
    }
    button {
      padding: 10px;
      border: none;
      background: #ff7f50;
      color: white;
      border-radius: 5px;
      cursor: pointer;
    }
  </style>
</head>
<body>

<div class="chat-container" id="chat">
  <div class="message bot">Hi! I'm your study buddy AI. Ask me anything! 😄</div>
</div>
<div style="position: absolute; bottom: 30px;">
  <input type="text" id="userInput" placeholder="Type your message...">
  <button onclick="sendMessage()">Send</button>
</div>

<script>
  function sendMessage() {
    const userText = document.getElementById('userInput').value;
    if (!userText.trim()) return;

    const chat = document.getElementById('chat');
    chat.innerHTML += `<div class="message user">${userText}</div>`;

    // Basic logic like AI
    let botReply = "I didn't understand that. Can you rephrase?";
    if (userText.toLowerCase().includes("hello") || userText.toLowerCase().includes("hi")) {
      botReply = "Hello! How can I help you today? 😊";
    } else if (userText.toLowerCase().includes("who are you")) {
      botReply = "I'm MKS AI, your smart assistant created by Madhur!";
    } else if (userText.toLowerCase().includes("study tips")) {
      botReply = "Tip: Focus on one subject at a time and take short breaks.";
    } else if (userText.toLowerCase().includes("thank")) {
      botReply = "You're welcome! 💙";
    } else if (userText.toLowerCase().includes("bye")) {
      botReply = "Goodbye! Come back soon.";
    }

    setTimeout(() => {
      chat.innerHTML += `<div class="message bot">${botReply}</div>`;
      chat.scrollTop = chat.scrollHeight;
    }, 500);

    document.getElementById('userInput').value = '';
  }
</script>

</body>
</html>
