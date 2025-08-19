Rodi.Mix
<html lang="ar">
<head>
  <meta charset="UTF-8" />
  <title>Rodi Mix Radio</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: #f7f3e9;
      text-align: center;
      margin: 0;
      padding: 20px;
      color: #333;
    }
    h2 {
      color: #8B4513;
    }
    button {
      margin: 8px;
      padding: 12px 20px;
      border: none;
      background: #8B4513;
      color: #fff;
      cursor: pointer;
      border-radius: 6px;
      font-size: 16px;
      transition: background 0.3s;
    }
    button:hover {
      background: #A0522D;
    }
    iframe {
      width: 90%;
      max-width: 700px;
      height: 300px;
      border: none;
      margin-top: 20px;
      border-radius: 12px;
      box-shadow: 0 6px 12px rgba(0,0,0,0.15);
    }
    .track-list {
      width: 90%;
      max-width: 700px;
      margin: 20px auto;
      background: white;
      border-radius: 10px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.1);
      padding: 15px;
    }
    .track-item {
      display: flex;
      justify-content: space-between;
      padding: 10px;
      border-bottom: 1px solid #eee;
      font-size: 14px;
    }
    .track-item:last-child {
      border-bottom: none;
    }
    .track-title {
      font-weight: bold;
      color: #5a3921;
      flex: 2;
      text-align: right;
    }
    .track-artist {
      flex: 2;
      color: #333;
      text-align: left;
    }
    .track-stats {
      color: #8B4513;
      font-size: 13px;
      min-width: 80px;
      text-align: right;
    }
    #player-box {
      margin-top: 20px;
    }
    @media (max-width: 600px) {
      .track-item {
        flex-direction: column;
        align-items: flex-start;
      }
      .track-stats {
        margin-top: 5px;
      }
    }
  </style>
</head>
<body>

  <h2>🎧 Rodi Mix Radio</h2>

  <button onclick="load('ku')">كردي</button>
  <button onclick="load('ar')">العربية</button>
  <button onclick="load('en')">English</button>
  <button onclick="load('de')">Deutsch</button>

  <div id="player-box"></div>
  <div id="track-list"></div>

  <script>
    // ✅ الروابط الجديدة (مُعدّة للإضافة)
    const players = {
      ku: "https://w.soundcloud.com/player/?url=https%3A//soundcloud.com/yusuf-i-k-685870955/sets/kurdish-music&color=%23ff5500&auto_play=false",
      ar: "https://w.soundcloud.com/player/?url=https%3A//soundcloud.com/bader-alzman/sets/2025a1&color=%23ff5500&auto_play=false",
      en: "https://w.soundcloud.com/player/?url=https%3A//soundcloud.com/turbulentz/sets/clean-hits-2025-best-pop-clean&color=%23ff5500&auto_play=false",
      de: "https://w.soundcloud.com/player/?url=https%3A//soundcloud.com/user-218498324/sets/deutsch-rap-remix&color=%23ff5500&auto_play=false"
    };

    // ✅ قوائم الأغاني من المحتوى الفعلي
    const tracks = {
      // الأغاني الكردية - من المحتوى الجديد في قاعدة المعرفة
      ku: [
        { title: "Ez Kurdistan Im", artist: "Serhado", plays: "" },
        { title: "Zap Zap Zape", artist: "sanliurfaHDP", plays: "" },
        { title: "Awaze Ciya Kato", artist: "Kadar Baze Kurdi", plays: "" },
        { title: "Awazê Çiya | Navê Wê", artist: "ewrêdeng", plays: "" },
        { title: "Awaze çiya - biji biji ypg", artist: "kurdishmusics", plays: "" }
      ],
      // الأغاني العربية - قائمة افتراضية (يمكن تحديثها لاحقًا)
      ar: [
        { title: "أغنية 1", artist: "فنان 1", plays: "" },
        { title: "أغنية 2", artist: "فنان 2", plays: "" },
        { title: "أغنية 3", artist: "فنان 3", plays: "" },
        { title: "أغنية 4", artist: "فنان 4", plays: "" },
        { title: "أغنية 5", artist: "فنان 5", plays: "" }
      ],
      // الأغاني الإنجليزية - من المحتوى الجديد
      en: [
        { title: "Ssio ehrenloser remix", artist: "Nikurazu", plays: "" },
        { title: "Paris Freestyle x Gangstas Paradise", artist: "r58", plays: "" },
        { title: "Airwaves Remix", artist: "roland", plays: "" },
        { title: "SSIO - HASH HASH x Barbra Streisand", artist: "FW", plays: "" },
        { title: "SSIO vs. Usher - Yeah Nuttööö", artist: "Daniel Hein Mashups", plays: "" }
      ],
      // الأغاني الألمانية - من المحتوى الجديد
      de: [
        { title: "Ssio ehrenloser remix", artist: "Nikurazu", plays: "" },
        { title: "Paris Freestyle x Gangstas Paradise", artist: "r58", plays: "" },
        { title: "Airwaves Remix", artist: "roland", plays: "" },
        { title: "SSIO - HASH HASH x Barbra Streisand", artist: "FW", plays: "" },
        { title: "SSIO vs. Usher - Yeah Nuttööö", artist: "Daniel Hein Mashups", plays: "" }
      ]
    };

    function load(lang) {
      const playerBox = document.getElementById('player-box');
      const trackList = document.getElementById('track-list');

      // تحميل المشغل
      if (players[lang]) {
        playerBox.innerHTML = `<iframe src="${players[lang]}" allow="autoplay" loading="lazy" title="مشغل موسيقى ${lang}"></iframe>`;
      } else {
        playerBox.innerHTML = "<p style='color: #888;'>المشغل غير متوفر.</p>";
      }

      // تحميل قائمة الأغاني
      if (tracks[lang] && tracks[lang].length > 0) {
        const listHTML = tracks[lang].map(track => 
          `<div class="track-item">
            <div class="track-title">${track.title}</div>
            <div class="track-artist">${track.artist}</div>
            <div class="track-stats">${track.plays} تشغيلاً</div>
          </div>`
        ).join('');
        trackList.innerHTML = `<div class="track-list"><h3>قائمة الأغاني</h3>${listHTML}</div>`;
      } else {
        trackList.innerHTML = "<p style='color: #888;'>قائمة الأغاني غير متوفرة.</p>";
      }
    }

    // تحميل اللغة الكردية افتراضيًا
    window.onload = () => load('ku');
  </script>

</body>
</html>
