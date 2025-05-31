<!DOCTYPE html>
<html>
<head>
  <title>Local Chatbot</title>
  <style>
    body { font-family: sans-serif; margin: 20px; }
    #chat { max-width: 600px; margin: auto; }
    .msg { padding: 10px; margin: 5px; border-radius: 5px; }
    .user { background: #ffd54f; text-align: right; }
    .bot { background: #c8e6c9; text-align: left; }
  </style>
</head>
<body>
  <h2>🤖 MKS Local AI</h2>
  <div id="chat"></div>
  <input id="userInput" placeholder="Type a message..." />
  <button onclick="send()">Send</button>

  <script>
    function fakeAIReply(msg) {
      msg = msg.toLowerCase();
      if (msg.includes("hi") || msg.includes("hello")) return "Hello! How can I help you?";
      if (msg.includes("name")) return "My name is MKS AI 😎";
      if (msg.includes("math")) return "Math is the language of the universe!";
      if (msg.includes("bye")) return "Goodbye! Study well!";
      return "Sorry, I didn't understand that. Try something else.";
    }

    function send() {
      const input = document.getElementById("userInput");
      const userMsg = input.value;
      if (!userMsg) return;
      
      const chat = document.getElementById("chat");
      chat.innerHTML += `<div class='msg user'>${userMsg}</div>`;
      
      const botReply = fakeAIReply(userMsg);
      setTimeout(() => {
        chat.innerHTML += `<div class='msg bot'>${botReply}</div>`;
      }, 500);
      
      input.value = "";
    }
  </script>
</body>
</html>
