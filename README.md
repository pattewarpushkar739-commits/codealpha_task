# codealpha_task
Web Devlopment Internship First Task 1 - Age Calculator
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Age Calculator</title>
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700;900&family=DM+Mono:wght@300;400;500&display=swap" rel="stylesheet"/>
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --bg:        #0d0d0d;
      --surface:   #141414;
      --border:    #2a2a2a;
      --accent:    #e8c97e;
      --accent2:   #c9a84c;
      --text:      #f0ece2;
      --muted:     #6b6660;
      --error:     #e07070;
      --success:   #70c99a;
      --radius:    12px;
    }

    body {
      min-height: 100vh;
      background: var(--bg);
      color: var(--text);
      font-family: 'DM Mono', monospace;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 24px;
      background-image:
        radial-gradient(ellipse 80% 60% at 50% -10%, rgba(232,201,126,.10) 0%, transparent 65%),
        repeating-linear-gradient(0deg, transparent, transparent 39px, rgba(255,255,255,.02) 40px),
        repeating-linear-gradient(90deg, transparent, transparent 39px, rgba(255,255,255,.02) 40px);
    }

    /* ─── Card ─────────────────────────────────── */
    .card {
      width: 100%;
      max-width: 540px;
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 20px;
      padding: 48px 44px;
      box-shadow: 0 32px 80px rgba(0,0,0,.6), 0 0 0 1px rgba(232,201,126,.06);
      animation: rise .6s cubic-bezier(.22,.61,.36,1) both;
    }

    @keyframes rise {
      from { opacity:0; transform: translateY(28px); }
      to   { opacity:1; transform: translateY(0); }
    }

    /* ─── Header ───────────────────────────────── */
    .header { text-align: center; margin-bottom: 40px; }

    .header .icon {
      display: inline-flex;
      align-items: center; justify-content: center;
      width: 56px; height: 56px;
      border-radius: 50%;
      background: linear-gradient(135deg, var(--accent2), var(--accent));
      margin-bottom: 18px;
      font-size: 24px;
      box-shadow: 0 8px 24px rgba(232,201,126,.25);
    }

    .header h1 {
      font-family: 'Playfair Display', serif;
      font-size: 2rem;
      font-weight: 900;
      letter-spacing: -0.5px;
      color: var(--text);
    }

    .header p {
      font-size: .78rem;
      color: var(--muted);
      margin-top: 6px;
      letter-spacing: .04em;
    }

    /* ─── Divider ──────────────────────────────── */
    .divider {
      display: flex; align-items: center; gap: 12px;
      margin: 32px 0;
    }
    .divider::before, .divider::after {
      content:''; flex:1; height:1px; background: var(--border);
    }
    .divider span {
      font-size: .7rem; color: var(--muted); letter-spacing:.1em; text-transform:uppercase;
    }

    /* ─── Form ─────────────────────────────────── */
    .form-label {
      display: block;
      font-size: .7rem;
      letter-spacing: .12em;
      text-transform: uppercase;
      color: var(--muted);
      margin-bottom: 10px;
    }

    .dob-row {
      display: grid;
      grid-template-columns: 1fr 1fr 1.4fr;
      gap: 12px;
      margin-bottom: 28px;
    }

    .field { display: flex; flex-direction: column; }

    .field label {
      font-size: .65rem;
      letter-spacing: .1em;
      text-transform: uppercase;
      color: var(--muted);
      margin-bottom: 6px;
    }

    .field input, .field select {
      background: #1c1c1c;
      border: 1.5px solid var(--border);
      border-radius: var(--radius);
      color: var(--text);
      font-family: 'DM Mono', monospace;
      font-size: .95rem;
      padding: 13px 14px;
      outline: none;
      transition: border-color .2s, box-shadow .2s;
      width: 100%;
      -webkit-appearance: none;
    }

    .field input::placeholder { color: #3a3a3a; }

    .field input:focus, .field select:focus {
      border-color: var(--accent);
      box-shadow: 0 0 0 3px rgba(232,201,126,.12);
    }

    .field input.error { border-color: var(--error); }

    /* hide number spinners */
    .field input[type=number]::-webkit-inner-spin-button,
    .field input[type=number]::-webkit-outer-spin-button { -webkit-appearance:none; }

    /* ─── Today reference ──────────────────────── */
    .today-row {
      display: flex; align-items: center; justify-content: space-between;
      background: #191919;
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 12px 16px;
      margin-bottom: 28px;
    }
    .today-row .lbl { font-size:.68rem; color:var(--muted); letter-spacing:.08em; text-transform:uppercase; }
    .today-row .val { font-size:.88rem; color:var(--accent); letter-spacing:.04em; }

    /* ─── Button ───────────────────────────────── */
    .btn {
      width: 100%;
      padding: 15px;
      background: linear-gradient(135deg, var(--accent2), var(--accent));
      color: #0d0d0d;
      border: none;
      border-radius: var(--radius);
      font-family: 'DM Mono', monospace;
      font-size: .88rem;
      font-weight: 500;
      letter-spacing: .12em;
      text-transform: uppercase;
      cursor: pointer;
      transition: transform .15s, box-shadow .15s, opacity .15s;
      box-shadow: 0 4px 20px rgba(232,201,126,.22);
    }
    .btn:hover { transform: translateY(-1px); box-shadow: 0 8px 28px rgba(232,201,126,.32); }
    .btn:active { transform: translateY(0); opacity: .9; }

    /* ─── Error message ────────────────────────── */
    .error-msg {
      display: none;
      margin-top: 14px;
      padding: 12px 16px;
      background: rgba(224,112,112,.08);
      border: 1px solid rgba(224,112,112,.3);
      border-radius: var(--radius);
      color: var(--error);
      font-size: .8rem;
      letter-spacing: .03em;
      text-align: center;
    }
    .error-msg.show { display: block; animation: shake .35s ease; }

    @keyframes shake {
      0%,100%{transform:translateX(0)}
      20%{transform:translateX(-6px)}
      40%{transform:translateX(6px)}
      60%{transform:translateX(-4px)}
      80%{transform:translateX(4px)}
    }

    /* ─── Result ───────────────────────────────── */
    .result {
      display: none;
      margin-top: 32px;
      animation: reveal .5s cubic-bezier(.22,.61,.36,1) both;
    }
    .result.show { display: block; }

    @keyframes reveal {
      from { opacity:0; transform:translateY(16px); }
      to   { opacity:1; transform:translateY(0); }
    }

    .result-header {
      text-align: center;
      font-family: 'Playfair Display', serif;
      font-size: .8rem;
      color: var(--muted);
      letter-spacing: .14em;
      text-transform: uppercase;
      margin-bottom: 20px;
    }

    .result-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 12px;
      margin-bottom: 20px;
    }

    .result-box {
      background: #191919;
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 22px 12px;
      text-align: center;
      position: relative;
      overflow: hidden;
      transition: border-color .2s;
    }
    .result-box::before {
      content:'';
      position:absolute; top:0; left:0; right:0; height:2px;
      background: linear-gradient(90deg, transparent, var(--accent), transparent);
      opacity: 0;
      transition: opacity .3s;
    }
    .result-box:hover { border-color: var(--accent2); }
    .result-box:hover::before { opacity:1; }

    .result-box .num {
      font-family: 'Playfair Display', serif;
      font-size: 2.4rem;
      font-weight: 900;
      color: var(--accent);
      line-height: 1;
      display: block;
      counter-reset: none;
    }

    .result-box .unit {
      font-size: .65rem;
      color: var(--muted);
      letter-spacing: .14em;
      text-transform: uppercase;
      margin-top: 6px;
      display: block;
    }

    /* total days card */
    .result-total {
      display: flex;
      align-items: center;
      justify-content: space-between;
      background: #191919;
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 16px 20px;
      margin-bottom: 10px;
    }
    .result-total .lbl {
      font-size:.68rem; color:var(--muted); letter-spacing:.1em; text-transform:uppercase;
    }
    .result-total .val {
      font-family:'Playfair Display',serif;
      font-size:1.3rem; font-weight:700; color:var(--text);
    }

    /* next birthday */
    .result-next {
      display: flex;
      align-items: center;
      justify-content: space-between;
      background: rgba(232,201,126,.04);
      border: 1px solid rgba(232,201,126,.18);
      border-radius: var(--radius);
      padding: 14px 20px;
    }
    .result-next .lbl {
      font-size:.68rem; color:var(--accent2); letter-spacing:.1em; text-transform:uppercase;
    }
    .result-next .val {
      font-size:.88rem; color:var(--accent); letter-spacing:.04em;
    }

    /* ─── Reset btn ────────────────────────────── */
    .btn-reset {
      width:100%; margin-top:20px;
      padding:11px;
      background:transparent;
      border:1px solid var(--border);
      border-radius:var(--radius);
      color:var(--muted);
      font-family:'DM Mono',monospace;
      font-size:.75rem;
      letter-spacing:.1em;
      text-transform:uppercase;
      cursor:pointer;
      transition: border-color .2s, color .2s;
    }
    .btn-reset:hover { border-color:var(--accent2); color:var(--accent2); }

    /* ─── Responsive ────────────────────────────── */
    @media(max-width:480px){
      .card { padding:36px 24px; }
      .result-grid { grid-template-columns:repeat(3,1fr); }
      .result-box .num { font-size:1.8rem; }
    }
  </style>
