<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DUMUNDO - Official Album</title>
    <link href="https://fonts.googleapis.com/css2?family=MedievalSharp&family=Inter:wght@300;400;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #ff4444;
            --bg-dark: #050505;
            --card-bg: rgba(20, 20, 20, 0.8);
            --text: #ffffff;
            --accent: #555;
        }

        body {
            font-family: 'Inter', sans-serif;
            background: #000;
            background-image: radial-gradient(circle at top, #1a0505 0%, #050505 100%);
            color: var(--text);
            margin: 0;
            padding: 10px;
            padding-bottom: 180px;
            min-height: 100vh;
            -webkit-tap-highlight-color: transparent;
        }

        header {
            text-align: center;
            padding: 30px 0 15px 0;
            border-bottom: 1px solid rgba(255, 68, 68, 0.1);
            margin-bottom: 30px;
        }

        h1 {
            font-family: 'MedievalSharp', cursive;
            font-size: clamp(2.5rem, 8vw, 4rem);
            color: var(--primary);
            margin: 0;
            letter-spacing: 4px;
            text-shadow: 0 0 20px rgba(255, 68, 68, 0.3);
        }

        .album-subtitle {
            color: #aaa;
            text-transform: uppercase;
            letter-spacing: 2px;
            font-size: 0.75rem;
            margin-top: 8px;
            margin-bottom: 20px;
        }

        .upload-btn {
            background: rgba(255, 68, 68, 0.15);
            color: var(--primary);
            border: 1px solid var(--primary);
            padding: 10px 20px;
            border-radius: 20px;
            font-family: 'Inter', sans-serif;
            font-size: 0.85rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
        }

        .upload-btn:hover { background: var(--primary); color: white; }
        #fileInput { display: none; }

        .playlist-container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
            gap: 15px;
            max-width: 1000px;
            margin: 0 auto;
        }

        .track-card {
            background: var(--card-bg);
            border-radius: 8px;
            overflow: hidden;
            border: 1px solid rgba(255, 255, 255, 0.05);
            transition: transform 0.2s;
            cursor: pointer;
        }

        .track-card.active {
            border-color: var(--primary);
            background: rgba(255, 68, 68, 0.1);
        }

        .video-container {
            width: 100%;
            aspect-ratio: 16/9;
            background: #111;
            position: relative;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .video-container video {
            width: 100%;
            height: 100%;
            object-fit: cover;
            display: none;
        }

        .track-card.active video { display: block; }

        .track-info {
            padding: 12px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .track-num {
            font-family: 'MedievalSharp';
            color: var(--primary);
            font-size: 0.9rem;
        }

        .track-name { 
            font-weight: 500; 
            font-size: 0.85rem; 
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }

        .player-footer {
            position: fixed;
            bottom: 0;
            left: 0;
            width: 100%;
            background: rgba(5, 5, 5, 0.98);
            backdrop-filter: blur(15px);
            border-top: 1px solid var(--primary);
            padding: 15px;
            z-index: 9999;
        }

        .player-content { max-width: 800px; margin: 0 auto; }
        .current-info { text-align: center; margin-bottom: 10px; }
        .current-info h3 { margin: 0; font-size: 1rem; color: var(--primary); font-family: 'MedievalSharp'; }

        .main-controls { display: flex; justify-content: center; align-items: center; gap: 30px; margin-bottom: 15px; }
        .btn-ctrl { background: none; border: none; color: white; font-size: 1.8rem; cursor: pointer; }

        #playPauseBtn {
            background: var(--primary);
            width: 55px; height: 55px;
            border-radius: 50%;
            font-size: 1.2rem;
            display: flex; justify-content: center; align-items: center;
        }

        .progress-container { display: flex; align-items: center; gap: 10px; font-size: 0.7rem; color: #888; }
        input[type="range"] { flex: 1; accent-color: var(--primary); height: 4px; }
    </style>
</head>
<body>

<header>
    <h1>DUMUNDO</h1>
    <p class="album-subtitle">Álbum Oficial • 2026 • Work Toda Hora Ent...</p>
    
    <input type="file" id="fileInput" multiple accept="audio/*, video/*">
    <button class="upload-btn" onclick="document.getElementById('fileInput').click()">
        📁 CARREGAR ARQUIVOS DO TELEFONE
    </button>
</header>

<main class="playlist-container" id="playlist"></main>

<footer class="player-footer">
    <div class="player-content">
        <div class="current-info">
            <h3 id="currentTitle">Selecione uma faixa</h3>
            <div style="font-size: 0.7rem; color: #666; margin-top: 4px;">DUMUNDO</div>
        </div>

        <div class="main-controls">
            <button class="btn-ctrl" id="prevBtn">⏮</button>
            <button class="btn-ctrl" id="playPauseBtn">▶</button>
            <button class="btn-ctrl" id="nextBtn">⏭</button>
        </div>

        <div class="progress-container">
            <span id="curTime">0:00</span>
            <input type="range" id="progressBar" value="0" min="0" max="100">
            <span id="totalTime">0:00</span>
        </div>
    </div>
</footer>

<script>
    const audio = new Audio();
    
    // ========================================================
    // EXEMPLOS REAIS DA INTERNET (No Copyright)
    // ========================================================
    let tracks = [
        {
            title: "Vibe Tropical (Instrumental)",
            audioUrl: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3",
            videoUrl: "https://vjs.zencdn.net/v/oceans.mp4" 
        },
        {
            title: "Beat Medieval Trap",
            audioUrl: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-2.mp3",
            videoUrl: "https://www.w3schools.com/html/mov_bbb.mp4" 
        },
        {
            title: "Work Toda Hora - Remix",
            audioUrl: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-8.mp3",
            videoUrl: "http://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ElephantsDream.mp4"
        },
        {
            title: "Gatpreto Lifestyle",
            audioUrl: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-10.mp3",
            videoUrl: "http://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ForBiggerBlazes.mp4"
        }
    ];

    const playlistContainer = document.getElementById('playlist');
    let currentIdx = -1;

    document.getElementById('fileInput').addEventListener('change', function(event) {
        const files = Array.from(event.target.files);
        files.forEach((file) => {
            const fileUrl = URL.createObjectURL(file);
            const isVideo = file.type.startsWith('video/');
            tracks.push({
                title: file.name.replace(/\.[^/.]+$/, ""),
                audioUrl: fileUrl,
                videoUrl: isVideo ? fileUrl : null
            });
        });
        initPlaylist();
    });

    function initPlaylist() {
        playlistContainer.innerHTML = '';
        tracks.forEach((track, index) => {
            const card = document.createElement('div');
            card.className = 'track-card';
            card.id = `track-${index}`;
            const mediaContent = track.videoUrl 
                ? `<video src="${track.videoUrl}" loop muted id="vid-${index}" playsinline></video>`
                : `<div style="font-size: 2rem; opacity: 0.3;">🎵</div>`;

            card.innerHTML = `<div class="video-container">${mediaContent}</div><div class="track-info"><span class="track-num">${(index + 1).toString().padStart(2, '0')}</span><span class="track-name">${track.title}</span></div>`;
            card.onclick = () => selectTrack(index);
            playlistContainer.appendChild(card);
        });
    }

    function selectTrack(index) {
        if (index < 0 || index >= tracks.length) return;
        if (currentIdx !== -1) {
            const prevCard = document.getElementById(`track-${currentIdx}`);
            if(prevCard) prevCard.classList.remove('active');
            const prevVid = document.getElementById(`vid-${currentIdx}`);
            if (prevVid) { prevVid.pause(); prevVid.style.display = "none"; }
        }
        currentIdx = index;
        const track = tracks[index];
        const card = document.getElementById(`track-${index}`);
        const video = document.getElementById(`vid-${index}`);
        if(card) card.classList.add('active');
        document.getElementById('currentTitle').innerText = track.title;
        audio.src = track.audioUrl;
        audio.play().catch(e => console.log("Erro ao tocar"));
        if (video) { video.style.display = "block"; video.play(); }
        document.getElementById('playPauseBtn').innerHTML = "<b>II</b>";
    }

    document.getElementById('playPauseBtn').onclick = () => {
        if (tracks.length === 0) return;
        if (currentIdx === -1) return selectTrack(0);
        const vid = document.getElementById(`vid-${currentIdx}`);
        if (audio.paused) { audio.play(); if(vid) vid.play(); document.getElementById('playPauseBtn').innerHTML = "<b>II</b>"; }
        else { audio.pause(); if(vid) vid.pause(); document.getElementById('playPauseBtn').innerHTML = "▶"; }
    };

    document.getElementById('nextBtn').onclick = () => tracks.length > 0 && selectTrack((currentIdx + 1) % tracks.length);
    document.getElementById('prevBtn').onclick = () => tracks.length > 0 && selectTrack((currentIdx - 1 + tracks.length) % tracks.length);

    audio.ontimeupdate = () => {
        if (!isNaN(audio.duration)) {
            document.getElementById('progressBar').value = (audio.currentTime / audio.duration) * 100;
            document.getElementById('curTime').innerText = formatTime(audio.currentTime);
        }
    };
    audio.onloadedmetadata = () => document.getElementById('totalTime').innerText = formatTime(audio.duration);
    document.getElementById('progressBar').oninput = (e) => audio.duration && (audio.currentTime = (e.target.value / 100) * audio.duration);
    function formatTime(sec) { let m = Math.floor(sec / 60); let s = Math.floor(sec % 60); return `${m}:${s < 10 ? '0' : ''}${s}`; }
    audio.onended = () => document.getElementById('nextBtn').click();

    initPlaylist();
</script>
</body>
</html>
