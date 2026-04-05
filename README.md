# AI-Learning-Application

import { useState } from "react";

function App() {
  const [content, setContent] = useState("Welcome! Let's learn 🎨");

  const [chatOpen, setChatOpen] = useState(false);
  const [messages, setMessages] = useState([]);
  const [input, setInput] = useState("");

  const handleLearning = (topic) => {
    if (topic === "animals") {
      setContent("🐶 Dog 🐱 Cat 🐼 Panda 🦁 Lion");
    } else if (topic === "cars") {
      setContent("🚗 Car 🏎️ Race Car 🚙 SUV");
    } else {
      setContent("🌈 Colors, Shapes, Numbers!");
    }
  };

  const sendMessage = () => {
    if (!input) return;

    let reply = "Let me help you learn 😊";

    const msg = input.toLowerCase();

    if (msg.includes("animal")) {
      reply = "Animals are living beings like dogs 🐶 and cats 🐱";
    } else if (msg.includes("car")) {
      reply = "Cars are vehicles used for transport 🚗";
    }

    setMessages([
      ...messages,
      { text: input, sender: "user" },
      { text: reply, sender: "bot" }
    ]);

    setInput("");
  };

  return (
    <div style={{
      height: "100vh",
      background: "linear-gradient(to right, #ffecd2, #fcb69f)",
      textAlign: "center",
      padding: "20px"
    }}>

      {/* MAIN LEARNING AREA */}
      <h1>🧸 Fun Learning App</h1>

      <h2>{content}</h2>

      <div style={{ fontSize: "60px", margin: "20px" }}>
        🐶 🐱 🐼 🚗 🎈 🌈
      </div>

      <button onClick={() => handleLearning("animals")}
        style={{ margin: "10px", padding: "10px", borderRadius: "10px" }}>
        Learn Animals
      </button>

      <button onClick={() => handleLearning("cars")}
        style={{ margin: "10px", padding: "10px", borderRadius: "10px" }}>
        Learn Vehicles
      </button>

      {/* FLOATING CHAT BUTTON */}
      <div
        onClick={() => setChatOpen(!chatOpen)}
        style={{
          position: "fixed",
          bottom: "20px",
          right: "20px",
          backgroundColor: "#ff6f61",
          color: "white",
          padding: "15px",
          borderRadius: "50%",
          cursor: "pointer",
          fontSize: "20px"
        }}
      >
        🤖
      </div>

      {/* CHATBOX */}
      {chatOpen && (
        <div style={{
          position: "fixed",
          bottom: "80px",
          right: "20px",
          width: "250px",
          background: "white",
          borderRadius: "15px",
          boxShadow: "0px 0px 10px rgba(0,0,0,0.2)",
          display: "flex",
          flexDirection: "column"
        }}>

          <div style={{
            background: "#ff6f61",
            color: "white",
            padding: "10px",
            borderTopLeftRadius: "15px",
            borderTopRightRadius: "15px"
          }}>
            🤖 Help Bot
          </div>

          <div style={{
            height: "150px",
            overflowY: "auto",
            padding: "10px"
          }}>
            {messages.map((msg, i) => (
              <div key={i} style={{
                textAlign: msg.sender === "user" ? "right" : "left",
                margin: "5px"
              }}>
                <span style={{
                  background: msg.sender === "user" ? "#ff6f61" : "#ddd",
                  padding: "5px",
                  borderRadius: "10px"
                }}>
                  {msg.text}
                </span>
              </div>
            ))}
          </div>

          <div style={{ display: "flex", padding: "5px" }}>
            <input
              value={input}
              onChange={(e) => setInput(e.target.value)}
              style={{
                flex: 1,
                padding: "5px",
                borderRadius: "10px",
                border: "none"
              }}
              placeholder="Ask..."
            />

            <button onClick={sendMessage}
              style={{
                marginLeft: "5px",
                borderRadius: "10px",
                border: "none",
                background: "#ff6f61",
                color: "white"
              }}>
              ➤
            </button>
          </div>

        </div>
      )}

    </div>
  );
}

export default App;
