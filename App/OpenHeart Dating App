import React, { useState, useEffect, useRef } from 'react';
import { Heart, X, MessageCircle, User, Settings, Send, ChevronLeft, Sparkles, ShieldCheck, MapPin, Coffee, Music, Camera, Book } from 'lucide-react';

// --- Mock Data & Utilities ---

const MOCK_PROFILES = [
  { id: 1, name: 'Alex', age: 24, bio: 'Coffee addict ☕ & amateur photographer. Looking for someone to explore the city with.', distance: '3 miles away', interests: ['Photography', 'Travel', 'Sushi'], image: 'https://images.unsplash.com/photo-1500648767791-00dcc994a43e?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3' },
  { id: 2, name: 'Sarah', age: 26, bio: 'Dog mom 🐕. I love hiking and spicy food. Let\'s go on an adventure!', distance: '5 miles away', interests: ['Hiking', 'Dogs', 'Tacos'], image: 'https://images.unsplash.com/photo-1494790108377-be9c29b29330?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3' },
  { id: 3, name: 'Jordan', age: 28, bio: 'Tech geek by day, musician by night. 🎸', distance: '2 miles away', interests: ['Music', 'Coding', 'Sci-Fi'], image: 'https://images.unsplash.com/photo-1506794778202-cad84cf45f1d?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3' },
  { id: 4, name: 'Emily', age: 23, bio: 'Art student. I paint feelings. 🎨', distance: '10 miles away', interests: ['Art', 'Museums', 'Wine'], image: 'https://images.unsplash.com/photo-1534528741775-53994a69daeb?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3' },
  { id: 5, name: 'David', age: 30, bio: 'Chef who loves to cook for others. 🍝', distance: '1 mile away', interests: ['Cooking', 'Wine', 'Movies'], image: 'https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3' },
  { id: 6, name: 'Jessica', age: 25, bio: 'Yoga instructor and plant lover. 🌱', distance: '4 miles away', interests: ['Yoga', 'Plants', 'Wellness'], image: 'https://images.unsplash.com/photo-1438761681033-6461ffad8d80?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3' },
  { id: 7, name: 'Michael', age: 27, bio: 'Avid reader and writer. Let\'s discuss our favorite books.', distance: '6 miles away', interests: ['Reading', 'Writing', 'History'], image: 'https://images.unsplash.com/photo-1492562080023-ab3db95bfbce?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3' },
  { id: 8, name: 'Olivia', age: 22, bio: 'Fashion enthusiast. 👗 Always looking for the next trend.', distance: '8 miles away', interests: ['Fashion', 'Shopping', 'Design'], image: 'https://images.unsplash.com/photo-1517841905240-472988babdf9?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3' },
];

const INITIAL_MESSAGES = [
  "Hey! How's your day going?",
  "I love your bio! 😊",
  "That picture is amazing, where was it taken?",
  "Hi there! Nice to match with you.",
];

// --- Components ---

const MatchPopup = ({ match, onClose }) => (
  <div className="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/80 animate-in fade-in duration-300">
    <div className="bg-gradient-to-br from-rose-500 to-pink-600 rounded-3xl p-8 max-w-sm w-full text-center relative shadow-2xl transform transition-all scale-100">
      <div className="absolute top-0 left-0 w-full h-full overflow-hidden rounded-3xl z-0">
        <div className="absolute top-10 left-10 w-20 h-20 bg-white/20 rounded-full blur-xl animate-pulse"></div>
        <div className="absolute bottom-10 right-10 w-32 h-32 bg-purple-500/30 rounded-full blur-xl animate-pulse"></div>
      </div>
      
      <div className="relative z-10">
        <Sparkles className="w-12 h-12 text-yellow-300 mx-auto mb-4 animate-bounce" />
        <h2 className="text-4xl font-black text-white italic mb-2 drop-shadow-md">IT'S A MATCH!</h2>
        <p className="text-white/90 mb-8">You and {match.name} like each other.</p>
        
        <div className="flex justify-center items-center gap-4 mb-8">
          <div className="w-20 h-20 rounded-full border-4 border-white overflow-hidden shadow-lg">
            <img src="https://images.unsplash.com/photo-1535713875002-d1d0cf377fde?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3" alt="You" className="w-full h-full object-cover" />
          </div>
          <Heart className="w-8 h-8 text-white fill-current animate-pulse" />
          <div className="w-20 h-20 rounded-full border-4 border-white overflow-hidden shadow-lg">
            <img src={match.image} alt={match.name} className="w-full h-full object-cover" />
          </div>
        </div>

        <button 
          onClick={onClose}
          className="w-full bg-white text-rose-600 font-bold py-3 rounded-full hover:bg-gray-100 transition-colors shadow-lg mb-3"
        >
          Send a Message
        </button>
        <button 
          onClick={onClose}
          className="w-full bg-transparent border-2 border-white text-white font-bold py-3 rounded-full hover:bg-white/10 transition-colors"
        >
          Keep Swiping
        </button>
      </div>
    </div>
  </div>
);

