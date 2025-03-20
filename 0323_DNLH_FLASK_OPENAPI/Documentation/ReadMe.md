# 📢 Dot Net Learners House Meetup – Monthly Event - Mar 2025

## Date Time: 23-Mar-2025 at 09:00 AM IST



## Event URL: [https://www.meetup.com/dot-net-learners-house-hyderabad/events/304750920](https://www.meetup.com/dot-net-learners-house-hyderabad/events/304750920)

## YouTube URL: [https://www.youtube.com/watch?v=rrZqYt2YDFM](https://www.youtube.com/watch?v=rrZqYt2YDFM)



![Information | 100x100](../Documentation/Images/Information.PNG)

![Seat Belt | 100x100](../Documentation/Images/SeatBelt.PNG)


//ScriptGot it! *Manozgna* will focus *only on the UI, and **Srivalli* will handle the *Flask integration, API calls, and CORS handling. Below are the updated **demo scripts* accordingly.  

---

# *🚀 Session 3: Bringing AI to Life – React, Tailwind, and UI Creation*  
🎙 *Speaker:* Manozgna  
🕘 *9:40 AM - 10:00 AM*  

## *🎯 Goal of the Session:*  
By the end of this session, attendees will:  
✅ Set up a *React + Tailwind CSS* project.  
✅ Build a *fully responsive chat UI*.  
✅ Ensure the UI follows a *modern, clean design* with Tailwind.  

---

## *📝 Demo Script:*

### *1️⃣ Introduction (2 min)*
- "Welcome, everyone! Now that we've built the backend, it’s time to focus on the *frontend experience*."
- "I’ll show you how to create a *beautiful, responsive UI* using *React and Tailwind CSS*."
- "At the end of this session, we’ll have a chat interface ready, and in the next session, Sowmya will integrate it with Flask."

---

### *2️⃣ Setting Up the React Project (4 min)*
- *Create a new project using Vite:*  
  bash
  npm create vite@latest flask-react-aoai-ui --template react-ts
  cd flask-react-aoai-ui
  npm install
  
- *Install Tailwind CSS:*  
  bash
  npm install -D tailwindcss postcss autoprefixer
  npx tailwindcss init -p
  
- **Configure Tailwind in tailwind.config.js:**  
  js
  export default {
    content: ["./index.html", "./src/**/*.{js,ts,jsx,tsx}"],
    theme: {
      extend: {},
    },
  };
  
- **Import Tailwind into index.css:**  
  css
  @import 'tailwindcss/base';
  @import 'tailwindcss/components';
  @import 'tailwindcss/utilities';
  
- "Now we are ready to build our chat UI!"

---

### *3️⃣ Creating the Chat UI (6 min)*
- "Let’s design the main chat component using Tailwind CSS."
- **Create Chat.tsx:**  
  tsx
  import { useState } from "react";

  const Chat: React.FC = () => {
    const [prompt, setPrompt] = useState<string>("");

    return (
      <div className="p-6 w-full max-w-2xl mx-auto space-y-4 font-inter">
        <h2 className="text-2xl font-semibold text-gray-800">Chat with AI 🤖</h2>
        
        <div className="bg-gray-700 text-white p-4 rounded-lg border-l-4 border-blue-500 min-h-[100px] flex items-center justify-center">
          <p className="text-base font-light">Your response will appear here</p>
        </div>

        <textarea
          className="w-full p-3 border rounded-lg shadow-md focus:ring focus:ring-blue-300"
          placeholder="Type your question..."
          value={prompt}
          onChange={(e) => setPrompt(e.target.value)}
        />

        <button
          className="bg-blue-600 text-white px-6 py-2 rounded-lg hover:bg-blue-700 transition"
        >
          🚀 Send
        </button>
      </div>
    );
  };

  export default Chat;
  
- "This gives us a *clean, structured UI*, ready for integration."

---

### *4️⃣ Running the React App & Testing (3 min)*
- *Start the React app:*  
  bash
  npm run dev
  
- "We now have a working UI. Next, Srivalli will integrate this with Flask."

