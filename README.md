<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Blood Connect — Demo (Single Page)</title>
<style>
  :root{
    --accent:#E53935;
    --accent-2:#ff6b6b;
    --bg:#f6f6f8;
    --card:#ffffff;
    --muted:#6b7280;
    --glass: rgba(255,255,255,0.7);
  }
  *{box-sizing:border-box}
  body{
    margin:0;
    font-family:Inter, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
    background: linear-gradient(180deg,var(--bg),#fff 60%);
    color:#111827;
    -webkit-font-smoothing:antialiased;
    -moz-osx-font-smoothing:grayscale;
    padding-bottom:40px;
  }

  /* App Top bar */
  .topbar{
    background: linear-gradient(90deg,var(--accent),var(--accent-2));
    color:white;
    padding:18px;
    display:flex;
    align-items:center;
    justify-content:space-between;
    gap:12px;
    border-bottom-left-radius:20px;
    border-bottom-right-radius:20px;
    box-shadow:0 6px 18px rgba(229,57,53,0.15);
    position:sticky;
    top:0;
    z-index:10;
  }
  .brand{
    display:flex;
    gap:12px;
    align-items:center;
  }
  .logo{
    width:44px;height:44px;border-radius:10px;
    background:rgba(255,255,255,0.18); display:flex; align-items:center; justify-content:center;
    font-weight:700; font-size:18px;
  }
  .brand h1{margin:0;font-size:18px;letter-spacing:0.2px}
  .small{font-size:12px;color:rgba(255,255,255,0.95);opacity:0.95}

  /* container */
  .app{
    max-width:420px;
    margin:18px auto;
    padding:12px;
  }

  /* cards */
  .card{
    background:var(--card);
    border-radius:18px;
    padding:16px;
    margin:14px 0;
    box-shadow: 0 8px 26px rgba(15,23,42,0.06);
  }

  .title{font-size:16px;font-weight:700;margin:0 0 8px 0}
  p.lead{margin:0;color:var(--muted);font-size:13px}

  /* inputs */
  input[type="text"], input[type="tel"], select, textarea {
    width:100%;
    padding:12px 14px;
    border-radius:12px;
    border:1px solid #e6e6ea;
    margin-top:10px;
    font-size:14px;
    background:transparent;
    outline:none;
  }

  label{font-size:13px;color:var(--muted);display:block;margin-top:12px}

  /* buttons */
  .btn{
    display:inline-block;
    background:var(--accent);
    color:white;
    padding:12px 16px;
    border-radius:14px;
    text-align:center;
    width:100%;
    border:none;
    font-weight:700;
    font-size:15px;
    margin-top:12px;
    box-shadow:0 8px 18px rgba(229,57,53,0.18);
    cursor:pointer;
  }
  .btn.secondary{background:transparent;color:var(--accent);border:1px solid #ffd6d6;box-shadow:none}

  /* small UI */
  .row{display:flex;gap:10px}
  .col{flex:1}
  .muted{color:var(--muted);font-size:13px}
  .pill{display:inline-block;background:#fff7f7;border:1px solid #ffecec;color:var(--accent);padding:6px 10px;border-radius:999px;font-weight:700;font-size:13px}

  /* results */
  .donor{
    display:flex;gap:12px;align-items:center;padding:12px;border-radius:12px;border:1px dashed #f1e7e7;margin-top:10px;
  }
  .donor .avatar{width:52px;height:52px;border-radius:12px;background:linear-gradient(180deg,#fff,#ffecec);display:flex;align-items:center;justify-content:center;font-weight:700}
  .donor .meta{flex:1}
  .donor .meta h4{margin:0;font-size:15px}
  .donor .meta p{margin:4px 0 0 0;color:var(--muted);font-size:13px}

  /* notification toast */
  .toast{
    position:fixed;
    right:18px;
    bottom:18px;
    background:#111827;color:white;padding:12px 14px;border-radius:10px;box-shadow:0 12px 30px rgba(2,6,23,0.4);
    transform:translateY(40px);
    opacity:0;
    transition:all .35s ease;
    z-index:40;
    max-width:320px;
  }
  .toast.show{transform:translateY(0);opacity:1}

  /* footer small */
  .footer{text-align:center;color:var(--muted);font-size:13px;margin-top:12px}

  /* small screen bobbles */
  @media (max-width:420px){
    body{padding-bottom:80px}
    .app{padding:10px}
  }
</style>
</head>
<body>

<header class="topbar">
  <div class="brand">
    <div class="logo">BC</div>
    <div>
      <h1>Blood Connect</h1>
      <div class="small">Mobile-style single page demo</div>
    </div>
  </div>
  <div class="pill">Demo</div>
</header>

<main class="app" id="app">

  <!-- INTRO -->
  <section class="card" id="home">
    <div class="title">Emergency Blood - Connect Donors & Hospitals</div>
    <p class="lead">This single-page demo shows donor registration and hospital emergency requests in a mobile-app style UI. No server needed — data stored locally for demo.</p>
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-top:12px">
      <button class="btn" onclick="scrollToSection('register')">Register as Donor</button>
      <button class="btn secondary" onclick="scrollToSection('request')">Hospital Request</button>
    </div>
  </section>

  <!-- REGISTER -->
  <section class="card" id="register">
    <div class="title">Donor Registration</div>
    <p class="muted">Register to be listed when hospitals search for blood.</p>

    <label>Name</label>
    <input id="donor_name" type="text" placeholder="Full name">

    <div class="row">
      <div class="col">
        <label>Blood Type</label>
        <select id="donor_btype">
          <option value="">Select</option>
          <option>A+</option><option>A-</option><option>B+</option><option>B-</option>
          <option>AB+</option><option>AB-</option><option>O+</option><option>O-</option>
        </select>
      </div>
      <div class="col">
        <label>Phone</label>
        <input id="donor_phone" type="tel" placeholder="+91-XXXXXXXXXX">
      </div>
    </div>

    <label>Location (city or area)</label>
    <input id="donor_loc" type="text" placeholder="e.g., Pune, MG Road">

    <label>Availability note (optional)</label>
    <textarea id="donor_note" rows="2" placeholder="Available after 5pm / Can donate at hospital"></textarea>

    <button class="btn" onclick="registerDonor()">Save & Register</button>

    <div id="donor_saved" style="display:none;margin-top:10px;color:green">✅ Donor registered (demo only)</div>
  </section>

  <!-- REQUEST -->
  <section class="card" id="request">
    <div class="title">Hospital Emergency Request</div>
    <p class="muted">Send an emergency request. Matching donors (stored locally) will be shown below.</p>

    <label>Hospital Name</label>
    <input id="hosp_name" type="text" placeholder="Hospital / Clinic name">

    <div class="row">
      <div class="col">
        <label>Blood Type Needed</label>
        <select id="req_btype">
          <option value="">Select</option>
          <option>A+</option><option>A-</option><option>B+</option><option>B-</option>
          <option>AB+</option><option>AB-</option><option>O+</option><option>O-</option>
        </select>
      </div>
      <div class="col">
        <label>Units</label>
        <input id="req_units" type="text" placeholder="e.g., 2">
      </div>
    </div>

    <label>Location (city or area)</label>
    <input id="req_loc" type="text" placeholder="e.g., Pune, MG Road">

    <label>Urgency note</label>
    <input id="req_note" type="text" placeholder="Within 1 hour / Operation ongoing">

    <button class="btn" onclick="sendRequest()">Send Emergency Request</button>

    <div id="req_status" style="margin-top:10px"></div>
  </section>

  <!-- RESULTS -->
  <section class="card" id="results">
    <div class="title">Matching Donors (demo results)</div>
    <p class="muted">Donors that match the requested blood type and location text (simple demo logic).</p>
    <div id="matches_list" style="margin-top:10px"></div>

    <div style="margin-top:12px">
      <button class="btn secondary" onclick="clearAllData()">Clear Demo Data</button>
    </div>
  </section>

  <div class="footer">Single-file demo • No server • For college presentation</div>
</main>

<!-- toast -->
<div id="toast" class="toast">Notification</div>

<script>
  // Utility: read donors from localStorage
  function getDonors(){
    try{
      const raw = localStorage.getItem('bc_donors_demo');
      return raw ? JSON.parse(raw) : [];
    }catch(e){
      return [];
    }
  }
  function saveDonors(arr){
    localStorage.setItem('bc_donors_demo', JSON.stringify(arr));
  }

  // Register donor
  function registerDonor(){
    const name = document.getElementById('donor_name').value.trim();
    const btype = document.getElementById('donor_btype').value;
    const phone = document.getElementById('donor_phone').value.trim();
    const loc = document.getElementById('donor_loc').value.trim();
    const note = document.getElementById('donor_note').value.trim();

    if(!name || !btype || !phone || !loc){
      showToast('Please fill name, blood type, phone and location.');
      return;
    }

    const donors = getDonors();
    donors.push({
      id: 'd_' + Date.now(),
      name, btype, phone, loc, note, created: new Date().toISOString()
    });
    saveDonors(donors);

    document.getElementById('donor_saved').style.display='block';
    setTimeout(()=>document.getElementById('donor_saved').style.display='none',2500);
    clearDonorForm();
  }

  function clearDonorForm(){
    document.getElementById('donor_name').value='';
    document.getElementById('donor_btype').value='';
    document.getElementById('donor_phone').value='';
    document.getElementById('donor_loc').value='';
    document.getElementById('donor_note').value='';
  }

  // Send hospital request
  function sendRequest(){
    const hosp = document.getElementById('hosp_name').value.trim();
    const btype = document.getElementById('req_btype').value;
    const units = document.getElementById('req_units').value.trim();
    const loc = document.getElementById('req_loc').value.trim();
    const note = document.getElementById('req_note').value.trim();

    if(!hosp || !btype || !loc){
      showToast('Please fill hospital name, blood type and location.');
      return;
    }

    // Save request in demo store (not required but helpful)
    const req = {id:'r_'+Date.now(), hosp, btype, units, loc, note, time:new Date().toISOString()};
    const reqs = JSON.parse(localStorage.getItem('bc_reqs_demo')||'[]');
    reqs.unshift(req);
    localStorage.setItem('bc_reqs_demo', JSON.stringify(reqs));

    document.getElementById('req_status').innerHTML = '<span style="color:green">Request sent (demo). Searching local donors...</span>';

    // simple matching logic: blood type exact match, location substring match (case-insensitive)
    setTimeout(()=>{
      const donors = getDonors();
      const matches = donors.filter(d=>{
        try{
          const locMatch = d.loc.toLowerCase().includes(loc.toLowerCase()) || loc.toLowerCase().includes(d.loc.toLowerCase());
          return d.btype === btype && locMatch;
        }catch(e){ return false }
      });

      renderMatches(matches);

      if(matches.length>0){
        showToast('Found ' + matches.length + ' matching donor(s).');
      } else {
        showToast('No matching donors found in demo store.');
      }
      document.getElementById('req_status').innerHTML = '<span style="color:var(--muted)">Search completed. See results below.</span>';

      // Scroll to results
      scrollToSection('results');
    },700);
  }

  function renderMatches(matches){
    const el = document.getElementById('matches_list');
    el.innerHTML = '';
    if(matches.length===0){
      el.innerHTML = '<div class="muted">No donors matched. Ask donors to register (demo)</div>';
      return;
    }
    matches.forEach(d=>{
      const div = document.createElement('div');
      div.className='donor';
      div.innerHTML = `
        <div class="avatar">${d.name.split(' ').map(n=>n[0]).slice(0,2).join('').toUpperCase()}</div>
        <div class="meta">
          <h4>${d.name} <span style="font-size:12px;color:var(--muted);font-weight:600">• ${d.btype}</span></h4>
          <p>${d.phone} • ${d.loc}<br><span style="color:var(--muted);font-size:13px">${d.note||''}</span></p>
        </div>
        <div style="text-align:right">
          <button class="btn secondary" style="width:auto;padding:8px 12px;font-size:13px" onclick="contactDonor('${d.phone}')">Contact</button>
        </div>
      `;
      el.appendChild(div);
    });
  }

  function contactDonor(phone){
    // demo: show toast and copy to clipboard
    navigator.clipboard?.writeText(phone).catch(()=>{});
    showToast('Phone copied: ' + phone);
  }

  // clear demo
  function clearAllData(){
    if(!confirm('Clear all demo donors & requests?')) return;
    localStorage.removeItem('bc_donors_demo');
    localStorage.removeItem('bc_reqs_demo');
    document.getElementById('matches_list').innerHTML = '';
    showToast('Demo data cleared.');
  }

  // small helper: scroll to section
  function scrollToSection(id){
    const sec = document.getElementById(id);
    if(!sec) return;
    sec.scrollIntoView({behavior:'smooth',block:'center'});
  }

  // toast
  function showToast(text, timeout=3000){
    const t = document.getElementById('toast');
    t.textContent = text;
    t.classList.add('show');
    clearTimeout(t._tim);
    t._tim = setTimeout(()=>t.classList.remove('show'), timeout);
  }

  // on load: render any existing donors
  document.addEventListener('DOMContentLoaded', ()=>{
    const donors = getDonors();
    if(donors.length>0){
      // show last 3 donors as demo
      renderMatches(donors.slice(0,3));
    } else {
      document.getElementById('matches_list').innerHTML = '<div class="muted">No donors registered yet (demo)</div>';
    }
  });
</script>
</body>
</html>
