import React, { useState } from "react";
import { Send } from "lucide-react";

export default function CampusAssist() {
  const [messages, setMessages] = useState([]);
  const [input, setInput] = useState("");

  const handleSend = () => {
    if (!input.trim()) return;
    setMessages([...messages, { sender: "user", text: input }]);
    setInput("");
    // You can add API call logic here to get AI response
  };

  const sampleQuestions = [
    "What are the library hours?",
    "Where can I find the dining hall menu?",
    "How do I register for classes?",
    "Tell me about the gym facilities.",
  ];

  const handleSampleClick = (question) => {
    setMessages([...messages, { sender: "user", text: question }]);
  };

  return (
    <div className="flex flex-col items-center justify-center min-h-screen bg-gray-50">
      {/* Logo */}
      <h1 className="text-2xl font-semibold text-blue-600 flex items-center gap-2 mb-6">
        🎓 CampusAssist AI
      </h1>

      {/* Chat window */}
      <div className="bg-white w-full max-w-lg rounded-2xl shadow p-6">
        <p className="text-center text-gray-600 mb-4">
          Or try one of these sample questions:
        </p>

        {/* Sample question buttons */}
        <div className="grid grid-cols-2 gap-3 mb-6">
          {sampleQuestions.map((q, i) => (
            <button
              key={i}
              onClick={() => handleSampleClick(q)}
              className="px-4 py-2 bg-gray-100 rounded-lg hover:bg-blue-100 text-gray-800 text-sm"
            >
              {q}
            </button>
          ))}
        </div>

        {/* Messages display */}
        <div className="h-40 overflow-y-auto border rounded-lg p-3 mb-4 bg-gray-50">
          {messages.length === 0 ? (
            <p className="text-gray-400 text-center text-sm">
              Ask about schedules, dining, library hours...
            </p>
          ) : (
            messages.map((m, i) => (
              <div
                key={i}
                className={`mb-2 ${
                  m.sender === "user" ? "text-blue-600" : "text-gray-700"
                }`}
              >
                <strong>{m.sender === "user" ? "You: " : "AI: "}</strong>
                {m.text}
              </div>
            ))
          )}
        </div>

        {/* Input box */}
        <div className="flex items-center gap-2">
          <input
            type="text"
            placeholder="Ask about schedules, dining, library hours..."
            className="flex-1 border rounded-lg px-3 py-2 text-sm focus:outline-none focus:ring-2 focus:ring-blue-400"
            value={input}
            onChange={(e) => setInput(e.target.value)}
            onKeyDown={(e) => e.key === "Enter" && handleSend()}
          />
          <button
            onClick={handleSend}
            className="bg-blue-500 hover:bg-blue-600 text-white p-2 rounded-lg"
          >
            <Send size={18} />
          </button>
        </div>
      </div>
    </div>
  );
}
