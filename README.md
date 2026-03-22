# ShubhangiRao25BAI10723
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>CampusCab — College Cab Booking</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;500;700&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  *{box-sizing:border-box;margin:0;padding:0}
  :root{
    --bg:#0a0a0f;--bg2:#13131a;--bg3:#1c1c26;--card:#1e1e2a;--card2:#252535;
    --accent:#f5c842;--accent2:#ff7f4e;--text:#f0eee8;--muted:#888;--border:#2a2a3a;
    --green:#4ade80;--red:#f87171;--blue:#60a5fa;
  }
  body{font-family:'DM Sans',sans-serif;background:var(--bg);color:var(--text);min-height:100vh;display:flex;justify-content:center;align-items:flex-start}
  .app{max-width:480px;width:100%;min-height:100vh;display:flex;flex-direction:column;background:var(--bg2)}
  .header{padding:20px 20px 12px;display:flex;align-items:center;justify-content:space-between;border-bottom:1px solid var(--border)}
  .logo{font-family:'Syne',sans-serif;font-weight:700;font-size:20px;letter-spacing:-0.5px;color:var(--text)}
  .logo span{color:var(--accent)}
  .avatar{width:36px;height:36px;border-radius:50%;background:var(--accent);display:flex;align-items:center;justify-content:center;font-weight:700;font-size:13px;color:#111}
  .nav{display:flex;gap:0;padding:0 20px;border-bottom:1px solid var(--border)}
  .nav-btn{flex:1;padding:12px 4px;background:none;border:none;color:var(--muted);font-size:13px;font-family:'DM Sans',sans-serif;cursor:pointer;border-bottom:2px solid transparent;transition:all .2s}
  .nav-btn.active{color:var(--accent);border-bottom-color:var(--accent);font-weight:500}
  .screen{flex:1;overflow-y:auto;padding:20px}
  .screen.hidden{display:none}
  .section-title{font-family:'Syne',sans-serif;font-size:22px;font-weight:700;margin-bottom:6px}
  .section-sub{font-size:13px;color:var(--muted);margin-bottom:20px}
  .mode-toggle{display:flex;background:var(--bg3);border-radius:12px;padding:4px;margin-bottom:20px;gap:4px}
  .mode-btn{flex:1;padding:9px;border:none;border-radius:8px;background:none;color:var(--muted);font-size:13px;font-family:'DM Sans',sans-serif;cursor:pointer;transition:all .2s;font-weight:500}
  .mode-btn.active{background:var(--card2);color:var(--text);box-shadow:0 1px 4px rgba(0,0,0,.4)}
  .field-label{font-size:11px;font-weight:500;letter-spacing:.5px;color:var(--muted);text-transform:uppercase;margin-bottom:6px}
  .input-row{position:relative;margin-bottom:12px}
  .field-input{width:100%;background:var(--bg3);border:1px solid var(--border);border-radius:10px;padding:12px 14px 12px 38px;color:var(--text);font-size:14px;font-family:'DM Sans',sans-serif;outline:none;transition:border-color .2s}
  .field-input:focus{border-color:var(--accent)}
  .field-icon{position:absolute;left:12px;top:50%;transform:translateY(-50%);font-size:14px}
  .row{display:flex;gap:10px;margin-bottom:12px}
  .row .input-row{flex:1;margin-bottom:0}
  .card{background:var(--card);border-radius:14px;border:1px solid var(--border);padding:16px;margin-bottom:12px}
  .card-title{font-weight:500;font-size:14px;margin-bottom:4px}
  .card-sub{font-size:12px;color:var(--muted)}
  .driver-card{display:flex;align-items:center;gap:12px;background:var(--card);border-radius:14px;border:1px solid var(--border);padding:14px;margin-bottom:10px;cursor:pointer;transition:border-color .2s}
  .driver-card:hover,.driver-card.selected{border-color:var(--accent)}
  .driver-avatar{width:44px;height:44px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-weight:700;font-size:16px;flex-shrink:0}
  .driver-info{flex:1}
  .driver-name{font-weight:500;font-size:14px}
  .driver-meta{font-size:12px;color:var(--muted);margin-top:2px}
  .driver-price{text-align:right}
  .price-main{font-family:'Syne',sans-serif;font-weight:700;font-size:18px;color:var(--accent)}
  .price-eta{font-size:11px;color:var(--muted)}
  .tag{display:inline-block;padding:2px 8px;border-radius:6px;font-size:10px;font-weight:500;margin-top:4px}
  .tag-green{background:rgba(74,222,128,.12);color:var(--green)}
  .tag-blue{background:rgba(96,165,250,.12);color:var(--blue)}
  .tag-orange{background:rgba(245,200,66,.12);color:var(--accent)}
  .btn{width:100%;padding:14px;border:none;border-radius:12px;background:var(--accent);color:#111;font-size:15px;font-weight:600;font-family:'DM Sans',sans-serif;cursor:pointer;transition:all .2s;margin-top:8px}
  .btn:hover{opacity:.9;transform:translateY(-1px)}
  .btn:active{transform:scale(.98)}
  .btn-outline{background:none;border:1px solid var(--border);color:var(--text)}
  .share-badge{background:rgba(245,200,66,.1);border:1px solid rgba(245,200,66,.3);border-radius:10px;padding:10px 14px;margin-bottom:14px;display:flex;align-items:center;gap:10px}
  .share-badge-icon{font-size:18px}
  .share-badge-text{font-size:13px;color:var(--text)}
  .share-badge-text span{color:var(--accent);font-weight:500}
  .divider{height:1px;background:var(--border);margin:14px 0}
  .rides-list{display:flex;flex-direction:column;gap:10px}
  .ride-card{background:var(--card);border-radius:14px;border:1px solid var(--border);padding:14px;position:relative;overflow:hidden}
  .ride-status{display:inline-block;padding:3px 10px;border-radius:20px;font-size:11px;font-weight:500;margin-bottom:8px}
  .status-active{background:rgba(74,222,128,.12);color:var(--green)}
  .status-scheduled{background:rgba(96,165,250,.12);color:var(--blue)}
  .status-done{background:rgba(136,136,136,.12);color:var(--muted)}
  .ride-route{font-size:13px;font-weight:500;margin-bottom:4px}
  .ride-detail{font-size:12px;color:var(--muted)}
  .ride-price{position:absolute;top:14px;right:14px;font-family:'Syne',sans-serif;font-weight:700;font-size:16px;color:var(--accent)}
  .tracking-card{background:var(--bg3);border-radius:14px;border:1px solid var(--border);height:160px;margin-bottom:14px;display:flex;align-items:center;justify-content:center;position:relative;overflow:hidden}
  .map-dot{position:absolute;width:10px;height:10px;border-radius:50%;background:var(--accent)}
  .map-road{position:absolute;background:var(--border);height:2px;left:10%;right:10%}
  .pulse{animation:pulse 1.5s ease infinite}
  @keyframes pulse{0%,100%{opacity:1}50%{opacity:.4}}
  .live-badge{position:absolute;top:12px;right:12px;background:rgba(74,222,128,.15);border:1px solid rgba(74,222,128,.3);border-radius:20px;padding:3px 10px;font-size:11px;color:var(--green);display:flex;align-items:center;gap:5px}
  .live-dot{width:6px;height:6px;border-radius:50%;background:var(--green);animation:pulse 1s infinite}
  .progress-bar{background:var(--bg3);border-radius:4px;height:4px;margin:8px 0;overflow:hidden}
  .progress-fill{height:100%;background:var(--accent);border-radius:4px;width:65%;animation:grow 3s ease forwards}
  @keyframes grow{from{width:10%}to{width:65%}}
  .step-row{display:flex;align-items:center;gap:10px;margin-bottom:10px}
  .step-dot{width:10px;height:10px;border-radius:50%;flex-shrink:0}
  .step-dot.done{background:var(--green)}
  .step-dot.active{background:var(--accent);animation:pulse 1s infinite}
  .step-dot.pending{background:var(--border)}
  .step-line{width:1px;height:14px;background:var(--border);margin-left:4px}
  .share-seats{display:flex;gap:8px;margin:10px 0}
  .seat{width:36px;height:36px;border-radius:8px;background:var(--bg3);border:1px solid var(--border);display:flex;align-items:center;justify-content:center;font-size:16px;cursor:pointer;transition:all .2s}
  .seat.taken{border-color:rgba(74,222,128,.4);background:rgba(74,222,128,.08);color:var(--green)}
  .seat.yours{border-color:var(--accent);background:rgba(245,200,66,.1)}
  .seat:hover{border-color:var(--muted)}
  .schedule-pill{display:flex;align-items:center;justify-content:space-between;background:var(--bg3);border-radius:10px;padding:10px 14px;margin-bottom:10px;border:1px solid var(--border);cursor:pointer;transition:border-color .2s}
  .schedule-pill:hover{border-color:var(--accent)}
  .schedule-time{font-family:'Syne',sans-serif;font-weight:700;font-size:15px;color:var(--accent)}
  .schedule-label{font-size:12px;color:var(--muted)}
</style>
</head>
<body>
<div class="app">
  <div class="header">
    <div class="logo">Campus<span>Cab</span></div>
    <div class="avatar">RS</div>
  </div>
  <div class="nav">
    <button class="nav-btn active" onclick="showScreen('book')">Book</button>
    <button class="nav-btn" onclick="showScreen('rides')">My Rides</button>
    <button class="nav-btn" onclick="showScreen('track')">Track</button>
  </div>

  <!-- BOOKING SCREEN -->
  <div class="screen" id="screen-book">
    <div class="section-title">Where to?</div>
    <div class="section-sub">Book or share a ride around campus</div>
    <div class="mode-toggle">
      <button class="mode-btn active" id="mode-solo" onclick="setMode('solo')">🚗 Solo Ride</button>
      <button class="mode-btn" id="mode-share" onclick="setMode('share')">👥 Share Cab</button>
      <button class="mode-btn" id="mode-sched" onclick="setMode('sched')">🕐 Schedule</button>
    </div>
    <div class="input-row">
      <span class="field-icon">📍</span>
      <input class="field-input" placeholder="Pickup — College gate, Hostel A…" id="pickup" value="Main Gate, VIT Bhopal University, Madhya Pradesh" />
    </div>
    <div class="input-row">
      <span class="field-icon">🏁</span>
      <input class="field-input" placeholder="Drop — Railway Station, Market…" id="drop" />
    </div>
    <div id="share-info" style="display:none">
      <div class="share-badge">
        <div class="share-badge-icon">💡</div>
        <div class="share-badge-text">Split fare with <span>2–3 others</span> going the same way. Save up to <span>60%</span>.</div>
      </div>
      <div class="field-label">Seats needed</div>
      <div class="share-seats">
        <div class="seat yours" title="You">👤</div>
        <div class="seat" id="s2" onclick="toggleSeat('s2')">➕</div>
        <div class="seat" id="s3" onclick="toggleSeat('s3')">➕</div>
        <div class="seat" id="s4" onclick="toggleSeat('s4')">➕</div>
      </div>
    </div>
    <div id="sched-info" style="display:none">
      <div class="field-label">Choose a time slot</div>
      <div class="schedule-pill" onclick="selectTime(this,'7:30 AM')"><div><div class="schedule-label">Morning</div><div class="schedule-time">7:30 AM</div></div><span style="color:var(--muted);font-size:12px">3 slots left</span></div>
      <div class="schedule-pill" onclick="selectTime(this,'9:00 AM')"><div><div class="schedule-label">Morning</div><div class="schedule-time">9:00 AM</div></div><span style="color:var(--muted);font-size:12px">Available</span></div>
      <div class="schedule-pill" onclick="selectTime(this,'1:00 PM')"><div><div class="schedule-label">Afternoon</div><div class="schedule-time">1:00 PM</div></div><span style="color:var(--muted);font-size:12px">Available</span></div>
      <div class="schedule-pill" onclick="selectTime(this,'6:00 PM')"><div><div class="schedule-label">Evening</div><div class="schedule-time">6:00 PM</div></div><span style="color:var(--muted);font-size:12px">2 slots left</span></div>
    </div>
    <button class="btn" onclick="searchDrivers()" style="margin-bottom:16px">Search Drivers →</button>
    <div id="drivers-section" style="display:none">
      <div class="divider"></div>
      <div class="field-label">Available Drivers — Price Comparison</div>
      <div id="drivers-list"></div>
      <button class="btn" id="confirm-btn" onclick="confirmRide()" style="display:none">Confirm Ride</button>
    </div>
  </div>

  <!-- MY RIDES SCREEN -->
  <div class="screen hidden" id="screen-rides">
    <div class="section-title">My Rides</div>
    <div class="section-sub">Your upcoming and past bookings</div>
    <div class="rides-list">
      <div class="ride-card">
        <span class="ride-status status-active">● Active</span>
        <div class="ride-price">₹85</div>
        <div class="ride-route">Main Gate → Railway Station</div>
        <div class="ride-detail">Rajesh K. · Maruti Alto · KA 03 AB 1234</div>
        <div class="progress-bar"><div class="progress-fill"></div></div>
        <div class="ride-detail">Arriving in ~4 min</div>
        <button class="btn btn-outline" style="padding:8px;font-size:12px;margin-top:10px" onclick="showScreen('track')">Track Live →</button>
      </div>
      <div class="ride-card">
        <span class="ride-status status-scheduled">◷ Scheduled</span>
        <div class="ride-price">₹120</div>
        <div class="ride-route">Hostel B → City Mall</div>
        <div class="ride-detail">Tomorrow · 9:00 AM · Shared (3 seats)</div>
      </div>
      <div class="ride-card">
        <span class="ride-status status-done">✓ Completed</span>
        <div class="ride-price">₹65</div>
        <div class="ride-route">Library Gate → Bus Stand</div>
        <div class="ride-detail">Yesterday · Priya M. · Shared</div>
      </div>
      <div class="ride-card">
        <span class="ride-status status-done">✓ Completed</span>
        <div class="ride-price">₹48</div>
        <div class="ride-route">Main Gate → Hostel C</div>
        <div class="ride-detail">2 days ago · Solo ride</div>
      </div>
    </div>
  </div>

  <!-- TRACK SCREEN -->
  <div class="screen hidden" id="screen-track">
    <div class="section-title">Live Tracking</div>
    <div class="section-sub">Main Gate → Railway Station</div>
    <div class="tracking-card">
      <div class="map-road" style="top:55%;transform:rotate(-5deg)"></div>
      <div class="map-road" style="top:40%;left:20%;right:30%;transform:rotate(10deg)"></div>
      <div class="map-dot pulse" style="left:62%;top:48%"></div>
      <div style="position:absolute;left:10%;top:50%;transform:translateY(-50%);font-size:11px;color:var(--muted)">📍 You</div>
      <div style="position:absolute;right:8%;top:40%;font-size:11px;color:var(--muted)">🏁 Dest</div>
      <div class="live-badge"><div class="live-dot"></div>Live</div>
      <div style="position:absolute;bottom:12px;left:14px;font-size:12px;color:var(--text)">Driver is <strong style="color:var(--accent)">4 min away</strong></div>
    </div>
    <div class="card">
      <div style="display:flex;align-items:center;gap:12px">
        <div class="driver-avatar" style="background:rgba(245,200,66,.15);color:var(--accent)">RK</div>
        <div style="flex:1">
          <div class="card-title">Rajesh Kumar</div>
          <div class="card-sub">⭐ 4.8 · Maruti Alto · KA 03 AB 1234</div>
        </div>
        <div style="display:flex;gap:8px">
          <div style="width:36px;height:36px;border-radius:50%;background:var(--bg3);border:1px solid var(--border);display:flex;align-items:center;justify-content:center;cursor:pointer;font-size:16px">📞</div>
          <div style="width:36px;height:36px;border-radius:50%;background:var(--bg3);border:1px solid var(--border);display:flex;align-items:center;justify-content:center;cursor:pointer;font-size:16px">💬</div>
        </div>
      </div>
    </div>
    <div class="card">
      <div class="step-row"><div class="step-dot done"></div><div style="flex:1"><div style="font-size:13px;font-weight:500">Driver accepted</div><div style="font-size:11px;color:var(--muted)">10:42 AM</div></div></div>
      <div class="step-line" style="margin-left:4px;height:10px"></div>
      <div class="step-row"><div class="step-dot done"></div><div style="flex:1"><div style="font-size:13px;font-weight:500">Driver en route to pickup</div><div style="font-size:11px;color:var(--muted)">10:43 AM</div></div></div>
      <div class="step-line" style="margin-left:4px;height:10px"></div>
      <div class="step-row"><div class="step-dot active"></div><div style="flex:1"><div style="font-size:13px;font-weight:500">Arriving at pickup — 4 min</div></div></div>
      <div class="step-line" style="margin-left:4px;height:10px"></div>
      <div class="step-row"><div class="step-dot pending"></div><div style="flex:1"><div style="font-size:13px;color:var(--muted)">Ride in progress</div></div></div>
      <div class="step-line" style="margin-left:4px;height:10px"></div>
      <div class="step-row"><div class="step-dot pending"></div><div style="flex:1"><div style="font-size:13px;color:var(--muted)">Reached destination</div></div></div>
    </div>
    <div style="display:flex;gap:10px">
      <div class="card" style="flex:1;text-align:center">
        <div style="font-size:11px;color:var(--muted)">Fare</div>
        <div style="font-family:'Syne',sans-serif;font-weight:700;font-size:20px;color:var(--accent)">₹85</div>
      </div>
      <div class="card" style="flex:1;text-align:center">
        <div style="font-size:11px;color:var(--muted)">Distance</div>
        <div style="font-family:'Syne',sans-serif;font-weight:700;font-size:20px;color:var(--text)">4.2 km</div>
      </div>
      <div class="card" style="flex:1;text-align:center">
        <div style="font-size:11px;color:var(--muted)">ETA</div>
        <div style="font-family:'Syne',sans-serif;font-weight:700;font-size:20px;color:var(--text)">~14 min</div>
      </div>
    </div>
  </div>
</div>

<script>
const drivers=[
  {name:"Rajesh K.",vehicle:"Maruti Alto",rating:"4.8",color:"#f5c842",bg:"rgba(245,200,66,.15)",price:85,shared:75,eta:"4 min",tag:"Nearest",tagClass:"tag-green"},
  {name:"Sunil M.",vehicle:"Tata Indica",rating:"4.6",color:"#60a5fa",bg:"rgba(96,165,250,.15)",price:95,shared:82,eta:"7 min",tag:"Verified",tagClass:"tag-blue"},
  {name:"Deepak P.",vehicle:"WagonR",rating:"4.9",color:"#4ade80",bg:"rgba(74,222,128,.15)",price:110,shared:90,eta:"9 min",tag:"Top Rated",tagClass:"tag-orange"},
];
let currentMode='solo',selectedDriver=null,selectedTime=null;

function showScreen(id){
  document.querySelectorAll('.screen').forEach(s=>s.classList.add('hidden'));
  document.querySelectorAll('.nav-btn').forEach(b=>b.classList.remove('active'));
  document.getElementById('screen-'+id).classList.remove('hidden');
  const idx=['book','rides','track'].indexOf(id);
  document.querySelectorAll('.nav-btn')[idx].classList.add('active');
}

function setMode(m){
  currentMode=m;
  ['solo','share','sched'].forEach(x=>{
    document.getElementById('mode-'+x).classList.toggle('active',x===m);
  });
  document.getElementById('share-info').style.display=m==='share'?'block':'none';
  document.getElementById('sched-info').style.display=m==='sched'?'block':'none';
  document.getElementById('drivers-section').style.display='none';
}

function toggleSeat(id){
  const s=document.getElementById(id);
  s.classList.toggle('taken');
  s.textContent=s.classList.contains('taken')?'👤':'➕';
}

function selectTime(el,t){
  document.querySelectorAll('.schedule-pill').forEach(p=>p.style.borderColor='var(--border)');
  el.style.borderColor='var(--accent)';
  selectedTime=t;
}

function searchDrivers(){
  const drop=document.getElementById('drop').value.trim();
  if(!drop){document.getElementById('drop').focus();document.getElementById('drop').style.borderColor='var(--red)';setTimeout(()=>document.getElementById('drop').style.borderColor='var(--border)',1500);return;}
  const sec=document.getElementById('drivers-section');
  sec.style.display='block';
  const list=document.getElementById('drivers-list');
  list.innerHTML='';
  drivers.forEach((d,i)=>{
    const price=currentMode==='share'?d.shared:d.price;
    const priceLabel=currentMode==='share'?`₹${d.shared} <span style="font-size:10px;color:var(--muted)">shared</span>`:`₹${d.price}`;
    const saving=currentMode==='share'?`<span class="tag tag-green">Save ₹${d.price-d.shared}</span>`:'';
    list.innerHTML+=`<div class="driver-card" id="dc${i}" onclick="selectDriver(${i})">
      <div class="driver-avatar" style="background:${d.bg};color:${d.color}">${d.name.split(' ').map(x=>x[0]).join('')}</div>
      <div class="driver-info">
        <div class="driver-name">${d.name}</div>
        <div class="driver-meta">⭐ ${d.rating} · ${d.vehicle} · ${d.eta} away</div>
        <span class="tag ${d.tagClass}">${d.tag}</span>${saving}
      </div>
      <div class="driver-price"><div class="price-main">${priceLabel}</div><div class="price-eta">ETA ${d.eta}</div></div>
    </div>`;
  });
}

function selectDriver(i){
  document.querySelectorAll('.driver-card').forEach(c=>c.classList.remove('selected'));
  document.getElementById('dc'+i).classList.add('selected');
  selectedDriver=i;
  document.getElementById('confirm-btn').style.display='block';
}

function confirmRide(){
  if(selectedDriver===null)return;
  document.getElementById('confirm-btn').textContent='✓ Ride Confirmed!';
  document.getElementById('confirm-btn').style.background='var(--green)';
  document.getElementById('confirm-btn').style.color='#111';
  setTimeout(()=>showScreen('track'),1200);
}
</script>
</body>
</html>