</head>
<body>

<div class="card">
  <!-- Header -->
  <div class="header">
    <div class="icon">⧖</div>
    <h1>Age Calculator</h1>
    <p>Enter your date of birth to calculate your exact age</p>
  </div>

  <!-- Today Reference -->
  <div class="today-row">
    <span class="lbl">Today's Date</span>
    <span class="val" id="todayDisplay">—</span>
  </div>

  <!-- Form -->
  <label class="form-label">Date of Birth</label>
  <div class="dob-row">
    <div class="field">
      <label for="dayInput">Day</label>
      <input id="dayInput" type="number" placeholder="DD" min="1" max="31"/>
    </div>
    <div class="field">
      <label for="monthInput">Month</label>
      <input id="monthInput" type="number" placeholder="MM" min="1" max="12"/>
    </div>
    <div class="field">
      <label for="yearInput">Year</label>
      <input id="yearInput" type="number" placeholder="YYYY" min="1900"/>
    </div>
  </div>

  <button class="btn" onclick="calculateAge()">Calculate Age →</button>
  <div class="error-msg" id="errorMsg"></div>

  <!-- Result -->
  <div class="result" id="result">
    <div class="divider"><span>Your Age</span></div>
    <div class="result-grid">
      <div class="result-box">
        <span class="num" id="resYears">0</span>
        <span class="unit">Years</span>
      </div>
      <div class="result-box">
        <span class="num" id="resMonths">0</span>
        <span class="unit">Months</span>
      </div>
      <div class="result-box">
        <span class="num" id="resDays">0</span>
        <span class="unit">Days</span>
      </div>
    </div>
    <div class="result-total">
      <span class="lbl">Total Days Lived</span>
      <span class="val" id="resTotalDays">—</span>
    </div>
    <div class="result-next">
      <span class="lbl">🎂 Next Birthday</span>
      <span class="val" id="resNextBday">—</span>
    </div>
    <button class="btn-reset" onclick="resetForm()">↺ Reset</button>
  </div>
