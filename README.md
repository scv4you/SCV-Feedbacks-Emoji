<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Sarawak Visitor Survey</title>
  <style>
    * { box-sizing: border-box; }

    body {
      margin: 0;
      padding: 20px;
      font-family: 'Segoe UI', Arial, sans-serif;
      /* Using a reliable high-res Sarawak Pua Kumbu pattern */
      background-image: linear-gradient(rgba(0, 0, 0, 0.6), rgba(0, 0, 0, 0.6)), 
                        url('https://images.squarespace-cdn.com/content/v1/58983995414fb571f54ad964/1589360814986-W19O3W8F3T006T8KMB9U/Pua+Kumbu+Details+1.jpg'); 
      background-size: cover;
      background-position: center;
      background-attachment: fixed;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
    }

    .container {
      background: rgba(255, 255, 255, 0.98);
      padding: clamp(20px, 5vw, 50px);
      border-radius: 24px;
      box-shadow: 0 20px 50px rgba(0,0,0,0.5);
      text-align: center;
      width: 100%;
      max-width: 850px;
      border-top: 10px solid #8B0000;
    }

    h1 { font-size: clamp(1.8rem, 5vw, 2.8rem); margin-bottom: 10px; color: #222; }
    p { color: #444; font-size: clamp(1rem, 2.5vw, 1.3rem); margin-bottom: 40px; }

    .emoji-group {
      display: grid;
      grid-template-columns: repeat(2, 1fr); 
      gap: 20px;
    }

    .emoji-btn {
      border: 3px solid #eee;
      background: #fff;
      border-radius: 25px;
      padding: 30px 10px;
      cursor: pointer;
      transition: all 0.3s ease;
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    .emoji-btn:hover {
      transform: translateY(-10px);
      border-color: #8B0000;
      background: #fff8f8;
    }

    .emoji { font-size: clamp(3rem, 10vw, 5rem); margin-bottom: 15px; }
    .label { font-size: 1.1rem; font-weight: 800; color: #8B0000; text-transform: uppercase; }

    #thank-you-ui { display: none; padding: 60px 0; }
    .success-icon { font-size: 6rem; margin-bottom: 20px; }

    @media (min-width: 768px) { .emoji-group { grid-template-columns: repeat(4, 1fr); } }
  </style>
</head>
<body>

  <div class="container">
    <div id="survey-ui">
      <h1>Selamat Datang</h1>
      <p>How was your experience today?</p>
      <div class="emoji-group">
        <button class="emoji-btn" onclick="submitFeedback('Bad')">
          <span class="emoji">😞</span>
          <span class="label">Bad</span>
        </button>
        <button class="emoji-btn" onclick="submitFeedback('Okay')">
          <span class="emoji">😐</span>
          <span class="label">Okay</span>
        </button>
        <button class="emoji-btn" onclick="submitFeedback('Good')">
          <span class="emoji">😊</span>
          <span class="label">Good</span>
        </button>
        <button class="emoji-btn" onclick="submitFeedback('Amazing')">
          <span class="emoji">😍</span>
          <span class="label">Amazing</span>
        </button>
      </div>
    </div>

    <div id="thank-you-ui">
      <div class="success-icon">✨</div>
      <h1>Terima Kasih!</h1>
      <p>Your feedback helps us improve.</p>
    </div>
  </div>

  <script>
    const SCRIPT_URL = 'https://script.google.com/macros/s/AKfycbw84oD3P8wRiHYiEJBw-0zRU7ghEKUalAY6ObfWaYZ8WAe3rvqwQiHNlwfVyQ-HWv378g/exec';

    function submitFeedback(rating) {
      document.getElementById('survey-ui').style.display = 'none';
      document.getElementById('thank-you-ui').style.display = 'block';

      fetch(SCRIPT_URL, {
        method: 'POST',
        mode: 'no-cors', 
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ rating: rating })
      });

      setTimeout(() => { window.location.reload(); }, 2000);
    }
  </script>
</body>
</html>
