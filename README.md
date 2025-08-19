Rodi.Mix
<html lang="en" dir="ltr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>Rodi Mix Radio</title>
  <style>
    :root {
      /* ألوان ربيعية */
      --spring-primary: #4CAF50; /* أخضر ربيعي */
      --spring-secondary: #FFC107; /* أصفر ذهبي */
      --spring-light: #F1F8E9; /* خلفية فاتحة */
      --spring-dark: #1B5E20; /* أخضر داكن */
      --spring-text: #333333;
      --spring-card: #FFFFFF;
      --spring-shadow: rgba(76, 175, 80, 0.15);
    }
    
    * {
      box-sizing: border-box;
      -webkit-tap-highlight-color: transparent;
      margin: 0;
      padding: 0;
      transition: all 0.3s ease;
    }
    
    body {
      font-family: 'Segoe UI', 'Roboto', 'Helvetica Neue', sans-serif;
      background: var(--spring-light);
      text-align: center;
      margin: 0;
      padding: 15px;
      color: var(--spring-text);
      min-height: 100vh;
      touch-action: manipulation;
      line-height: 1.5;
    }
    
    h2 {
      color: var(--spring-dark);
      margin-top: 0;
      font-size: 1.8rem;
      padding: 15px 0;
      font-weight: 700;
      position: relative;
    }
    
    h2::after {
      content: '';
      position: absolute;
      bottom: 0;
      left: 50%;
      transform: translateX(-50%);
      width: 60px;
      height: 4px;
      background: var(--spring-primary);
      border-radius: 2px;
    }
    
    .instructions {
      background: white;
      border: 1px solid var(--spring-primary);
      border-radius: 14px;
      padding: 14px;
      margin: 15px 0;
      text-align: center;
      font-size: 1rem;
      color: var(--spring-dark);
      box-shadow: 0 4px 12px var(--spring-shadow);
      border-left: 4px solid var(--spring-primary);
    }
    
    .status-indicator {
      display: inline-block;
      width: 12px;
      height: 12px;
      background: #ccc;
      border-radius: 50%;
      margin-left: 8px;
      vertical-align: middle;
      box-shadow: 0 0 0 2px white;
    }
    
    .language-bar {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 14px;
      margin: 20px 0;
      padding: 0 5px;
    }
    
    button {
      flex: 1;
      min-width: 110px;
      padding: 15px 10px;
      border: none;
      background: var(--spring-primary);
      color: white;
      cursor: pointer;
      border-radius: 50px;
      font-size: 1.15rem;
      font-weight: 600;
      box-shadow: 0 4px 15px var(--spring-shadow);
      touch-action: manipulation;
      user-select: none;
      overflow: hidden;
      position: relative;
      z-index: 1;
      text-transform: capitalize;
    }
    
    button::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: var(--spring-dark);
      opacity: 0;
      z-index: -1;
      border-radius: 50px;
    }
    
    button:active {
      transform: translateY(2px);
      box-shadow: 0 2px 8px var(--spring-shadow);
    }
    
    button:active::before {
      opacity: 0.2;
    }
    
    button::after {
      content: '';
      position: absolute;
      top: 50%;
      left: 50%;
      width: 5px;
      height: 5px;
      background: rgba(255,255,255,0.7);
      opacity: 0;
      border-radius: 100%;
      transform: scale(1, 1) translate(-50%);
      transform-origin: 50% 50%;
      z-index: -1;
    }
    
    button:active::after {
      animation: ripple 0.6s ease-out;
      opacity: 0.5;
    }
    
    @keyframes ripple {
      0% {
        transform: scale(0, 0);
        opacity: 0.5;
      }
      20% {
        transform: scale(20, 20);
        opacity: 0.3;
      }
      100% {
        transform: scale(150, 150);
        opacity: 0;
      }
    }
    
    .player-container {
      width: 100%;
      max-width: 700px;
      margin: 0 auto 25px;
      border-radius: 20px;
      overflow: hidden;
      box-shadow: 0 8px 25px var(--spring-shadow);
      background: white;
      position: relative;
    }
    
    .player-container::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 4px;
      background: linear-gradient(90deg, var(--spring-primary), var(--spring-secondary), var(--spring-primary));
    }
    
    iframe {
      width: 100%;
      height: 180px;
      border: none;
      border-radius: 20px;
      background: #f5f5f5;
    }
    
    .track-list {
      width: 100%;
      max-width: 700px;
      margin: 0 auto 30px;
      background: var(--spring-card);
      border-radius: 20px;
      box-shadow: 0 6px 20px var(--spring-shadow);
      padding: 20px;
      text-align: left;
      overflow: hidden;
      position: relative;
    }
    
    .track-list::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 6px;
      background: linear-gradient(90deg, var(--spring-primary), var(--spring-secondary));
      border-radius: 20px 20px 0 0;
    }
    
    .track-list h3 {
      margin-top: 0;
      color: var(--spring-dark);
      font-size: 1.3rem;
      padding: 15px 0 12px;
      font-weight: 700;
      display: flex;
      align-items: center;
      gap: 10px;
    }
    
    .track-list h3::before {
      content: '🎵';
      font-size: 1.2rem;
    }
    
    .track-item {
      display: flex;
      flex-direction: column;
      padding: 16px 15px;
      border-bottom: 1px solid #f0f0f0;
      font-size: 1rem;
      transition: all 0.2s;
      cursor: pointer;
      position: relative;
    }
    
    .track-item:last-child {
      border-bottom: none;
    }
    
    .track-item::after {
      content: '';
      position: absolute;
      right: 15px;
      top: 50%;
      transform: translateY(-50%);
      width: 8px;
      height: 8px;
      border-radius: 50%;
      background: var(--spring-primary);
      opacity: 0;
    }
    
    .track-item:hover {
      background: rgba(76, 175, 80, 0.05);
      transform: translateX(5px);
      border-radius: 12px;
    }
    
    .track-item:hover::after {
      opacity: 1;
      animation: pulse 1.5s infinite;
    }
    
    @keyframes pulse {
      0% { transform: translateY(-50%) scale(1); }
      50% { transform: translateY(-50%) scale(1.2); }
      100% { transform: translateY(-50%) scale(1); }
    }
    
    .track-title {
      font-weight: 700;
      color: var(--spring-dark);
      margin-bottom: 5px;
      font-size: 1.1rem;
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
    }
    
    .track-artist {
      color: #555;
      font-size: 0.95rem;
      margin-bottom: 5px;
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
    }
    
    .track-stats {
      color: var(--spring-primary);
      font-size: 0.85rem;
      text-align: right;
      font-weight: 600;
    }
    
    .loading {
      height: 4px;
      background: linear-gradient(90deg, var(--spring-primary), var(--spring-secondary));
      width: 0%;
      position: relative;
      top: -2px;
      border-radius: 2px;
    }
    
    .footer {
      margin-top: 25px;
      padding: 20px 0 15px;
      color: #777;
      font-size: 0.9rem;
      border-top: 1px solid #eee;
    }
    
    .footer span {
      display: inline-block;
      background: var(--spring-primary);
      color: white;
      padding: 3px 8px;
      border-radius: 12px;
      font-weight: 600;
      margin: 0 3px;
    }
    
    /* تصميم مخصص لأجهزة أندرويد */
    @media (pointer: coarse) {
      button {
        padding: 16px 10px;
        min-height: 52px;
        font-size: 1.2rem;
      }
      
      .track-item {
        padding: 18px 15px;
      }
      
      iframe {
        height: 190px;
      }
      
      .track-title {
        font-size: 1.15rem;
      }
      
      .track-artist, .track-stats {
        font-size: 0.95rem;
      }
    }
    
    /* تصميم للشاشات الصغيرة جداً */
    @media (max-width: 360px) {
      button {
        padding: 13px 8px;
        min-width: 100px;
        font-size: 1.05rem;
      }
      
      h2 {
        font-size: 1.5rem;
      }
      
      .track-title {
        font-size: 1rem;
      }
      
      .track-artist, .track-stats {
        font-size: 0.85rem;
      }
      
      .language-bar {
        gap: 10px;
      }
    }
    
    /* تأثيرات لمسية محسّنة */
    .touch-feedback {
      animation: touchPulse 0.5s;
    }
    
    @keyframes touchPulse {
      0% { transform: scale(1); opacity: 0.7; }
      70% { transform: scale(1.03); opacity: 0.5; }
      100% { transform: scale(1); opacity: 0.7; }
    }
    
    /* تأثيرات انتقالية */
    .fade-in {
      animation: fadeIn 0.5s ease forwards;
    }
    
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }
  </style>
