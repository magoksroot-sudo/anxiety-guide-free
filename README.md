<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>CalmNow — Free Anxiety Guide</title>
  <style>
    :root{--bg:#0f1724;--card:#0b1220;--accent:#6ee7b7;--muted:#94a3b8}
    *{box-sizing:border-box}
    body{margin:0;font-family:Inter,system-ui,Segoe UI,Roboto,'Helvetica Neue',Arial;background:linear-gradient(180deg,#071023 0%, #081226 60%);color:#e6eef6;min-height:100vh;display:flex;align-items:center;justify-content:center;padding:40px}
    .wrap{max-width:980px;width:100%;display:grid;grid-template-columns:1fr 420px;gap:32px}
    .hero{padding:36px;border-radius:20px;background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));box-shadow:0 8px 30px rgba(2,6,23,.6)}
    h1{font-size:32px;margin:0 0 12px}
    p.lead{color:var(--muted);line-height:1.5;margin:0 0 20px}
    .features{display:flex;gap:12px;margin-top:18px}
    .feature{background:rgba(255,255,255,0.02);padding:12px;border-radius:12px;flex:1}
    .card{padding:26px;border-radius:16px;background:linear-gradient(180deg, rgba(255,255,255,0.015), rgba(255,255,255,0.01));}
    .form-title{font-weight:600;margin-bottom:6px}
    input[type=email]{width:100%;padding:12px;border-radius:10px;border:1px solid rgba(255,255,255,0.06);background:transparent;color:inherit;font-size:15px}
    button{margin-top:12px;width:100%;padding:12px;border-radius:10px;border:0;background:linear-gradient(90deg,var(--accent),#34d399);color:#052018;font-weight:700;cursor:pointer}
    small{color:var(--muted)}
    .success{display:none;padding:12px;border-radius:10px;background:#052018;color:var(--accent);margin-top:12px}
    .legal{font-size:12px;color:var(--muted);margin-top:10px}
    .hero-visual{display:flex;flex-direction:column;gap:10px}
    .preview{background:linear-gradient(90deg,#071733, #07233a);padding:14px;border-radius:12px;border:1px solid rgba(255,255,255,0.03)}
    .pdf-card{height:120px;border-radius:10px;display:flex;align-items:center;justify-content:center;flex-direction:column}
    footer{grid-column:1/-1;margin-top:18px;color:var(--muted);font-size:13px;text-align:center}
    @media (max-width:940px){.wrap{grid-template-columns:1fr;gap:18px;padding:0}body{padding:20px}}
  </style>
</head>
<body>
  <main class="wrap">
    <section class="hero card">
      <h1>Free Guide: Simple Tools to Reduce Anxiety</h1>
      <p class="lead">Short, science-backed strategies you can use today to feel calmer, sleep better, and take back control. Designed for busy people — quick reads, practical exercises, and calming practices.</p>
      <div class="features">
        <div class="feature">
          <strong>Quick exercises</strong>
          <div style="color:var(--muted);font-size:13px">3–10 minute practices you can do anywhere</div>
        </div>
        <div class="feature">
          <strong>Evidence-based</strong>
          <div style="color:var(--muted);font-size:13px">Tools grounded in CBT and mindfulness</div>
        </div>
        <div class="feature">
          <strong>No spam</strong>
          <div style="color:var(--muted);font-size:13px">Just the guide and occasional useful tips</div>
        </div>
      </div>
      <div style="margin-top:22px;display:flex;gap:14px;align-items:center">
        <img src="data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='88' height='88'><rect rx='14' width='88' height='88' fill='%236ee7b7'/><text x='50%' y='54%' dominant-baseline='middle' text-anchor='middle' font-size='32' fill='%23051f12' font-family='Arial'>🙂</text></svg>" alt="icon" style="width:88px;height:88px;border-radius:12px;"/>
        <div>
          <div style="font-weight:700">Instant PDF</div>
          <div style="color:var(--muted);font-size:13px">Enter your email and we'll send the guide immediately — plus downloadable PDF right away.</div>
        </div>
      </div>
    </section>

    <aside class="card">
      <div class="form-title">Get the free guide</div>
      <form id="signupForm">
        <label for="email" style="display:block;margin-bottom:8px;color:var(--muted);font-size:13px">Email address</label>
        <input type="email" id="email" name="email" placeholder="you@example.com" required />
        <button type="submit" id="submitBtn">Send me the guide</button>
        <div id="success" class="success">Thanks — you are being redirected to the guide now.</div>
        <div class="legal">We respect your privacy. Unsubscribe any time.</div>
      </form>

      <div style="margin-top:18px">
        <div style="font-weight:700;margin-bottom:8px">Preview</div>
        <div class="preview pdf-card">
          <div style="font-size:16px">Anxiety Guide — Large Print</div>
          <div style="color:var(--muted);font-size:13px">From Moodcafe • Practical steps • Breathing • Night routine</div>
        </div>
      </div>
    </aside>

    <footer>
      Built with care • Emails are stored via Google Apps Script webhook.
    </footer>

  </main>

  <script>
    const SERVER_ENDPOINT = 'https://script.google.com/macros/s/AKfycbzpVNbxWsTtIEV0fuR6jsCIQDsha-BOt9Aa-Mgn_UhjVytbTC8cu-UkcC22-xMOfjA/exec';
    const PDF_URL = 'https://www.moodcafe.co.uk/media/43771/understanding-anxiety_large-print.pdf';

    const form = document.getElementById('signupForm');
    const emailInput = document.getElementById('email');
    const submitBtn = document.getElementById('submitBtn');
    const successBox = document.getElementById('success');

    form.addEventListener('submit', async (e) => {
      e.preventDefault();
      const email = emailInput.value.trim();
      if (!email) return;
      submitBtn.disabled = true;
      submitBtn.textContent = 'Sending...';

      try {
        const formData = new FormData();
        formData.append('email', email);
        formData.append('timestamp', new Date().toISOString());

        await fetch(SERVER_ENDPOINT, {
          method: 'POST',
          body: formData
        });
      } catch (err) {
        console.warn('Server save failed:', err);
      }

      successBox.style.display = 'block';
      submitBtn.disabled = false;
      submitBtn.textContent = 'Send me the guide';
      emailInput.value = '';

      window.location.href = PDF_URL;
    });
  </script>
</body>
</html>
