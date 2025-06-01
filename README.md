<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>AI Chatbot (Hugging Face)</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(to right, #ff9900, #ffff66);
      margin: 0;
      padding: 0;
      display: flex;
      flex-direction: column;
      height: 100vh;
    }
    h1 {
      text-align: center;
      background-color: #333;
      color: white;
      margin: 0;
      padding: 1rem;
    }
    #chat {
      flex: 1;
      padding: 1rem;
      overflow-y: auto;
      background: #f4f4f4;
    }
    .message {
      padding: 0.5rem;
      margin: 0.5rem 0;
      border-radius: 10px;
      max-width: 70%;
    }
    .user {
      background-color: #d1ffd6;
      align-self: flex-end;
      text-align: right;
    }
    .bot {
      background-color: #d6eaff;
      align-self: flex-start;
      text-align: left;
    }
    #inputForm {
      display: flex;
      padding: 1rem;
      background: #fff;
    }
    #input {
      flex: 1;
      padding: 0.5rem;
      font-size: 1rem;
    }
    button {
      padding: 0.5rem 1rem;
      background-color: #333;
      color: white;
      border: none;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <h1>Madhur's AI Chatbot 🤖</h1>
  <div id="chat"></div>
  <form id="inputForm">
    <input type="text" id="input" placeholder="Ask something..." required />
    <button type="submit">Send</button>
  </form>

  <script>
    const chat = document.getElementById("chat");
    const inputForm = document.getElementById("inputForm");
    const input = document.getElementById("input");

    const HF_API_TOKEN = "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"; // <== Yahan token daalo
    const MODEL = "facebook/blenderbot-3B"; // ya "microsoft/DialoGPT-medium"

    inputForm.addEventListener("submit", async (e) => {
      e.preventDefault();
      const userMessage = input.value.trim();
      if (!userMessage) return;

      addMessage(userMessage, "user");
      input.value = "";

      addMessage("Typing...", "bot");
      const botResponse = await queryModel(userMessage);
      chat.lastChild.textContent = botResponse;
    });

    function addMessage(text, sender) {
      const message = document.createElement("div");
      message.classList.add("message", sender);
      message.textContent = text;
      chat.appendChild(message);
      chat.scrollTop = chat.scrollHeight;
    }

    async function queryModel(prompt) {
      try {
        const response = await fetch(`https://api-inference.huggingface.co/models/${MODEL}`, {
          method: "POST",
          headers: {
            Authorization: `Bearer ${HF_API_TOKEN}`,
            "Content-Type": "application/json",
          },
          body: JSON.stringify({ inputs: prompt }),
        });

        const result = await response.json();
        if (result.generated_text) {
          return result.generated_text;
        } else if (result[0]?.generated_text) {
          return result[0].generated_text;
        } else if (result.error) {
          return "⚠️ Error: " + result.error;
        } else {
          return "❌ Sorry, no response.";
        }
      } catch (error) {
        return "⚠️ Connection failed.";
      }
    }
  </script>
</body>
</html>