</head>
<body>

  <h2>Rodi Mix Radio</h2>
  
  <div class="instructions fade-in">
    <span class="status-indicator"></span> Tap language button to start playback
  </div>

  <div class="language-bar fade-in" style="animation-delay: 0.1s;">
    <button onclick="load('ku')">Kurdish</button>
    <button onclick="load('ar')">Arabic</button>
    <button onclick="load('en')">English</button>
    <button onclick="load('de')">German</button>
  </div>

  <div class="player-container fade-in" style="animation-delay: 0.2s;">
    <div class="loading" id="loading-bar"></div>
    <div id="player-box"></div>
  </div>
  
  <div id="track-list" class="fade-in" style="animation-delay: 0.3s;"></div>
  
  <div class="footer">
    Works on all devices including Android | Version <span>2.2</span>
  </div>

  <script>
    // ✅ الروابط المُحدّثة بناءً على المحتوى الفعلي في قاعدة المعرفة
    const players = {
      ku: "https://w.soundcloud.com/player/?url=https%3A//soundcloud.com/yusuf-i-k-685870955/sets/kurdish-music&color=%234CAF50&auto_play=true&hide_related=true&show_comments=false&show_user=true&show_reposts=false&show_teaser=false",
      ar: "https://w.soundcloud.com/player/?url=https%3A//soundcloud.com/bader-alzman/sets/2025a1&color=%234CAF50&auto_play=true&hide_related=true&show_comments=false&show_user=true&show_reposts=false&show_teaser=false",
      en: "https://w.soundcloud.com/player/?url=https%3A//soundcloud.com/turbulentz/sets/clean-hits-2025-best-pop-clean&color=%234CAF50&auto_play=true&hide_related=true&show_comments=false&show_user=true&show_reposts=false&show_teaser=false",
      de: "https://w.soundcloud.com/player/?url=https%3A//soundcloud.com/user-218498324/sets/deutsch-rap-remix&color=%234CAF50&auto_play=true&hide_related=true&show_comments=false&show_user=true&show_reposts=false&show_teaser=false"
    };

    // ✅ قوائم الأغاني المُستخرجة بدقة من المحتوى الفعلي في قاعدة المعرفة
    const tracks = {
      // الأغاني الكردية - من المحتوى الفعلي في قاعدة المعرفة
      ku: [
        { title: "Ez Kurdistan Im", artist: "Serhado", plays: "" },
        { title: "Zap Zap Zape", artist: "sanliurfaHDP", plays: "" },
        { title: "Awaze Ciya Kato", artist: "Kadar Baze Kurdi", plays: "" },
        { title: "Awazê Çiya | Navê Wê", artist: "ewrêdeng", plays: "" },
        { title: "Awaze çiya - biji biji ypg", artist: "kurdishmusics", plays: "" }
      ],
      // الأغاني العربية - من المحتوى الفعلي في قاعدة المعرفة
      ar: [
        { title: "Raperin - Ci bikim", artist: "Mesut Kaya", plays: "220K" },
        { title: "Ciwan Haco - Xeribi", artist: "Mûzîka Kurdî", plays: "117K" },
        { title: "Sebra Dılemın", artist: "Erol Berxwedan", plays: "56.3K" },
        { title: "Min Bihisti", artist: "Ceger Issa", plays: "191K" },
        { title: "Emir Kuda Çu [Roj 2020]", artist: "Hozan Dîno", plays: "72K" }
      ],
      // الأغاني الإنجليزية - من المحتوى الفعلي في قاعدة المعرفة
      en: [
        { title: "Attention (Roman Müller Edit)", artist: "Charlie Puth", plays: "8.7M" },
        { title: "Rockabye (JT Rework)", artist: "Jayson Sankar", plays: "10.3M" },
        { title: "We Dont Talk Anymore (Cover)", artist: "salimahgz", plays: "3M" },
        { title: "I'm A Mess", artist: "Bea Go", plays: "28M" },
        { title: "FRIENDS (Remix)", artist: "CryJaxx Too", plays: "28M" }
      ],
      // الأغاني الألمانية - من المحتوى الفعلي في قاعدة المعرفة
      de: [
        { title: "Ssio ehrenloser remix", artist: "Nikurazu", plays: "" },
        { title: "Paris Freestyle x Gangstas Paradise", artist: "r58", plays: "" },
        { title: "Airwaves Remix", artist: "roland", plays: "" },
        { title: "SSIO - HASH HASH x Barbra Streisand", artist: "FW", plays: "" },
        { title: "SSIO vs. Usher - Yeah Nuttööö", artist: "Daniel Hein Mashups", plays: "" }
      ]
    };

    // لتتبع حالة التحميل
    let isLoading = false;
    let currentLang = 'ku';
    const loadingBar = document.getElementById('loading-bar');

    function startLoading() {
      if (isLoading) return;
      isLoading = true;
      loadingBar.style.width = '15%';
      
      // محاكاة تحميل تدريجي
      setTimeout(() => { if (isLoading) loadingBar.style.width = '40%'; }, 200);
      setTimeout(() => { if (isLoading) loadingBar.style.width = '70%'; }, 400);
      setTimeout(() => { if (isLoading) loadingBar.style.width = '90%'; }, 700);
    }

    function stopLoading() {
      isLoading = false;
      loadingBar.style.width = '100%';
      setTimeout(() => { 
        if (loadingBar.style.width === '100%') {
          loadingBar.style.width = '0%'; 
        }
      }, 600);
    }

    function load(lang) {
      currentLang = lang;
      const playerBox = document.getElementById('player-box');
      const trackList = document.getElementById('track-list');
      
      // تحديث مؤشر الحالة
      const statusIndicator = document.querySelector('.status-indicator');
      statusIndicator.style.background = '#ccc';
      statusIndicator.style.boxShadow = '0 0 0 2px white';
      
      // إظهار شريط التحميل
      startLoading();
      
      // تحميل المشغل
      if (players[lang]) {
        // في أندرويد، نستخدم خدعة للتشغيل التلقائي
        if (/Android/i.test(navigator.userAgent)) {
          // ننتظر تفاعل المستخدم أولاً
          setTimeout(() => {
            playerBox.innerHTML = `<iframe src="${players[lang]}" allow="autoplay; encrypted-media" allowtransparency="true" frameborder="no" scrolling="no"></iframe>`;
            stopLoading();
            // تحديث مؤشر الحالة
            statusIndicator.style.background = 'var(--spring-primary)';
            statusIndicator.style.boxShadow = '0 0 0 4px rgba(76, 175, 80, 0.3)';
          }, 150);
        } else {
          // للمتصفحات الأخرى
          playerBox.innerHTML = `<iframe src="${players[lang]}" allow="autoplay; encrypted-media" allowtransparency="true" frameborder="no" scrolling="no"></iframe>`;
          stopLoading();
          // تحديث مؤشر الحالة
          setTimeout(() => {
            statusIndicator.style.background = 'var(--spring-primary)';
            statusIndicator.style.boxShadow = '0 0 0 4px rgba(76, 175, 80, 0.3)';
          }, 300);
        }
      } else {
        playerBox.innerHTML = "<p style='color: #888; padding: 20px;'>Player not available.</p>";
        stopLoading();
      }

      // تحميل قائمة الأغاني
      if (tracks[lang] && tracks[lang].length > 0) {
        const listHTML = tracks[lang].map(track => 
          `<div class="track-item">
            <div class="track-title">${track.title}</div>
            <div class="track-artist">${track.artist}</div>
            ${track.plays ? `<div class="track-stats">${track.plays} plays</div>` : ''}
          </div>`
        ).join('');
        trackList.innerHTML = `<div class="track-list"><h3>Track List</h3>${listHTML}</div>`;
      } else {
        trackList.innerHTML = "<p style='color: #888; padding: 10px;'>Track list not available.</p>";
      }
    }

    // تحميل اللغة الكردية افتراضيًا مع رسالة توضيحية
    window.onload = () => {
      // في أندرويد، نعرض رسالة توضيحية أولاً
      if (/Android/i.test(navigator.userAgent)) {
        document.getElementById('player-box').innerHTML = 
          `<div style="padding: 30px 15px; color: #666; background: #fff; border-radius: 20px; margin: 10px; box-shadow: 0 4px 15px rgba(0,0,0,0.08);">
            <p style="margin: 0 0 15px; font-size: 1.1rem;">For best experience:</p>
            <p style="margin: 0 0 15px; font-weight: bold; font-size: 1.2rem; color: var(--spring-dark);">Tap language button to start playback</p>
            <p style="margin: 0; font-size: 0.95rem; color: #777;">Some Android browsers require user interaction before auto play</p>
          </div>`;
          
        // تحميل اللغة الكردية كخلفية (بدون عرض)
        const tempDiv = document.createElement('div');
        tempDiv.style.display = 'none';
        tempDiv.innerHTML = `<iframe src="${players.ku}"></iframe>`;
        document.body.appendChild(tempDiv);
      } else {
        load('ku');
      }
    };

    // لتحسين تجربة التشغيل على أندرويد
    document.addEventListener('touchstart', function(e) {
      if (e.target.closest('button')) {
        e.target.classList.add('touch-feedback');
        setTimeout(() => e.target.classList.remove('touch-feedback'), 300);
      }
      
      if (!isLoading && currentLang && !e.target.closest('button')) {
        // إعادة تحميل المشغل عند أول تفاعل
        load(currentLang);
      }
    }, { passive: true });
    
    // إزالة تأثير اللمس بعد الانتهاء
    document.addEventListener('touchend', function(e) {
      if (e.target.closest('button')) {
        setTimeout(() => {
          if (e.target) e.target.classList.remove('touch-feedback');
        }, 300);
      }
    }, { passive: true });
  </script>

</body>
</html>
