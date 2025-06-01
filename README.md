<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Madhur's AI Chatbot</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(135deg, orange, yellow);
      color: #333;
      margin: 0;
      padding: 0;
      display: flex;
      flex-direction: column;
      align-items: center;
      height: 100vh;
    }
    h1 {
      background-color: #fff3cd;
      color: #856404;
      padding: 1rem 2rem;
      border-radius: 10px;
      margin-top: 1rem;
      box-shadow: 0 0 10px rgba(0,0,0,0.2);
    }
    #chat {
      width: 90%;
      max-width: 600px;
      height: 60vh;
      background-color: white;
      border-radius: 10px;
      padding: 1rem;
      overflow-y: auto;
      margin: 1rem 0;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    .user, .bot {
      margin-bottom: 1rem;
      padding: 0.5rem;
      border-radius: 5px;
    }
    .user {
      background-color: #d1e7dd;
    }
    .bot {
      background-color: #f8d7da;
    }
    input {
      width: 80%;
      padding: 0.5rem;
      margin: 0.5rem;
      border-radius: 5px;
      border: 1px solid #ccc;
    }
    button {
      padding: 0.5rem 1rem;
      background-color: #4CAF50;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    button:hover {
      background-color: #45a049;
    }
  </style>
</head>
<body>
  <h1>Madhur's AI Chatbot 🤖</h1>
  <div id="chat"></div>
  <input type="text" id="userInput" placeholder="Apna sawal likho...">
  <button onclick="askBot()">Send</button>  <script>
    const HF_API_TOKEN = ""; // <-- Yahan Hugging Face ka token daalo

    async function askBot() {
      const userMessage = document.getElementById("userInput").value;
      if (!userMessage) return;

      document.getElementById("chat").innerHTML += `<div class='user'>👤: ${userMessage}</div>`;
      document.getElementById("userInput").value = "";

      const response = await fetch(
        "https://api-inference.huggingface.co/models/facebook/blenderbot-3B",
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
      const botReply = data.generated_text || "Sorry, couldn't understand.";

      document.getElementById("chat").innerHTML += `<div class='bot'>🤖: ${botReply}</div>`;
    }
  </script></body>
</html>