// New Separated Component for Chat View to fix Hook Rules
const ChatView = ({ activeChat, messages, onSendMessage, onBack }) => {
  const scrollRef = useRef(null);
  const [inputText, setInputText] = useState('');

  useEffect(() => {
      if (scrollRef.current) {
          scrollRef.current.scrollTop = scrollRef.current.scrollHeight;
      }
  }, [messages]);

  if (!activeChat) return null;

  return (
    <div className="flex flex-col h-full bg-white">
      {/* Chat Header */}
      <div className="flex items-center gap-3 p-4 border-b border-gray-100 shadow-sm z-10">
        <button onClick={onBack} className="p-2 hover:bg-gray-100 rounded-full">
          <ChevronLeft className="w-6 h-6 text-gray-600" />
        </button>
        <img src={activeChat.image} alt={activeChat.name} className="w-10 h-10 rounded-full object-cover" />
        <div>
          <h3 className="font-bold text-gray-800 leading-none">{activeChat.name}</h3>
          <span className="text-xs text-green-500 font-medium">Online now</span>
        </div>
      </div>

      {/* Messages */}
      <div className="flex-1 overflow-y-auto p-4 bg-gray-50" ref={scrollRef}>
        {messages.length === 0 && (
            <div className="text-center mt-8 opacity-50">
                <p className="text-sm">You matched with {activeChat.name}!</p>
                <p className="text-xs">Say hello 👋</p>
            </div>
        )}
        {messages.map((msg, idx) => (
          <div key={idx} className={`flex mb-4 ${msg.sender === 'me' ? 'justify-end' : 'justify-start'}`}>
            <div className={`max-w-[75%] p-3 rounded-2xl text-sm ${
              msg.sender === 'me' 
                ? 'bg-rose-500 text-white rounded-br-none' 
                : 'bg-white text-gray-800 border border-gray-100 shadow-sm rounded-bl-none'
            }`}>
              {msg.text}
            </div>
          </div>
        ))}
      </div>

      {/* Input */}
      <div className="p-3 border-t border-gray-100 bg-white">
        <form 
          onSubmit={(e) => { e.preventDefault(); onSendMessage(inputText); setInputText(''); }}
          className="flex gap-2 items-center"
        >
          <input
            type="text"
            value={inputText}
            onChange={(e) => setInputText(e.target.value)}
            placeholder="Type a message..."
            className="flex-1 bg-gray-100 text-gray-800 rounded-full px-4 py-3 text-sm focus:outline-none focus:ring-2 focus:ring-rose-500/50"
          />
          <button 
              type="submit" 
              disabled={!inputText.trim()}
              className="w-10 h-10 bg-rose-500 text-white rounded-full flex items-center justify-center disabled:opacity-50 disabled:cursor-not-allowed hover:bg-rose-600 transition-colors"
          >
            <Send className="w-4 h-4 ml-0.5" />
          </button>
        </form>
      </div>
    </div>
  );
};

