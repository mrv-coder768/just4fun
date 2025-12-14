import express from "express";
import fetch from "node-fetch";
import cors from "cors";

const app = express();
app.use(cors());
app.use(express.json());

// ✅ PASTE YOUR OPENAI API KEY HERE (KEEP IT SECRET)
const OPENAI_KEY = "PASTE_YOUR_API_KEY_HERE";  // ← Replace with your key

// User system
const users = { admin: "1234", guest: "guest" };

// AI memory
const memory = {};

// LOGIN endpoint
app.post("/login", (req, res) => {
  const { username, password } = req.body;
  if (users[username] === password) {
    res.json({ role: username });
  } else {
    res.status(401).json({ error: "ACCESS DENIED" });
  }
});

// CHATGPT endpoint
app.post("/chat", async (req, res) => {
  const { user, message } = req.body;
  if (!memory[user]) memory[user] = [];
  memory[user].push({ role: "user", content: message });

  try {
    const response = await fetch(
      "https://api.openai.com/v1/chat/completions",
      {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          Authorization: `Bearer ${OPENAI_KEY}`
        },
        body: JSON.stringify({
          model: "gpt-4o-mini",
          messages: [
            { role: "system", content: "You are a cyberpunk AI assistant. Remember user context and respond cool." },
            ...memory[user]
          ]
        })
      }
    );
    const data = await response.json();
    const reply = data.choices[0].message.content;
    memory[user].push({ role: "assistant", content: reply });
    res.json({ reply });
  } catch (e) {
    res.status(500).json({ error: "AI ERROR" });
  }
});

// Start server
app.listen(3000, () =>
  console.log("🔥 Server running at http://localhost:3000")
);
