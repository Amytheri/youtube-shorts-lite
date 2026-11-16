# youtube-shorts-lite
Simple YouTube Shorts-inspired vertical video feed prototype
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>YouTube Shorts Lite</title>
    <style>
      :root {
        --bg: #0f0f0f;
        --card: #121212;
        --muted: #b0b0b0;
        --text: #ffffff;
        --accent: #ff0033;
        --shadow: rgba(0, 0, 0, 0.45);
      }

      * {
        box-sizing: border-box;
      }

      html, body {
        margin: 0;
        height: 100%;
        background: var(--bg);
        color: var(--text);
        font-family: Arial, Helvetica, sans-serif;
      }

      body {
        display: flex;
        justify-content: center;
        align-items: stretch;
      }

      .app {
        width: 100%;
        max-width: 430px;
        height: 100vh;
        background: #000;
        position: relative;
        overflow: hidden;
      }

      .topbar {
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        padding: 18px 16px 0;
        display: flex;
        align-items: center;
        justify-content: space-between;
        z-index: 10;
        background: linear-gradient(to bottom, rgba(0,0,0,0.7), transparent);
      }

      .brand {
        font-weight: 700;
        letter-spacing: 0.5px;
      }

      .top-icons {
        display: flex;
        gap: 12px;
        font-size: 20px;
      }

      .feed {
        height: 100%;
        overflow-y: auto;
        scroll-snap-type: y mandatory;
        scrollbar-width: none;
      }

      .feed::-webkit-scrollbar {
        display: none;
      }

      .short {
        position: relative;
        height: 100vh;
        scroll-snap-align: start;
        background: #111;
        overflow: hidden;
      }

      .short video {
        width: 100%;
        height: 100%;
        object-fit: cover;
        display: block;
        background: #000;
      }

      .short::after {
        content: "";
        position: absolute;
        inset: 0;
        background: linear-gradient(to top, rgba(0,0,0,0.8), rgba(0,0,0,0.08) 40%, transparent 70%);
      }

      .content {
        position: absolute;
        left: 0;
        right: 0;
        bottom: 0;
        z-index: 2;
        display: flex;
        justify-content: space-between;
        padding: 20px 14px 20px 16px;
        gap: 12px;
      }

      .meta {
        max-width: 72%;
      }

      .channel {
        font-size: 14px;
        font-weight: 700;
        margin-bottom: 8px;
        opacity: 0.95;
      }

      .title {
        font-size: 18px;
        line-height: 1.3;
        font-weight: 700;
        margin-bottom: 10px;
      }

      .tag {
        font-size: 13px;
        color: #ddd;
        opacity: 0.9;
      }

      .actions {
        display: flex;
        flex-direction: column;
        gap: 14px;
        align-items: center;
        justify-content: flex-end;
        margin-bottom: 8px;
      }

      .action {
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 6px;
        font-size: 12px;
        color: white;
      }

      .circle {
        width: 50px;
        height: 50px;
        border-radius: 50%;
        background: rgba(255,255,255,0.15);
        backdrop-filter: blur(5px);
        display: grid;
        place-items: center;
        font-size: 22px;
        font-weight: 700;
      }

      .profile {
        background: linear-gradient(135deg, #ff8a00, #e52e71, #5b2cff);
      }

      .play-toggle {
        position: absolute;
        inset: 0;
        z-index: 3;
        display: grid;
        place-items: center;
        opacity: 0;
        pointer-events: none;
        transition: opacity 0.2s ease;
      }

      .play-toggle.show {
        opacity: 1;
      }

      .play-btn {
        width: 72px;
        height: 72px;
        border-radius: 50%;
        background: rgba(0,0,0,0.38);
        border: 2px solid rgba(255,255,255,0.45);
        display: grid;
        place-items: center;
        font-size: 32px;
      }

      @media (max-width: 420px) {
        .title {
          font-size: 16px;
        }
      }
    </style>
  </head>
  <body>
    <div class="app">
      <div class="topbar">
        <div class="brand">Shorts</div>
        <div class="top-icons">
          <span>⌕</span>
          <span>◌</span>
        </div>
      </div>

      <div class="feed" id="feed">
        <article class="short">
          <video
            muted
            loop
            playsinline
            autoplay
            preload="metadata"
            src="https://videos.pexels.com/video-files/3195394/3195394-hd_1920_1080.mp4"
          ></video>

          <div class="play-toggle">
            <div class="play-btn">▶</div>
          </div>

          <div class="content">
            <div class="meta">
              <div class="channel">@travelwithlina</div>
              <div class="title">Amazing sunset walk in the city</div>
              <div class="tag">#travel #city #sunset</div>
            </div>

            <div class="actions">
              <div class="action">
                <div class="circle">♥</div>
                <div>18.2K</div>
              </div>
              <div class="action">
                <div class="circle">💬</div>
                <div>540</div>
              </div>
              <div class="action">
                <div class="circle">↗</div>
                <div>Share</div>
              </div>
              <div class="action">
                <div class="circle profile">L</div>
              </div>
            </div>
          </div>
        </article>

        <article class="short">
          <video
            muted
            loop
            playsinline
            autoplay
            preload="metadata"
            src="https://videos.pexels.com/video-files/854952/854952-hd_1920_1080.mp4"
          ></video>

          <div class="play-toggle">
            <div class="play-btn">▶</div>
          </div>

          <div class="content">
            <div class="meta">
              <div class="channel">@fitnessflow</div>
              <div class="title">10-minute HIIT workout at home</div>
              <div class="tag">#fitness #workout #home</div>
            </div>

            <div class="actions">
              <div class="action">
                <div class="circle">♥</div>
                <div>9.8K</div>
              </div>
              <div class="action">
                <div class="circle">💬</div>
                <div>320</div>
              </div>
              <div class="action">
                <div class="circle">↗</div>
                <div>Share</div>
              </div>
              <div class="action">
                <div class="circle profile">F</div>
              </div>
            </div>
          </div>
        </article>

        <article class="short">
          <video
            muted
            loop
            playsinline
            autoplay
            preload="metadata"
            src="https://videos.pexels.com/video-files/853889/853889-hd_1920_1080.mp4"
          ></video>

          <div class="play-toggle">
            <div class="play-btn">▶</div>
          </div>

          <div class="content">
            <div class="meta">
              <div class="channel">@nightmode</div>
              <div class="title">Neon city vibes after dark</div>
              <div class="tag">#night #city #music</div>
            </div>

            <div class="actions">
              <div class="action">
                <div class="circle">♥</div>
                <div>27.1K</div>
              </div>
              <div class="action">
                <div class="circle">💬</div>
                <div>890</div>
              </div>
              <div class="action">
                <div class="circle">↗</div>
                <div>Share</div>
              </div>
              <div class="action">
                <div class="circle profile">N</div>
              </div>
            </div>
          </div>
        </article>
      </div>
    </div>

    <script>
      const videos = document.querySelectorAll('.short video');
      const toggles = document.querySelectorAll('.play-toggle');

      videos.forEach((video) => {
        video.addEventListener('click', () => {
          const toggle = video.parentElement.querySelector('.play-toggle');
          if (video.paused) {
            video.play();
            toggle.classList.remove('show');
          } else {
            video.pause();
            toggle.classList.add('show');
          }
        });
      });

      const observer = new IntersectionObserver((entries) => {
        entries.forEach((entry) => {
          const video = entry.target.querySelector('video');
          const toggle = entry.target.querySelector('.play-toggle');

          if (entry.isIntersecting) {
            video.play();
            toggle.classList.remove('show');
          } else {
            video.pause();
            toggle.classList.add('show');
          }
        });
      }, {
        threshold: 0.7
      });

      document.querySelectorAll('.short').forEach((short) => {
        observer.observe(short);
      });
    </script>
  </body>
</html>