// Main Application Component
export default function OpenHeartApp() {
  const [activeTab, setActiveTab] = useState('home'); // home, matches, profile, chat
  const [profiles, setProfiles] = useState(MOCK_PROFILES);
  const [currentIndex, setCurrentIndex] = useState(0);
  const [lastDirection, setLastDirection] = useState(null);
  const [matches, setMatches] = useState([]);
  const [activeChat, setActiveChat] = useState(null);
  const [showMatchPopup, setShowMatchPopup] = useState(null);
  const [userProfile, setUserProfile] = useState({
    name: 'You',
    age: 25,
    bio: 'New to OpenHeart! Looking for genuine connections.',
    interests: ['Travel', 'Music', 'Food'],
    image: 'https://images.unsplash.com/photo-1535713875002-d1d0cf377fde?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3'
  });
  const [chats, setChats] = useState({}); // { matchId: [{sender: 'me'|'them', text: ''}] }

  // --- Swiping Logic ---

  const swipe = (direction) => {
    if (currentIndex >= profiles.length) return;

    const currentProfile = profiles[currentIndex];
    setLastDirection(direction);
    
    // Simulate swiping animation delay
    setTimeout(() => {
      if (direction === 'right') {
        // 40% chance of a match for simulation purposes
        const isMatch = Math.random() > 0.6; 
        if (isMatch) {
          handleMatch(currentProfile);
        }
      }
      setCurrentIndex((prev) => prev + 1);
      setLastDirection(null);
    }, 200);
  };

  const handleMatch = (profile) => {
    const newMatch = { ...profile, matchedAt: new Date() };
    setMatches(prev => [newMatch, ...prev]);
    setShowMatchPopup(newMatch);
    
    // Add initial greeting after delay
    setTimeout(() => {
        addMessage(profile.id, { 
            sender: 'them', 
            text: INITIAL_MESSAGES[Math.floor(Math.random() * INITIAL_MESSAGES.length)] 
        });
    }, 3000);
  };

  const addMessage = (matchId, message) => {
    setChats(prev => ({
      ...prev,
      [matchId]: [...(prev[matchId] || []), { ...message, timestamp: new Date() }]
    }));
  };

  const handleSendMessage = (text) => {
    if (!text.trim() || !activeChat) return;
    
    addMessage(activeChat.id, { sender: 'me', text });
    
    // Simulate reply
    setTimeout(() => {
      const replies = ["That's interesting!", "Haha, totally!", "Tell me more about that.", "I was thinking the same thing.", "So, what are you up to this weekend?"];
      addMessage(activeChat.id, { sender: 'them', text: replies[Math.floor(Math.random() * replies.length)] });
    }, 2000 + Math.random() * 3000);
  };

  // --- Views ---

  const renderHome = () => {
    if (currentIndex >= profiles.length) {
      return (
        <div className="flex flex-col items-center justify-center h-full p-8 text-center animate-in fade-in">
          <div className="w-24 h-24 bg-gray-100 rounded-full flex items-center justify-center mb-6">
            <Sparkles className="w-10 h-10 text-gray-400" />
          </div>
          <h2 className="text-2xl font-bold text-gray-800 mb-2">That's everyone for now!</h2>
          <p className="text-gray-500 mb-8">You've seen all the profiles in your area. Check back later for more.</p>
          <button 
            onClick={() => setCurrentIndex(0)}
            className="px-6 py-3 bg-rose-500 text-white rounded-full font-semibold shadow-lg hover:bg-rose-600 transition-colors"
          >
            Start Over (Demo)
          </button>
        </div>
      );
    }

    const profile = profiles[currentIndex];

    return (
      <div className="relative h-full flex flex-col p-4 max-w-md mx-auto w-full">
        {/* Header */}
        <div className="flex justify-between items-center mb-4">
            <div className="flex items-center gap-1 text-rose-500">
                <Heart className="fill-current w-6 h-6" />
                <span className="font-bold text-xl tracking-tight">OpenHeart</span>
            </div>
            <div className="bg-rose-100 px-3 py-1 rounded-full">
                <span className="text-xs font-bold text-rose-600 uppercase tracking-wider">Free Forever</span>
            </div>
        </div>

        {/* Card Stack Container */}
        <div className="flex-1 relative mb-6">
            {/* Background Card Effect */}
            <div className="absolute inset-0 top-2 scale-95 bg-white border border-gray-200 rounded-3xl shadow-sm z-0"></div>
            
            {/* Active Card */}
            <div className={`absolute inset-0 bg-white rounded-3xl shadow-xl overflow-hidden border border-gray-100 z-10 transition-transform duration-300 ${lastDirection === 'left' ? '-translate-x-full opacity-0 rotate-[-20deg]' : lastDirection === 'right' ? 'translate-x-full opacity-0 rotate-[20deg]' : ''}`}>
                <div className="relative h-[65%]">
                    <img src={profile.image} alt={profile.name} className="w-full h-full object-cover" />
                    <div className="absolute inset-0 bg-gradient-to-t from-black/80 via-transparent to-transparent"></div>
                    <div className="absolute bottom-4 left-4 text-white">
                        <h2 className="text-3xl font-bold flex items-end gap-2">
                            {profile.name} <span className="text-xl font-normal opacity-90">{profile.age}</span>
                        </h2>
                        <div className="flex items-center gap-1 opacity-90 text-sm mt-1">
                            <MapPin className="w-3 h-3" />
                            <span>{profile.distance}</span>
                        </div>
                    </div>
                </div>
                
                <div className="p-5 h-[35%] flex flex-col">
                    <div className="flex flex-wrap gap-2 mb-3">
                        {profile.interests.map((tag, i) => (
                            <span key={i} className="px-3 py-1 bg-gray-100 text-gray-600 text-xs rounded-full font-medium">
                                {tag}
                            </span>
                        ))}
                    </div>
                    <p className="text-gray-600 text-sm line-clamp-3 leading-relaxed">
                        {profile.bio}
                    </p>
                </div>
            </div>
        </div>

        {/* Controls */}
        <div className="h-20 flex justify-center items-center gap-6 z-20">
            <button 
                onClick={() => swipe('left')}
                className="w-14 h-14 bg-white text-rose-500 rounded-full shadow-lg border border-gray-100 flex items-center justify-center hover:scale-110 hover:bg-rose-50 transition-all duration-200 focus:outline-none"
            >
                <X className="w-8 h-8" />
            </button>
            <button 
                onClick={() => swipe('right')}
                className="w-16 h-16 bg-rose-500 text-white rounded-full shadow-xl shadow-rose-200 flex items-center justify-center hover:scale-110 hover:bg-rose-600 transition-all duration-200 focus:outline-none"
            >
                <Heart className="w-8 h-8 fill-current" />
            </button>
        </div>
      </div>
    );
  };

  const renderMatches = () => (
    <div className="flex flex-col h-full bg-white">
      <div className="p-4 border-b border-gray-100">
        <h2 className="text-xl font-bold text-gray-800">Matches</h2>
        <p className="text-sm text-gray-500">People who liked you back</p>
      </div>
      
      <div className="flex-1 overflow-y-auto p-4">
        {matches.length === 0 ? (
          <div className="flex flex-col items-center justify-center h-64 text-center">
             <div className="w-16 h-16 bg-gray-50 rounded-full flex items-center justify-center mb-4">
                <Heart className="w-8 h-8 text-gray-300" />
            </div>
            <p className="text-gray-500 font-medium">No matches yet.</p>
            <p className="text-gray-400 text-sm mt-1">Keep swiping to find your person!</p>
          </div>
        ) : (
          <div className="grid grid-cols-1 gap-4">
            {matches.map(match => (
              <div 
                key={match.id} 
                onClick={() => { setActiveChat(match); setActiveTab('chat'); }}
                className="flex items-center gap-4 p-3 rounded-xl hover:bg-gray-50 cursor-pointer transition-colors border border-transparent hover:border-gray-100"
              >
                <div className="relative">
                    <img src={match.image} alt={match.name} className="w-16 h-16 rounded-full object-cover border-2 border-white shadow-sm" />
                    <div className="absolute bottom-0 right-0 w-4 h-4 bg-green-500 border-2 border-white rounded-full"></div>
                </div>
                <div className="flex-1">
                  <h3 className="font-bold text-gray-800">{match.name}, {match.age}</h3>
                  <p className="text-sm text-gray-500 truncate">
                    {chats[match.id]?.length > 0 
                        ? chats[match.id][chats[match.id].length - 1].text 
                        : "Start a conversation!"}
                  </p>
                </div>
                <div className="w-8 h-8 flex items-center justify-center text-gray-300">
                    <MessageCircle className="w-5 h-5" />
                </div>
              </div>
            ))}
          </div>
        )}
      </div>
    </div>
  );

  const renderProfile = () => (
    <div className="h-full overflow-y-auto bg-gray-50 pb-20">
      <div className="relative h-64 bg-gray-200">
        <img src={userProfile.image} alt="You" className="w-full h-full object-cover" />
        <div className="absolute inset-0 bg-gradient-to-t from-black/60 to-transparent"></div>
        <div className="absolute bottom-4 left-4 text-white">
             <h2 className="text-3xl font-bold">{userProfile.name}, {userProfile.age}</h2>
        </div>
        <button className="absolute top-4 right-4 bg-white/20 backdrop-blur-md p-2 rounded-full text-white hover:bg-white/30 transition-colors">
            <Settings className="w-6 h-6" />
        </button>
      </div>

      <div className="p-4">
        {/* Stats */}
        <div className="flex gap-4 mb-6">
            <div className="flex-1 bg-white p-4 rounded-2xl shadow-sm border border-gray-100 text-center">
                <span className="block text-2xl font-bold text-rose-500">{matches.length}</span>
                <span className="text-xs text-gray-500 uppercase tracking-wide font-medium">Matches</span>
            </div>
            <div className="flex-1 bg-white p-4 rounded-2xl shadow-sm border border-gray-100 text-center">
                <span className="block text-2xl font-bold text-purple-500">0</span>
                <span className="text-xs text-gray-500 uppercase tracking-wide font-medium">Likes Sent</span>
            </div>
        </div>

        {/* Premium Banner (Free) */}
        <div className="bg-gradient-to-r from-yellow-400 to-orange-500 p-4 rounded-2xl text-white mb-6 shadow-lg shadow-orange-200 relative overflow-hidden">
            <div className="relative z-10">
                <div className="flex items-center gap-2 mb-1">
                    <ShieldCheck className="w-5 h-5" />
                    <span className="font-bold text-lg">OpenHeart Premium</span>
                </div>
                <p className="text-white/90 text-sm mb-3">Unlimited swipes, see who likes you, and more.</p>
                <div className="inline-block bg-white/20 backdrop-blur-sm px-3 py-1 rounded-lg text-xs font-bold border border-white/30">
                    ACTIVATED FOR FREE
                </div>
            </div>
            <Sparkles className="absolute -right-4 -bottom-4 w-24 h-24 text-white/20 rotate-12" />
        </div>

        {/* Bio Section */}
        <div className="bg-white p-5 rounded-2xl shadow-sm border border-gray-100 mb-4">
            <h3 className="font-bold text-gray-800 mb-3 flex items-center gap-2">
                <User className="w-4 h-4 text-rose-500" /> About Me
            </h3>
            <p className="text-gray-600 text-sm leading-relaxed">{userProfile.bio}</p>
        </div>

        {/* Interests */}
        <div className="bg-white p-5 rounded-2xl shadow-sm border border-gray-100 mb-4">
            <h3 className="font-bold text-gray-800 mb-3 flex items-center gap-2">
                <Sparkles className="w-4 h-4 text-rose-500" /> Interests
            </h3>
            <div className="flex flex-wrap gap-2">
                {userProfile.interests.map((int, i) => (
                    <span key={i} className="px-3 py-1 bg-rose-50 text-rose-600 text-xs rounded-full font-medium border border-rose-100">
                        {int}
                    </span>
                ))}
            </div>
        </div>

        <button className="w-full py-4 text-gray-400 font-medium hover:text-rose-500 transition-colors text-sm">
            Sign Out
        </button>
      </div>
    </div>
  );

  return (
    <div className="h-screen w-full bg-gray-100 flex items-center justify-center font-sans antialiased text-gray-900">
      <div className="w-full max-w-[480px] h-full sm:h-[90vh] sm:rounded-[40px] bg-white shadow-2xl relative overflow-hidden flex flex-col">
        
        {/* Main Content Area */}
        <div className="flex-1 overflow-hidden relative">
          {activeTab === 'home' && renderHome()}
          {activeTab === 'matches' && renderMatches()}
          {activeTab === 'chat' && activeChat && (
              <ChatView 
                  activeChat={activeChat} 
                  messages={chats[activeChat.id] || []}
                  onSendMessage={handleSendMessage}
                  onBack={() => setActiveTab('matches')}
              />
          )}
          {activeTab === 'profile' && renderProfile()}
        </div>

        {/* Navigation Bar */}
        {activeTab !== 'chat' && (
          <div className="h-16 bg-white border-t border-gray-100 flex justify-around items-center px-2 z-30">
            <button 
                onClick={() => setActiveTab('home')}
                className={`p-3 rounded-2xl transition-all duration-300 ${activeTab === 'home' ? 'text-rose-500 bg-rose-50' : 'text-gray-400 hover:text-gray-600'}`}
            >
              <Heart className={`w-6 h-6 ${activeTab === 'home' ? 'fill-current' : ''}`} />
            </button>
            <button 
                onClick={() => setActiveTab('matches')}
                className={`p-3 rounded-2xl transition-all duration-300 relative ${activeTab === 'matches' ? 'text-rose-500 bg-rose-50' : 'text-gray-400 hover:text-gray-600'}`}
            >
              <MessageCircle className="w-6 h-6" />
              {matches.length > 0 && (
                  <span className="absolute top-2 right-2 w-2.5 h-2.5 bg-rose-500 border-2 border-white rounded-full"></span>
              )}
            </button>
            <button 
                onClick={() => setActiveTab('profile')}
                className={`p-3 rounded-2xl transition-all duration-300 ${activeTab === 'profile' ? 'text-rose-500 bg-rose-50' : 'text-gray-400 hover:text-gray-600'}`}
            >
              <User className="w-6 h-6" />
            </button>
          </div>
        )}

        {/* Match Popup */}
        {showMatchPopup && (
            <MatchPopup match={showMatchPopup} onClose={() => setShowMatchPopup(null)} />
        )}

      </div>
    </div>
  );
}
