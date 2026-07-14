# BMI-TIP-Calculator                                                                                                                          [quick-calc-blogger-embed.html](https://github.com/user-attachments/files/29997851/quick-calc-blogger-embed.html)
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@500;600;700&family=Inter:wght@400;500;600&family=IBM+Plex+Mono:wght@500;600&display=swap" rel="stylesheet">
<style>
  :root{
    --bg:#F7F8FA;
    --ink:#14181F;
    --muted:#5B6470;
    --line:#E2E5EA;
    --surface:#FFFFFF;
    --teal:#0F6B5C;
    --teal-soft:#E6F1EE;
    --bronze:#A8672B;
    --bronze-soft:#F5EBE0;
    --danger:#B23B3B;
    --radius:14px;
  }
  *{box-sizing:border-box;}
  html,body{margin:0;padding:0;}
  body{
    background:var(--bg);
    color:var(--ink);
    font-family:'Inter',system-ui,sans-serif;
    -webkit-font-smoothing:antialiased;
    min-height:100vh;
  }
  .wrap{max-width:760px;margin:0 auto;padding:28px 20px 60px;}

  header.top{display:flex;align-items:center;justify-content:space-between;margin-bottom:28px;}
  .brand{display:flex;align-items:center;gap:10px;}
  .brand-mark{
    width:34px;height:34px;border-radius:9px;
    background:linear-gradient(135deg,var(--teal),#0a4a40);
    display:flex;align-items:center;justify-content:center;
    color:#fff;font-family:'Space Grotesk',sans-serif;font-weight:700;font-size:16px;
    flex-shrink:0;
  }
  .brand-name{font-family:'Space Grotesk',sans-serif;font-weight:700;font-size:17px;letter-spacing:-0.01em;}
  .brand-sub{font-size:11px;color:var(--muted);letter-spacing:.06em;text-transform:uppercase;margin-top:1px;}

  h1.hero{
    font-family:'Space Grotesk',sans-serif;
    font-weight:700;
    font-size:clamp(28px,5vw,40px);
    line-height:1.08;
    letter-spacing:-0.02em;
    margin:0 0 8px;
  }
  p.hero-sub{color:var(--muted);font-size:15px;margin:0 0 28px;max-width:46ch;}

  .tabs{display:flex;gap:8px;margin-bottom:20px;border-bottom:1px solid var(--line);}
  .tab{
    appearance:none;border:none;background:none;cursor:pointer;
    font-family:'Inter',sans-serif;font-weight:600;font-size:14px;
    color:var(--muted);padding:10px 4px;margin-right:20px;
    border-bottom:2.5px solid transparent;
    transition:color .15s ease, border-color .15s ease;
  }
  .tab[aria-selected="true"]{color:var(--ink);border-bottom-color:var(--teal);}
  .tab:focus-visible{outline:2px solid var(--teal);outline-offset:3px;}

  .panel{display:none;}
  .panel.active{display:block;}

  .card{
    background:var(--surface);
    border:1px solid var(--line);
    border-radius:var(--radius);
    padding:26px;
    box-shadow:0 1px 2px rgba(20,24,31,0.03);
  }

  .grid2{display:grid;grid-template-columns:1fr 1fr;gap:14px;}
  @media(max-width:560px){.grid2{grid-template-columns:1fr;}}

  label{
    display:block;font-size:12.5px;font-weight:600;color:var(--muted);
    margin-bottom:6px;letter-spacing:.02em;text-transform:uppercase;
  }
  .field{margin-bottom:16px;}
  .input-row{display:flex;gap:8px;}
  input[type="number"]{
    width:100%;
    font-family:'IBM Plex Mono',monospace;
    font-size:16px;font-weight:500;
    padding:11px 12px;
    border:1.5px solid var(--line);
    border-radius:9px;
    background:#FCFDFD;
    color:var(--ink);
    transition:border-color .15s ease;
  }
  input[type="number"]:focus{outline:none;border-color:var(--teal);}
  select{
    font-family:'Inter',sans-serif;font-size:14px;font-weight:500;
    padding:11px 10px;border:1.5px solid var(--line);border-radius:9px;
    background:#FCFDFD;color:var(--ink);
  }
  .unit-toggle{display:flex;border:1.5px solid var(--line);border-radius:9px;overflow:hidden;}
  .unit-toggle button{
    flex:1;appearance:none;border:none;background:#FCFDFD;cursor:pointer;
    font-family:'Inter',sans-serif;font-size:13px;font-weight:600;color:var(--muted);
    padding:10px 6px;
  }
  .unit-toggle button.active{background:var(--teal);color:#fff;}

  /* ---- BMI gauge (signature element) ---- */
  .gauge-wrap{display:flex;flex-direction:column;align-items:center;padding:14px 0 6px;}
  .gauge-value{
    font-family:'Space Grotesk',sans-serif;font-weight:700;
    font-size:44px;letter-spacing:-0.02em;margin-top:-64px;
  }
  .gauge-label{font-size:13px;color:var(--muted);margin-top:2px;font-weight:600;}
  .gauge-category{
    display:inline-block;margin-top:10px;padding:5px 14px;border-radius:100px;
    font-size:12.5px;font-weight:700;letter-spacing:.02em;
  }
  .gauge-range{
    font-family:'IBM Plex Mono',monospace;font-size:11.5px;color:var(--muted);margin-top:6px;
  }
  .bmi-scale{
    display:flex;justify-content:space-between;font-family:'IBM Plex Mono',monospace;
    font-size:10.5px;color:var(--muted);margin-top:10px;padding:0 6px;
  }

  /* ---- Tip receipt (signature element) ---- */
  .receipt{
    font-family:'IBM Plex Mono',monospace;
    background:var(--bronze-soft);
    border:1px dashed #D8BFA0;
    border-radius:10px;
    padding:18px 20px;
    margin-top:18px;
  }
  .receipt-row{
    display:flex;justify-content:space-between;font-size:14px;
    padding:6px 0;color:var(--ink);
  }
  .receipt-row.dotted{border-bottom:1px dotted #C9A87E;}
  .receipt-row .label{color:var(--muted);}
  .receipt-row.total{font-weight:700;font-size:16px;margin-top:4px;padding-top:10px;border-top:1px solid #C9A87E;}
  .receipt-row.total .value{color:var(--bronze);}
  .receipt-row.per-person{font-weight:600;}

  .stepper{display:flex;align-items:center;gap:10px;}
  .stepper button{
    width:38px;height:38px;border-radius:9px;border:1.5px solid var(--line);
    background:#FCFDFD;font-size:18px;font-weight:600;cursor:pointer;color:var(--ink);
    flex-shrink:0;
  }
  .stepper button:active{background:var(--teal-soft);}
  .stepper .val{
    font-family:'IBM Plex Mono',monospace;font-weight:600;font-size:16px;
    min-width:34px;text-align:center;
  }

  .tip-presets{display:flex;gap:8px;margin-bottom:14px;flex-wrap:wrap;}
  .tip-presets button{
    appearance:none;border:1.5px solid var(--line);background:#FCFDFD;border-radius:8px;
    padding:8px 14px;font-family:'IBM Plex Mono',monospace;font-weight:600;font-size:14px;
    cursor:pointer;color:var(--ink);
  }
  .tip-presets button.active{background:var(--bronze);border-color:var(--bronze);color:#fff;}

  .info{
    margin-top:34px;padding-top:22px;border-top:1px solid var(--line);
    color:var(--muted);font-size:13.5px;line-height:1.65;
  }
  .info h2{font-family:'Space Grotesk',sans-serif;font-size:16px;color:var(--ink);margin:0 0 8px;}
  .info p{margin:0 0 10px;}

  .ad-slot{
    margin:26px 0;min-height:90px;border:1px dashed var(--line);border-radius:10px;
    display:flex;align-items:center;justify-content:center;color:#B7BEC7;font-size:12px;
    font-family:'IBM Plex Mono',monospace;letter-spacing:.03em;
  }

  footer{text-align:center;color:var(--muted);font-size:12px;margin-top:36px;}
</style>
<div class="wrap">

  <header class="top">
    <div class="brand">
      <div class="brand-mark">Q</div>
      <div>
        <div class="brand-name">Quick Calc</div>
        <div class="brand-sub">Instant &amp; free</div>
      </div>
    </div>
  </header>

  <h1 class="hero">Two numbers you actually need, right now.</h1>
  <p class="hero-sub">No sign-up, no app download. Type a number, get an answer.</p>

  <div class="tabs" role="tablist">
    <button class="tab" id="tab-bmi" role="tab" aria-selected="true" aria-controls="panel-bmi">BMI Calculator</button>
    <button class="tab" id="tab-tip" role="tab" aria-selected="false" aria-controls="panel-tip">Tip Calculator</button>
  </div>

  <!-- ============ BMI PANEL ============ -->
  <section class="panel active" id="panel-bmi" role="tabpanel" aria-labelledby="tab-bmi">
    <div class="card">
      <div class="unit-toggle" style="margin-bottom:18px;max-width:220px;">
        <button type="button" id="bmi-unit-metric" class="active">Metric</button>
        <button type="button" id="bmi-unit-imperial">Imperial</button>
      </div>

      <div class="grid2" id="bmi-metric-fields">
        <div class="field">
          <label for="bmi-height-cm">Height (cm)</label>
          <input type="number" id="bmi-height-cm" placeholder="170" inputmode="decimal">
        </div>
        <div class="field">
          <label for="bmi-weight-kg">Weight (kg)</label>
          <input type="number" id="bmi-weight-kg" placeholder="65" inputmode="decimal">
        </div>
      </div>

      <div class="grid2" id="bmi-imperial-fields" style="display:none;">
        <div class="field">
          <label for="bmi-height-ft">Height (ft + in)</label>
          <div class="input-row">
            <input type="number" id="bmi-height-ft" placeholder="5" inputmode="decimal">
            <input type="number" id="bmi-height-in" placeholder="7" inputmode="decimal">
          </div>
        </div>
        <div class="field">
          <label for="bmi-weight-lb">Weight (lb)</label>
          <input type="number" id="bmi-weight-lb" placeholder="143" inputmode="decimal">
        </div>
      </div>

      <div class="gauge-wrap">
        <svg id="gauge-svg" width="220" height="130" viewBox="0 0 220 130">
          <path d="M 15 115 A 95 95 0 0 1 205 115" fill="none" stroke="#E2E5EA" stroke-width="14" stroke-linecap="round"/>
          <path id="gauge-arc" d="M 15 115 A 95 95 0 0 1 205 115" fill="none" stroke="#0F6B5C" stroke-width="14" stroke-linecap="round" stroke-dasharray="298" stroke-dashoffset="298"/>
          <circle id="gauge-needle" cx="15" cy="115" r="6" fill="#14181F"/>
        </svg>
        <div class="gauge-value" id="bmi-value">—</div>
        <div class="gauge-label">Body Mass Index</div>
        <div class="gauge-category" id="bmi-category">Enter your numbers</div>
        <div class="gauge-range" id="bmi-range"></div>
        <div class="bmi-scale"><span>15</span><span>18.5</span><span>25</span><span>30</span><span>40</span></div>
      </div>
    </div>

    <div class="ad-slot">Ad slot — paste your AdSense unit code here</div>

    <div class="info">
      <h2>What is BMI?</h2>
      <p>Body Mass Index (BMI) is a simple screening measure that divides your weight by the square of your height. It's used as a quick, population-level indicator — not a diagnosis — of whether your weight falls in a typical range for your height.</p>
      <p>The categories most health bodies use are: under 18.5 (underweight), 18.5–24.9 (typical range), 25–29.9 (above typical range), and 30+ (well above typical range). BMI doesn't account for muscle mass, bone density, age, or sex, so athletes and older adults in particular should treat it as one data point, not the full picture. For a complete health assessment, talk to a doctor.</p>
    </div>
  </section>

  <!-- ============ TIP PANEL ============ -->
  <section class="panel" id="panel-tip" role="tabpanel" aria-labelledby="tab-tip">
    <div class="card">
      <div class="field">
        <label for="tip-bill">Bill amount</label>
        <input type="number" id="tip-bill" placeholder="0.00" inputmode="decimal">
      </div>

      <label>Tip percentage</label>
      <div class="tip-presets" id="tip-presets">
        <button type="button" data-pct="10">10%</button>
        <button type="button" data-pct="15" class="active">15%</button>
        <button type="button" data-pct="18">18%</button>
        <button type="button" data-pct="20">20%</button>
        <button type="button" data-pct="25">25%</button>
      </div>

      <div class="field">
        <label for="tip-custom">Or enter a custom %</label>
        <input type="number" id="tip-custom" placeholder="15" inputmode="decimal">
      </div>

      <div class="field" style="margin-top:20px;">
        <label>Split between</label>
        <div class="stepper">
          <button type="button" id="split-minus">−</button>
          <span class="val" id="split-count">1</span>
          <button type="button" id="split-plus">+</button>
          <span style="color:var(--muted);font-size:13px;">people</span>
        </div>
      </div>

      <div class="receipt">
        <div class="receipt-row dotted"><span class="label">Bill</span><span class="value" id="r-bill">$0.00</span></div>
        <div class="receipt-row dotted"><span class="label">Tip (<span id="r-pct">15</span>%)</span><span class="value" id="r-tip">$0.00</span></div>
        <div class="receipt-row total"><span class="label">Total</span><span class="value" id="r-total">$0.00</span></div>
        <div class="receipt-row per-person"><span class="label">Per person</span><span class="value" id="r-per">$0.00</span></div>
      </div>
    </div>

    <div class="ad-slot">Ad slot — paste your AdSense unit code here</div>

    <div class="info">
      <h2>How much should you tip?</h2>
      <p>In the US, 15–20% of the pre-tax bill is the standard range for sit-down restaurant service, with 18–20% typical for good service. Many countries handle tipping very differently — some include service in the bill already, others consider tipping unusual — so it's worth checking local norms if you're traveling.</p>
      <p>Splitting the tip evenly is simplest for groups, though some people prefer splitting only the bill evenly and calculating tip separately based on total spend.</p>
    </div>
  </section>

  <footer>Quick Calc — free forever. No account needed.</footer>
</div>

<script>
(function(){
  // ---------- Tabs ----------
  var tabBmi = document.getElementById('tab-bmi');
  var tabTip = document.getElementById('tab-tip');
  var panelBmi = document.getElementById('panel-bmi');
  var panelTip = document.getElementById('panel-tip');

  function selectTab(which){
    var bmiOn = which === 'bmi';
    tabBmi.setAttribute('aria-selected', bmiOn ? 'true':'false');
    tabTip.setAttribute('aria-selected', bmiOn ? 'false':'true');
    panelBmi.classList.toggle('active', bmiOn);
    panelTip.classList.toggle('active', !bmiOn);
  }
  tabBmi.addEventListener('click', function(){ selectTab('bmi'); });
  tabTip.addEventListener('click', function(){ selectTab('tip'); });

  // ---------- BMI ----------
  var unitMetricBtn = document.getElementById('bmi-unit-metric');
  var unitImperialBtn = document.getElementById('bmi-unit-imperial');
  var metricFields = document.getElementById('bmi-metric-fields');
  var imperialFields = document.getElementById('bmi-imperial-fields');
  var isMetric = true;

  unitMetricBtn.addEventListener('click', function(){
    isMetric = true;
    unitMetricBtn.classList.add('active'); unitImperialBtn.classList.remove('active');
    metricFields.style.display=''; imperialFields.style.display='none';
    computeBmi();
  });
  unitImperialBtn.addEventListener('click', function(){
    isMetric = false;
    unitImperialBtn.classList.add('active'); unitMetricBtn.classList.remove('active');
    metricFields.style.display='none'; imperialFields.style.display='';
    computeBmi();
  });

  var bmiValueEl = document.getElementById('bmi-value');
  var bmiCategoryEl = document.getElementById('bmi-category');
  var bmiRangeEl = document.getElementById('bmi-range');
  var gaugeArc = document.getElementById('gauge-arc');
  var gaugeNeedle = document.getElementById('gauge-needle');
  var ARC_LEN = 298;

  function categoryFor(bmi){
    if (bmi < 18.5) return {label:'Underweight', range:'Below 18.5', color:'#2E7BB5', bg:'#E4F0F8'};
    if (bmi < 25) return {label:'Normal weight', range:'18.5 – 24.9', color:'#0F6B5C', bg:'#E6F1EE'};
    if (bmi < 30) return {label:'Overweight', range:'25 – 29.9', color:'#B08324', bg:'#FBF1DD'};
    return {label:'Obese', range:'30 and above', color:'#B23B3B', bg:'#FAE6E6'};
  }

  function computeBmi(){
    var heightM, weightKg;
    if (isMetric){
      var cm = parseFloat(document.getElementById('bmi-height-cm').value);
      var kg = parseFloat(document.getElementById('bmi-weight-kg').value);
      if (!cm || !kg){ resetGauge(); return; }
      heightM = cm/100; weightKg = kg;
    } else {
      var ft = parseFloat(document.getElementById('bmi-height-ft').value) || 0;
      var inch = parseFloat(document.getElementById('bmi-height-in').value) || 0;
      var lb = parseFloat(document.getElementById('bmi-weight-lb').value);
      var totalIn = ft*12 + inch;
      if (!totalIn || !lb){ resetGauge(); return; }
      heightM = totalIn * 0.0254; weightKg = lb * 0.453592;
    }
    var bmi = weightKg / (heightM*heightM);
    if (!isFinite(bmi) || bmi <= 0){ resetGauge(); return; }

    bmiValueEl.textContent = bmi.toFixed(1);
    var cat = categoryFor(bmi);
    bmiCategoryEl.textContent = cat.label;
    bmiCategoryEl.style.color = cat.color;
    bmiCategoryEl.style.background = cat.bg;
    bmiRangeEl.textContent = cat.range;

    // map bmi 15-40 to arc fill 0-1
    var pct = Math.min(Math.max((bmi-15)/(40-15),0),1);
    var offset = ARC_LEN * (1-pct);
    gaugeArc.style.stroke = cat.color;
    gaugeArc.setAttribute('stroke-dashoffset', offset);

    // Needle position: the arc runs from (cx-r, cy) at pct=0, over the top,
    // to (cx+r, cy) at pct=1 — same direction the colored stroke reveals in,
    // so the dot always sits exactly at the tip of the colored arc.
    var cx = 110, cy = 115, r = 95;
    var theta = Math.PI * (1 - pct);
    var px = cx + r * Math.cos(theta);
    var py = cy - r * Math.sin(theta);
    gaugeNeedle.setAttribute('cx', px);
    gaugeNeedle.setAttribute('cy', py);
    gaugeNeedle.setAttribute('fill', cat.color);
  }

  function resetGauge(){
    bmiValueEl.textContent = '—';
    bmiCategoryEl.textContent = 'Enter your numbers';
    bmiCategoryEl.style.color = '#5B6470';
    bmiCategoryEl.style.background = 'transparent';
    bmiRangeEl.textContent = '';
    gaugeArc.setAttribute('stroke-dashoffset', ARC_LEN);
    gaugeNeedle.setAttribute('cx', 15);
    gaugeNeedle.setAttribute('cy', 115);
  }

  ['bmi-height-cm','bmi-weight-kg','bmi-height-ft','bmi-height-in','bmi-weight-lb'].forEach(function(id){
    document.getElementById(id).addEventListener('input', computeBmi);
  });

  // ---------- Tip ----------
  var billInput = document.getElementById('tip-bill');
  var customInput = document.getElementById('tip-custom');
  var presetBtns = document.querySelectorAll('#tip-presets button');
  var splitCount = 1;
  var currentPct = 15;

  presetBtns.forEach(function(btn){
    btn.addEventListener('click', function(){
      presetBtns.forEach(function(b){ b.classList.remove('active'); });
      btn.classList.add('active');
      currentPct = parseFloat(btn.getAttribute('data-pct'));
      customInput.value = '';
      computeTip();
    });
  });
  customInput.addEventListener('input', function(){
    var v = parseFloat(customInput.value);
    if (v >= 0){
      presetBtns.forEach(function(b){ b.classList.remove('active'); });
      currentPct = v;
      computeTip();
    }
  });
  billInput.addEventListener('input', computeTip);

  document.getElementById('split-minus').addEventListener('click', function(){
    splitCount = Math.max(1, splitCount-1);
    document.getElementById('split-count').textContent = splitCount;
    computeTip();
  });
  document.getElementById('split-plus').addEventListener('click', function(){
    splitCount = Math.min(50, splitCount+1);
    document.getElementById('split-count').textContent = splitCount;
    computeTip();
  });

  function fmt(n){ return '$' + n.toFixed(2); }

  function computeTip(){
    var bill = parseFloat(billInput.value) || 0;
    var pct = isFinite(currentPct) ? currentPct : 0;
    var tip = bill * (pct/100);
    var total = bill + tip;
    var per = total / splitCount;

    document.getElementById('r-bill').textContent = fmt(bill);
    document.getElementById('r-pct').textContent = pct;
    document.getElementById('r-tip').textContent = fmt(tip);
    document.getElementById('r-total').textContent = fmt(total);
    document.getElementById('r-per').textContent = fmt(per);
  }

  resetGauge();
  computeTip();
})();
</script>