---

### *5️⃣ Wrap-up & Next Steps (1 min)*
- "Now we have a structured UI. In the next session, *Srivalli will connect this UI to Flask and handle API communication.*"
- "Thank you! 🎉"

---

# *🚀 Session 4: Connecting the React UI with Flask API & Handling CORS*  
🎙 *Speaker:* Srivalli  
🕙 *10:00 AM - 10:20 AM*  

## *🎯 Goal of the Session:*  
✅ Connect the *React UI* to the Flask backend.  
✅ Learn how *React sends API requests* to Flask.  
✅ Handle *CORS errors & security*.  

---

## *📝 Demo Script:*

### *1️⃣ Introduction (2 min)*
- "Now that Manozgna has built the UI, let’s integrate it with our Flask API."
- "We’ll focus on making *API calls from React to Flask* and fixing *CORS issues*."
- "By the end of this session, our UI will *send user prompts to Flask and receive AI responses.*"

---

### *2️⃣ Setting Up API Calls in React (6 min)*
- "Instead of handling API calls inside every component, let’s *create a separate API utility*."
- **Create api.ts:**
  tsx
  export const fetchAIResponse = async (prompt: string): Promise<string> => {
    try {
      const res = await fetch("http://127.0.0.1:5009/api/completions", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ prompt }),
      });

      if (!res.ok) {
        throw new Error("Failed to fetch response");
      }

      return await res.text();
    } catch (error) {
      console.error("Error:", error);
      return "⚠ Error fetching response.";
    }
  };
  
- "This makes our API calls *cleaner and reusable*."

---

### **3️⃣ Modifying Chat.tsx to Send Requests (5 min)**
- "Now, let’s modify our UI to fetch responses."
- **Update Chat.tsx:**
  tsx
  import { useState } from "react";
  import { fetchAIResponse } from "./api";

  const Chat: React.FC = () => {
    const [prompt, setPrompt] = useState<string>("");
    const [response, setResponse] = useState<string>("Your response will appear here");

    const sendRequest = async () => {
      setResponse("Thinking... 🤔");
      setResponse(await fetchAIResponse(prompt));
    };

    return (
      <div className="p-6 w-full max-w-2xl mx-auto space-y-4 font-inter">
        <h2 className="text-2xl font-semibold text-gray-800">Chat with AI 🤖</h2>

        <div className="bg-gray-700 text-white p-4 rounded-lg border-l-4 border-blue-500 min-h-[100px] flex items-center">
          <p className="text-base font-light">{response}</p>
        </div>

        <textarea
          className="w-full p-3 border rounded-lg shadow-md focus:ring focus:ring-blue-300"
          placeholder="Type your question..."
          value={prompt}
          onChange={(e) => setPrompt(e.target.value)}
        />

        <button
          onClick={sendRequest}
          className="bg-blue-600 text-white px-6 py-2 rounded-lg hover:bg-blue-700 transition"
        >
          🚀 Send
        </button>
      </div>
    );
  };

  export default Chat;
  
- "Now, our UI can send requests to Flask and display responses!"

---

### *4️⃣ Fixing CORS Issues in Flask (4 min)*
- "If we see *CORS errors*, we need to enable CORS in Flask."
- *Install Flask-CORS:*
  bash
  pip install flask-cors
  
- **Modify app.py:**
  python
  from flask import Flask
  from flask_cors import CORS

  app = Flask(__name__)
  CORS(app)  # Enable CORS globally
  
- "Now, restart Flask, and the UI should work!"

---

### *5️⃣ Wrap-up & Next Steps (2 min)*
- "Now our *React UI communicates with Flask without issues!* 🎉"
- "Swamy will now take over to discuss *.NET Aspire & more tech integrations.*"
- "Thanks for joining!"

---

### 🔹 *Final Thoughts*
- *Manozgna’s session* focused on UI development.  
- *Srivalli’s session* handled API integration, CORS, and structured API calls.  

These changes *perfectly align with the revised agenda!* 🚀 Let me know if you need any refinements.