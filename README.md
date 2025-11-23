💘 OpenHeart: The Free Dating App Simulation

OpenHeart is a fully functional, single-player dating app prototype built with React. It operates in "Simulation Mode," allowing users to experience the full flow of a modern dating app—swiping, matching, and chatting—without the need for a live backend or active user base.

It was designed with a "Free Forever" philosophy, showcasing a premium UI/UX without paywalls.

✨ Features

🃏 Interactive Deck: Smooth, physics-based card swiping interface (Right to Like, Left to Pass).

🤖 Simulation Engine:

Pre-loaded with diverse, realistic mock profiles.

Randomized matching algorithm (approx. 40% match rate).

Matches simulate activity by sending initial greetings.

💬 Chat System: Fully functional chat UI where "matches" reply to your messages using randomized, context-aware responses with realistic typing delays.

📱 Responsive Design: Built mobile-first but includes a desktop wrapper that simulates a mobile device frame.

💎 Premium UI: A polished aesthetic using gold gradients and high-quality iconography to mimic a premium unlocked experience.

🚀 Getting Started

This project is built using standard React tooling.

Prerequisites

Node.js (v14 or higher)

npm or yarn

Installation

Clone the repository

git clone [https://github.com/yourusername/openheart.git](https://github.com/yourusername/openheart.git)
cd openheart


Install dependencies

npm install
# or
yarn install


Install required icons
This project uses lucide-react. If not installed automatically:

npm install lucide-react


Start the development server

npm start
# or
yarn start


🛠️ Tech Stack

Frontend Framework: React (Hooks: useState, useEffect, useRef)

Styling: Tailwind CSS (for layout, typography, and animations)

Icons: Lucide React

Assets: Unsplash (for demo profile images)

🧩 How It Works

The Data Model

The app uses a static array of objects (MOCK_PROFILES) containing IDs, names, ages, bios, and image URLs.

Simulation Logic

Swiping: When you swipe right, the app triggers a Math.random() check. If the result is > 0.6, a match is triggered.

Chatting: When you send a message, the app appends it to the chat history. A setTimeout is then triggered to simulate the other person reading and typing, eventually adding a randomized response from a predefined list.

🔮 Future Improvements

Add local storage persistence to save matches/chats on refresh.

Add "Undo" swipe functionality.

Implement more complex chat logic (keywords detection).

Add a profile editor to change your own photo and bio.

📄 License

This project is open source and available under the MIT License.