</div>

<script>
  /* ── Helpers ─────────────────────────────────────── */
  const $ = id => document.getElementById(id);

  const MONTHS = [
    'January','February','March','April','May','June',
    'July','August','September','October','November','December'
  ];
  const DAYS_SHORT = ['Sun','Mon','Tue','Wed','Thu','Fri','Sat'];

  function pad(n){ return String(n).padStart(2,'0'); }

  function daysInMonth(month, year){
    // month is 1-based
    return new Date(year, month, 0).getDate();
  }

  /* ── Display today ───────────────────────────────── */
  function showToday(){
    const t = new Date();
    $('todayDisplay').textContent =
      `${DAYS_SHORT[t.getDay()]}, ${pad(t.getDate())} ${MONTHS[t.getMonth()]} ${t.getFullYear()}`;
  }
  showToday();

  /* ── Validation ──────────────────────────────────── */
  function showError(msg){
    const el = $('errorMsg');
    el.textContent = msg;
    el.classList.remove('show');
    void el.offsetWidth;          // reflow → re-trigger shake
    el.classList.add('show');
    [$('dayInput'), $('monthInput'), $('yearInput')].forEach(i => i.classList.add('error'));
    $('result').classList.remove('show');
  }

  function clearErrors(){
    $('errorMsg').classList.remove('show');
    [$('dayInput'), $('monthInput'), $('yearInput')].forEach(i => i.classList.remove('error'));
  }

  function validate(day, month, year){
    if(!day || !month || !year)     return 'Please fill in all three fields.';
    if(month < 1 || month > 12)     return 'Month must be between 1 and 12.';
    if(year < 1900)                 return 'Year must be 1900 or later.';
    if(year > new Date().getFullYear()) return 'Birth year cannot be in the future.';

    const maxDay = daysInMonth(month, year);
    if(day < 1 || day > maxDay)
      return `Day must be between 1 and ${maxDay} for the given month.`;

    const dob = new Date(year, month - 1, day);
    if(dob > new Date())            return 'Date of birth cannot be in the future.';

    return null; // valid
  }

  /* ── Core calculation ────────────────────────────── */
  function calculateAge(){
    clearErrors();

    const day   = parseInt($('dayInput').value,  10);
    const month = parseInt($('monthInput').value, 10);
    const year  = parseInt($('yearInput').value,  10);

    const err = validate(day, month, year);
    if(err){ showError(err); return; }

    const dob   = new Date(year, month - 1, day);
    const today = new Date();
    today.setHours(0,0,0,0);

    /* ── Years, Months, Days ── */
    let ageY = today.getFullYear() - dob.getFullYear();
    let ageM = today.getMonth()    - dob.getMonth();
    let ageD = today.getDate()     - dob.getDate();

    if(ageD < 0){
      ageM--;
      // borrow days from the previous month
      const prevMonth = new Date(today.getFullYear(), today.getMonth(), 0);
      ageD += prevMonth.getDate();
    }
    if(ageM < 0){
      ageY--;
      ageM += 12;
    }

    /* ── Total days lived ── */
    const msPerDay   = 1000 * 60 * 60 * 24;
    const totalDays  = Math.floor((today - dob) / msPerDay);

    /* ── Next birthday ── */
    const nextBday = new Date(today.getFullYear(), dob.getMonth(), dob.getDate());
    if(nextBday <= today) nextBday.setFullYear(today.getFullYear() + 1);
    const daysUntil = Math.ceil((nextBday - today) / msPerDay);
    const nextStr   = daysUntil === 0
      ? '🎉 Today!'
      : `${MONTHS[nextBday.getMonth()]} ${nextBday.getDate()}, ${nextBday.getFullYear()} (in ${daysUntil} day${daysUntil!==1?'s':''})`;

    /* ── Render ── */
    $('resYears').textContent    = ageY;
    $('resMonths').textContent   = ageM;
    $('resDays').textContent     = ageD;
    $('resTotalDays').textContent = totalDays.toLocaleString();
    $('resNextBday').textContent  = nextStr;

    $('result').classList.remove('show');
    void $('result').offsetWidth;
    $('result').classList.add('show');
  }

  /* ── Reset ───────────────────────────────────────── */
  function resetForm(){
    ['dayInput','monthInput','yearInput'].forEach(id => $( id).value = '');
    clearErrors();
    $('result').classList.remove('show');
    $('dayInput').focus();
  }

  /* ── Enter key support ───────────────────────────── */
  document.addEventListener('keydown', e => {
    if(e.key === 'Enter') calculateAge();
  });

  /* ── Allow only numeric input ────────────────────── */
  ['dayInput','monthInput','yearInput'].forEach(id => {
    $(id).addEventListener('input', function(){
      this.value = this.value.replace(/[^0-9]/g,'');
    });
  });
</script>
</body>
</html>
