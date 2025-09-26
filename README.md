<!-- text_to_speech.html -->
<!DOCTYPE html>
<html lang="fa">
<head>
  <meta charset="UTF-8">
  <title>🎤 تبدیل متن به گفتار</title>
  <style>
    ody {
      font-family: sans-serif;
      background: linear-gradient(135deg, #f6d365, #fda085);
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      text-align: center;
    }
    textarea {
      width: 300px;
      height: 120px;
      border-radius: 10px;
      border: 1px solid #ccc;
      padding: 10px;
      font-size: 16px;
      margin-bottom: 15px;
    }
    button {
      padding: 10px 20px;
      border: none;
      border-radius: 8px;
      background: #333;
      color: #fff;
      cursor: pointer;
      margin: 5px;
      transition: 0.3s;
    }
    button:hover {
      background: #555;
    }
    select {
      padding: 5px;
      margin-bottom: 10px;
      border-radius: 6px;
      font-size: 14px;
    }
  </style>
</head>
<body>
  <h1>🎤 تبدیل متن به گفتار</h1>
  <textarea id="text" placeholder="متن خود را اینجا بنویسید..."></textarea>
  <select id="voices"></select><br>
  <button onclick="speak()">🔊 پخش صدا</button>
  <button onclick="stop()">⏹ توقف</button>

  <script>
    const synth = window.speechSynthesis;
    const voiceSelect = document.getElementById("voices");

    function loadVoices() {
      const voices = synth.getVoices();
      voiceSelect.innerHTML = "";
      voices.forEach((voice, i) => {
        const option = document.createElement("option");
        option.value = i;
        option.textContent = `${voice.name} (${voice.lang})`;
        voiceSelect.appendChild(option);
      });
    }

    function speak() {
      const text = document.getElementById("text").value;
      if (!text) {
        alert("⚠️ لطفاً متنی وارد کنید!");
        return;
      }
      const utterance = new SpeechSynthesisUtterance(text);
      const selectedVoice = synth.getVoices()[voiceSelect.value];
      if (selectedVoice) utterance.voice = selectedVoice;
      synth.speak(utterance);
    }

    function stop() {
      synth.cancel();
    }

    loadVoices();
    if (speechSynthesis.onvoiceschanged !== undefined) {
      speechSynthesis.onvoiceschanged = loadVoices;
    }
  </script>
</body>
</html>
