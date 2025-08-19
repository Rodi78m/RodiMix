# RodiMix
<!DOCTYPE html>
<html lang="ar">
<head>
  <meta charset="UTF-8" />
  <title>Rodi Mix Radio</title>
  <style>
    body {
      font-family: sans-serif;
      background: #eee;
      text-align: center;
      margin: 0;
      padding: 20px;
    }
    button {
      margin: 5px;
      padding: 10px;
      border: none;
      background: #8B4513;
      color: #fff;
      cursor: pointer;
      border-radius: 5px;
      font-size: 16px;
    }
    iframe {
      width: 100%;
      max-width: 700px;
      height: 300px;
      border: none;
      margin-top: 20px;
      border-radius: 10px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.1);
    }
    #player-box {
      margin-top: 20px;
    }
  </style>
</head>
<body>

  <h2>🎧 Rodi Mix Radio</h2>

  <button onclick="load('ar')">العربية</button>
  <button onclick="load('ku')">كردي</button>
  <button onclick="load('en')">English</button>
  <button onclick="load('de')">Deutsch</button>

  <div id="player-box"></div>

  <script>
    const links = {
      ar: "https://w.soundcloud.com/player/?url=https%3A//on.soundcloud.com/8F4OjyT2rhUL06Friu&color=%23ff5500&auto_play=false&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true",
      ku: "https://w.soundcloud.com/player/?url=https%3A//on.soundcloud.com/TRu6ULP4OOhHfDiSuq&color=%23ff5500&auto_play=false&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true",
      en: "https://w.soundcloud.com/player/?url=https%3A//on.soundcloud.com/uasUDhCcNVwcpXOmxw&color=%23ff5500&auto_play=false&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true",
      de: "https://w.soundcloud.com/player/?url=https%3A//on.soundcloud.com/8S47Uqyf05VRGGCDRn&color=%23ff5500&auto_play=false&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true"
    };

    function load(lang) {
      const playerBox = document.getElementById('player-box');
      if (links[lang]) {
        playerBox.innerHTML = `<iframe src="${links[lang]}" allow="autoplay" loading="lazy"></iframe>`;
      } else {
        playerBox.innerHTML = "<p>محتوى غير متوفر</p>";
      }
    }

    // تحميل اللغة الافتراضية عند فتح الصفحة (مثلاً الكردية)
    load('ku');
  </script>

</body>
</html>
