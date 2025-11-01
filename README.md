# Astrologer-website
My College project astrologer website
<!doctype html>

<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>AstroConnect: Chat with Your Astrologer 🌙</title>
  <style>
    :root{
      --royal: #2b3ba7; /* royal blue */
      --bg: radial-gradient(1200px 600px at 10% 10%, rgba(255,255,255,0.03), transparent),
            radial-gradient(1000px 400px at 90% 90%, rgba(255,255,255,0.02), transparent),
            var(--pattern), linear-gradient(180deg,var(--royal), #1e2a7a);
      --card: rgba(255,255,255,0.06);
      --glass: rgba(255,255,255,0.06);
      --accent: #ffd54a;
    }/* White hearts pattern using inline SVG data URI */
:root{ --pattern: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='80' height='80' viewBox='0 0 24 24'%3E%3Cpath fill='%23ffffff' fill-opacity='0.06' d='M12 21s-6.716-4.35-9.243-6.966C.063 11.9 2.08 7.5 6 6.94 7.93 6.62 9.3 7.9 12 10.5c2.7-2.6 4.07-3.88 6-3.56 3.92.56 5.94 4.96 3.243 7.094C18.716 16.65 12 21 12 21z'/%3E%3C/svg%3E"); }

*{box-sizing:border-box}
html,body{height:100%;margin:0;font-family:Inter, system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial; background:var(--bg); color: #fff}

/* Center layout */
.wrap{min-height:100vh;display:flex;align-items:center;justify-content:center;padding:28px}
.card{
  width:100%;max-width:980px;border-radius:18px;background:linear-gradient(180deg, rgba(255,255,255,0.04), rgba(255,255,255,0.02));backdrop-filter: blur(6px);box-shadow:0 10px 30px rgba(10,10,30,0.4);overflow:hidden;display:grid;grid-template-columns:1fr 420px;gap:0;
}

/* Left side: header + info */
.left{
  padding:28px;display:flex;flex-direction:column;gap:18px;
  background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
}

header.site-header{display:flex;align-items:center;gap:14px}
.logo{width:64px;height:64px;border-radius:12px;background:linear-gradient(135deg,var(--accent),#ff9f00);display:flex;align-items:center;justify-content:center;box-shadow:0 6px 20px rgba(0,0,0,0.35);font-weight:700;color:#10203a}
.title{font-size:20px;font-weight:700;line-height:1}
.subtitle{font-size:13px;opacity:0.9}

.desc{font-size:14px;line-height:1.5;opacity:0.95}

/* Right side: chat area */
.chat-area{display:flex;flex-direction:column;height:620px;background:transparent;padding:18px}
.messages{flex:1;overflow:auto;padding:14px;display:flex;flex-direction:column;gap:12px}

.msg{max-width:78%;padding:12px 14px;border-radius:14px;animation:fadeIn .28s ease both;position:relative}
.user{align-self:flex-end;background:linear-gradient(180deg, rgba(255,255,255,0.09), rgba(255,255,255,0.05));color:#04132b}
.astro{align-self:flex-start;background:rgba(255,255,255,0.04);border:1px solid rgba(255,255,255,0.03)}

.meta{font-size:11px;opacity:0.7;margin-top:6px}

/* Typing bubble */
.typing{display:inline-flex;gap:6px;align-items:center;padding:10px 12px;border-radius:12px}
.dot{width:7px;height:7px;border-radius:50%;background:#fff;opacity:0.85;animation:blink 1s infinite}
.dot:nth-child(2){animation-delay:0.15s}
.dot:nth-child(3){animation-delay:0.3s}

/* Input area */
.input-wrap{display:flex;gap:12px;padding:12px;border-top:1px solid rgba(255,255,255,0.03);background:linear-gradient(180deg, rgba(0,0,0,0.02), transparent)}
.input{flex:1;background:transparent;border:1px solid rgba(255,255,255,0.06);padding:12px 14px;border-radius:12px;color:#fff;font-size:15px;outline:none}
.send-btn{background:linear-gradient(90deg,var(--accent),#ffb857);border:none;padding:0 16px;border-radius:12px;color:#10203a;font-weight:700;cursor:pointer;box-shadow:0 8px 18px rgba(0,0,0,0.28);transition:transform .12s ease}
.send-btn:active{transform:translateY(1px)}

/* Small screen layout */
@media (max-width:900px){
  .card{grid-template-columns:1fr;max-width:640px}
  .left{order:2}
  .chat-area{order:1;height:74vh}
}

/* Animations */
@keyframes fadeIn{from{transform:translateY(6px);opacity:0}to{transform:none;opacity:1}}
@keyframes blink{0%{opacity:0.2}50%{opacity:1}100%{opacity:0.2}}

/* small touches */
.hint{font-size:13px;opacity:0.85}
.footer-note{font-size:12px;opacity:0.65}

/* nice scroll bar */
.messages::-webkit-scrollbar{width:8px}
.messages::-webkit-scrollbar-thumb{background:rgba(255,255,255,0.06);border-radius:12px}

/* accessible focus */
.send-btn:focus, .input:focus{box-shadow:0 0 0 4px rgba(255,213,74,0.08)}

  </style>
</head>
<body>
  <div class="wrap">
    <div class="card" role="application" aria-label="AstroConnect chat app">
      <div class="left">
        <header class="site-header">
          <div class="logo" aria-hidden>🌙</div>
          <div>
            <div class="title">AstroConnect: Chat with Your Astrologer 🌙</div>
            <div class="subtitle">Quick readings • Friendly astrologer • No signup</div>
          </div>
        </header><p class="desc">Namaste! Welcome to AstroConnect — ek halka phulka aur tez astrologer chat experience. Type your message and get a human-like reply with smooth typing animation. Yeh demo offline hai (no backend), purely frontend simulation.</p>

    <div style="display:flex;gap:10px;flex-direction:column">
      <div class="hint">Tips:</div>
      <ul style="margin:6px 0 0 18px;opacity:0.95">
        <li>Share your zodiac sign or birth details for a quick reading.</li>
        <li>Try: "Hello" or "Meray stars batao"</li>
      </ul>
    </div>

    <div style="margin-top:auto" class="footer-note">Made with ❤ — demo frontend only.</div>
  </div>

  <div class="chat-area">
    <div class="messages" id="messages" aria-live="polite" aria-atomic="false"></div>

    <div class="input-wrap">
      <input id="userInput" class="input" type="text" placeholder="Type your message... e.g. 'Namaste, mera zodiac sign Leo hai'" aria-label="Message input" />
      <button id="sendBtn" class="send-btn" aria-label="Send message">Send</button>
    </div>
  </div>

</div>

  </div>  <script>
    // Sample astrologer replies
    const SAMPLE = [
      "Namaste 🙏 I sense strong energy around you today. What’s your zodiac sign?",
      "Let me see your stars... 🌟",
      "Please share your date of birth and time for a quick reading.",
      "Your charts show a shift in love & career — thoda sabr rakho.",
      "The moon is influencing decisions this week — avoid big risks until Sunday."
    ];

    const messagesEl = document.getElementById('messages');
    const inputEl = document.getElementById('userInput');
    const sendBtn = document.getElementById('sendBtn');

    // Utility to create message element
    function createMsg(text, who){
      const div = document.createElement('div');
      div.className = 'msg ' + (who === 'user' ? 'user' : 'astro');
      div.setAttribute('role','article');
      div.innerHTML = <div class="bubble">${escapeHtml(text)}</div>;
      return div;
    }

    function escapeHtml(unsafe){
      return unsafe
        .replace(/&/g, '&amp;')
        .replace(/</g, '&lt;')
        .replace(/>/g, '&gt;')
        .replace(/"/g, '&quot;')
        .replace(/'/g, '&#039;');
    }

    // Smooth scroll to bottom
    function scrollToBottom(){
      messagesEl.scrollTo({top: messagesEl.scrollHeight, behavior: 'smooth'});
    }

    // Show typing indicator
    function showTyping(){
      const wrap = document.createElement('div');
      wrap.className = 'msg astro';
      wrap.innerHTML = <div class="typing"><div class="dot"></div><div class="dot"></div><div class="dot"></div></div>;
      messagesEl.appendChild(wrap);
      scrollToBottom();
      return wrap;
    }

    // Bot 'types' the message character by character inside a bubble
    function botReply(fullText, typingEl){
      // replace typing element with actual message and animate chars
      const bubble = document.createElement('div');
      bubble.className = 'msg astro';
      const inner = document.createElement('div');
      inner.style.whiteSpace = 'pre-wrap';
      inner.style.overflowWrap = 'break-word';
      inner.textContent = '';
      bubble.appendChild(inner);

      // replace typingEl
      messagesEl.replaceChild(bubble, typingEl);
      scrollToBottom();

      // Typing speed: faster for short messages, slower for long
      const baseDelay = Math.max(12, 24 - Math.min(12, fullText.length / 15)); // ms per char
      let idx = 0;

      return new Promise(resolve => {
        function step(){
          if(idx <= fullText.length){
            inner.textContent = fullText.slice(0, idx);
            idx++;
            scrollToBottom();
            setTimeout(step, baseDelay + Math.random()*20);
          } else {
            // add small delay then resolve
            setTimeout(()=>{ resolve(); }, 250);
          }
        }
        step();
      });
    }

    // Main send handler
    async function handleSend(){
      const text = inputEl.value.trim();
      if(!text) return;
      // append user message
      const userMsg = createMsg(text, 'user');
      messagesEl.appendChild(userMsg);
      inputEl.value = '';
      inputEl.focus();
      scrollToBottom();

      // Simulate fast-response: pick a reply timeframe based on user input length
      const typingIndicator = showTyping();

      // Choose an intelligent-ish reply: if user asks for zodiac, ask for sign; else random sample
      const lower = text.toLowerCase();
      let reply;
      if(/zodiac|sign|leo|virgo|aries|libra|scorpio|taurus|gemini|sagittarius|capricorn|aquarius|pisces/.test(lower)){
        reply = SAMPLE[1]; // Let me see your stars... 🌟
      } else if(/birth|dob|date of birth|time of birth|jan|feb|mar|april|may|june|july|aug|sep|oct|nov|dec/.test(lower)){
        reply = SAMPLE[2];
      } else if(/hello|hi|namaste|hey|hii/.test(lower)){
        reply = SAMPLE[0];
      } else {
        // random with higher chance for friendly prompts
        reply = SAMPLE[Math.floor(Math.random()*SAMPLE.length)];
      }

      // Emulate thinking time proportional to message length (but keep it 'fast')
      const thinkTime = Math.min(1200, 350 + Math.random()*600);
      await new Promise(r => setTimeout(r, thinkTime));

      // Now perform typing animation to reveal reply
      await botReply(reply, typingIndicator);

      // After reply, optionally append a follow-up quick tip (small chance)
      if(Math.random() < 0.3){
        const tip = createMsg("Tip: If you want a deeper reading, share your birth place and exact birth time.", 'astro');
        tip.style.opacity = '0';
        messagesEl.appendChild(tip);
        // subtle reveal
        setTimeout(()=>{ tip.style.transition = 'opacity .4s ease'; tip.style.opacity = '1'; scrollToBottom(); }, 180);
      }
    }

    sendBtn.addEventListener('click', handleSend);
    inputEl.addEventListener('keydown', function(e){ if(e.key === 'Enter') handleSend(); });

    // Add a tiny welcome sequence
    (async function welcome(){
      const t1 = showTyping();
      await new Promise(r=>setTimeout(r, 700));
      await botReply("Namaste 🙏 I am your friendly Astro guide. What's your zodiac sign or birth details?", t1);

      // add small second message after pause
      await new Promise(r=>setTimeout(r, 900));
      const t2 = showTyping();
      await new Promise(r=>setTimeout(r, 500));
      await botReply("Sample: 'I am Leo' or 'DOB 12-08-1995 03:30'", t2);
    })();

    // Accessibility: focus input on load
    window.addEventListener('load', ()=>{ inputEl.focus(); });

  </script></body>
</html>
