<!DOCTYPE html>
<html>
<head>
  <title>MKS Hugging Face Chatbot</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(to right, #ffb347, #ffcc33);
      margin: 0; padding: 0;
      display: flex; flex-direction: column;
      align-items: center;
    }
    h1 { margin-top: 20px; color: #333; }
    #chat {
      width: 90%;
      max-width: 600px;
      background: white;
      border-radius: 10px;
      padding: 20px;
      box-shadow: 0 0 10px rgba(0,0,0,0.2);
      overflow-y: auto;
      height: 500px;
      margin-bottom: 20px;
    }
    .message {
      padding: 10px;
      margin: 10px 0;
      border-radius: 8px;
    }
    .user { background-color: #d0f0fd; text-align: right; }
    .bot { background-color: #e1f5c4; text-align: left; }
    #inputArea {
      width: 90%;
      max-width: 600px;
      display: flex;
      gap: 10px;
    }
    input {
      flex: 1;
      padding: 10px;
      font-size: 16px;
    }
    button {
      padding: 10px 20px;
      font-size: 16px;
      background: #4caf50;
      color: white;
      border: none;
      cursor: pointer;
      border-radius: 5px;
    }
  </style>
</head>
<body>

<h1>🤖 MKS Hugging Face Chatbot</h1>

<div id="chat"></div>

<div id="inputArea">
  <input id="userInput" placeholder="Type a message..." />
  <button onclick="send()">Send</button>
</div>

<script>
  const chatBox = document.getElementById("chat");
  const HF_API_TOKEN = "https://api-inference.huggingface.co/models/google/flan-t5-large"; // <--- Replace this

  async function send() {
    const input = document.getElementById("userInput");
    const userMessage = input.value;
    if (!userMessage) return;

    // Add user message to chat
    chatBox.innerHTML += `<div class="message user">${userMessage}</div>`;
    chatBox.scrollTop = chatBox.scrollHeight;
    input.value = "";

    // Add loading message
    chatBox.innerHTML += `<div class="message bot" id="loading">Typing...</div>`;
    chatBox.scrollTop = chatBox.scrollHeight;

    // Send to Hugging Face
    const response = await fetch(
      "https://api-inference.huggingface.co/models/google/flan-t5-large",  // You can change model here
      {
        method: "POST",
        headers: {
          Authorization: `Bearer ${HF_API_TOKEN}`,
          "Content-Type": "application/json"
        },
        body: JSON.stringify({ inputs: userMessage })
      }
    );

    const data = await response.json();
    document.getElementById("loading").remove();

    const botReply = data[0]?.generated_text || "Sorry, I couldn't understand.";
    chatBox.innerHTML += `<div class="message bot">${botReply}</div>`;
    chatBox.scrollTop = chatBox.scrollHeight;
  }
</script>

</body>
</html>
