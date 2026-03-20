<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>AdityaGamerYT Dashboard</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap');

html, body {
  margin:0; padding:0;
  font-family:'Press Start 2P', monospace;
  overflow-x:hidden; background:#000; color:#fff; text-align:center;
}

h1 { font-size:2em; text-shadow:0 0 10px #fff; }
h2,h3 { margin:10px 0; }

/* Video background */
#userBgVideo {
  position:fixed; top:0; left:0; width:100%; height:100%;
  object-fit:cover; z-index:-2; filter:brightness(0.4);
}

/* Admin panel background */
#adminPanel {
  display:none; position:relative; z-index:1; padding:20px;
  background-image:url('https://freeimage.host/i/qw42EIs');
  background-size:cover; background-position:center; background-repeat:no-repeat;
}

/* Dashboard panel */
#dashboard { display:none; position:relative; z-index:1; padding:20px; }

/* Login panel */
#login { padding:20px; }

/* Cards */
.card {
  background:rgba(0,0,0,0.5);
  margin:15px auto; padding:20px; border-radius:20px; width:320px;
  box-shadow:0 0 15px #fff;
  transition: transform 0.3s, box-shadow 0.3s; position:relative;
}
.card:hover { transform:scale(1.05); box-shadow:0 0 20px #42e695, 0 0 20px #7873f5; }

/* Buttons */
button {
  background:linear-gradient(45deg,#42e695,#7873f5);
  color:white; border-radius:12px; border:none;
  padding:12px 22px; font-weight:bold; cursor:pointer; margin:8px;
  transition:0.3s; box-shadow:0 0 5px #fff;
}
button:hover { transform:scale(1.1); opacity:0.9; box-shadow:0 0 15px #42e695,0 0 15px #7873f5; }

/* XP Bar */
#xpBarContainer { width:100%; height:20px; background:rgba(255,255,255,0.2); border-radius:12px; overflow:hidden; box-shadow:0 0 8px #fff inset; margin-top:10px; }
#xpBar { width:0%; height:100%; border-radius:12px; background: linear-gradient(90deg,#42e695,#7873f5); transition:width 0.5s; position:relative; }

/* Sparkles */
.sparkle { position:absolute; width:4px; height:4px; border-radius:50%; background:white; opacity:0.7; pointer-events:none; animation:sparkleAnim 0.8s linear infinite; }
@keyframes sparkleAnim { 0%{transform:translate(0,0) scale(1); opacity:1;} 50%{transform:translate(4px,-4px) scale(0.5); opacity:0.5;} 100%{transform:translate(0,0) scale(1); opacity:1;} }

/* Confetti */
.confetti { position:absolute; width:6px; height:6px; top:0; animation:fall 3s linear forwards; }
@keyframes fall {0%{top:-10px;opacity:1;}100%{top:100%;opacity:0;}}

/* Input fields */
input { padding:10px; border-radius:8px; border:none; margin:5px; width:80%; text-align:center; }

/* Social links */
.social-btn { display:inline-block; width:140px; }

/* Particles */
#particleCanvas { position:fixed; top:0; left:0; width:100%; height:100%; z-index:-1; pointer-events:none; }
</style>
<script src="https://unpkg.com/@lottiefiles/lottie-player@latest/dist/lottie-player.js"></script>
</head>
<body>

<h1>AdityaGamerYT Dashboard 🌧️</h1>

<!-- Video background -->
<video autoplay muted loop id="userBgVideo">
  <source src="https://www.w3schools.com/howto/rain.mp4" type="video/mp4">
</video>

<!-- Login Panel -->
<div id="login">
  <h2>User / Admin Login 🔐</h2>
  <div class="card">
    <h3>User Login 📱</h3>
    <input type="text" id="phone" placeholder="Phone Number"><br>
    <button onclick="fakeOTP()">Send OTP</button><br>
    <input type="text" id="otp" placeholder="OTP"><br>
    <button onclick="loginUser()">Login as User</button>
  </div>
  <div class="card">
    <h3>Admin Login 👑</h3>
    <input type="text" id="adminEmail" placeholder="Gmail"><br>
    <input type="password" id="adminPass" placeholder="Password"><br>
    <button onclick="loginAdmin()">Login as Admin</button>
  </div>
</div>

<!-- User Dashboard -->
<div id="dashboard">
  <div class="card">
    <lottie-player src="https://assets3.lottiefiles.com/packages/lf20_tfb3estd.json" background="transparent" speed="1" style="width:180px;height:180px;margin:auto;" loop autoplay></lottie-player>
    <h3 id="greeting">👋 Hello Gamer</h3>
    <p id="time">⏰ Time: </p>
  </div>

  <div class="card">
    <h3>👤 Your Info</h3>
    <p id="userNumber">📱 Number: </p>
  </div>

  <div class="card">
    <h3>🎮 Minecraft Server</h3>
    <img src="https://media.giphy.com/media/l0HlQ7LRal8nE2pGk/giphy.gif" style="width:100%;border-radius:15px;">
    <p>Server: GLAXY HOST</p>
    <p>IP: play.adityamc.fun</p>
    <button onclick="copyIP()">📋 Copy IP</button>
  </div>

  <div class="card">
    <h3>📸 Social Links</h3>
    <a class="social-btn" href="https://instagram.com/_btwitsadityagg" target="_blank"><button>😎 Instagram</button></a>
    <a class="social-btn" href="https://www.youtube.com/@AdityaGamerYT-s-3p" target="_blank"><button>🔥 YouTube</button></a>
  </div>

  <div class="card">
    <h3>🎮 Player Stats</h3>
    <p>Level: <span id="level">1</span></p>
    <p>XP: <span id="xp">0</span>/100</p>
    <div id="xpBarContainer"><div id="xpBar"></div></div>
    <button onclick="gainXP()">🔥 Gain XP</button>
  </div>

  <div class="card">
    <h3>🌐 Open Live Link</h3>
    <button onclick="openLiveLink()">Open Live Link</button>
  </div>

  <button onclick="logout()">🔄 Logout</button>
</div>

<!-- Admin Panel -->
<div id="adminPanel">
  <h2>👑 Admin Panel</h2>
  <div class="card">
    <img src="https://freeimage.host/i/qw42EIs" style="width:100%;border-radius:20px;">
  </div>
  <h3>Change Welcome Text</h3>
  <input type="text" id="newText" placeholder="New Text">
  <button onclick="changeText()">Update</button>
  <button onclick="logout()">🔄 Logout</button>
</div>

<script>
// Login info
const allowedPhone="7696044754", otpCode="2013";
const adminEmailFixed="admin@gmail.com", adminPasswordFixed="admin2013";

// User/Admin login
function fakeOTP(){ const phone=document.getElementById("phone").value; if(phone===allowedPhone){alert("OTP Sent 📱 (2013)");}else{alert("Number not allowed ❌");} }
function loginUser(){ const phone=document.getElementById("phone").value, otp=document.getElementById("otp").value; if(phone===allowedPhone&&otp===otpCode){ document.getElementById("login").style.display="none"; document.getElementById("dashboard").style.display="block"; document.getElementById("userNumber").innerText="📱 Number: "+phone; } else{ alert("Wrong User details ❌"); } }
function loginAdmin(){ const email=document.getElementById("adminEmail").value, pass=document.getElementById("adminPass").value; if(email===adminEmailFixed&&pass===adminPasswordFixed){ document.getElementById("login").style.display="none"; document.getElementById("adminPanel").style.display="block"; }else{ alert("Wrong Admin details ❌"); } }
function logout(){ location.reload(); }

// Greeting & time
function updateTime(){ const now=new Date(); document.getElementById("time").innerText="⏰ Time: "+now.toLocaleTimeString(); let h=now.getHours(), greet="👋 Hello"; if(h<12) greet="🌅 Good Morning"; else if(h<18) greet="☀️ Good Afternoon"; else greet="🌙 Good Evening"; document.getElementById("greeting").innerText=greet+" Gamer 😎"; }
setInterval(updateTime,1000);

// XP
let xp=0, level=1;
function gainXP(){
  xp+=10;
  if(xp>=100){ xp=0; level++; alert("Level Up! 🎉"); addConfetti();}
  document.getElementById("xp").innerText=xp;
  document.getElementById("level").innerText=level;
  const xpBar=document.getElementById("xpBar"); xpBar.style.width=xp+"%";
  for(let i=0;i<5;i++){
    const sparkle=document.createElement("div"); sparkle.className="sparkle";
    sparkle.style.left=Math.random()*xpBar.offsetWidth+"px"; sparkle.style.top=Math.random()*xpBar.offsetHeight+"px"; xpBar.appendChild(sparkle);
    setTimeout(()=>{sparkle.remove();},800);
  }
}

// Copy IP
function copyIP(){ navigator.clipboard.writeText("play.adityamc.fun"); alert("IP Copied ✅"); }
function changeText(){ document.getElementById("greeting").innerText=document.getElementById("newText").value; }

// Particles
const canvas=document.createElement('canvas'); canvas.id='particleCanvas'; document.body.appendChild(canvas);
const ctx=canvas.getContext('2d'); canvas.width=window.innerWidth; canvas.height=window.innerHeight;
const particles=[];
for(let i=0;i<150;i++){ particles.push({x:Math.random()*canvas.width,y:Math.random()*canvas.height,r:Math.random()*2+1,dx:(Math.random()-0.5)*0.5,dy:(Math.random()-0.5)*0.5}); }
function drawParticles(){ ctx.clearRect(0,0,canvas.width,canvas.height); particles.forEach(p=>{ ctx.beginPath(); ctx.arc(p.x,p.y,p.r,0,Math.PI*2); ctx.fillStyle="rgba(255,255,255,0.5)"; ctx.fill(); p.x+=p.dx; p.y+=p.dy; if(p.x<0||p.x>canvas.width) p.dx*=-1; if(p.y<0||p.y>canvas.height) p.dy*=-1; }); requestAnimationFrame(drawParticles); }
drawParticles();

function addConfetti(){ for(let i=0;i<50;i++){ const conf=document.createElement("div"); conf.className="confetti"; conf.style.left=Math.random()*window.innerWidth+"px"; conf.style.background=`hsl(${Math.random()*360},100%,50%)`; document.body.appendChild(conf); setTimeout(()=>conf.remove(),3500); } }

// Open Live Link with prompt
function openLiveLink(){
  let url = prompt("Enter your live dashboard URL:", "https://adityagamergg2008"); // prefilled
  if(url && url.trim() !== ""){ window.open(url, "_blank"); } else{ alert("No URL entered ❌"); }
}
</script>

</body>
</html>
