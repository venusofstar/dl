const TMDB_API_KEY = "b5632a62ba8688ec27b39712c1d5cfcc";
const TMDB_IMG_BASE = "https://image.tmdb.org/t/p/w500";
const VIDVAULT_MOVIE = "https://vidvault.ru/movie/";
const VIDVAULT_TV    = "https://vidvault.ru/tv/";

let currentShowId = null, showSeasons = [];

// ✅ OPEN PLAYER — Movies direct / Series → LOAD ALL SEASONS FROM TMDB
async function openFullscreenPlayer(type, directUrl = null, showId = null){
  const overlay = document.getElementById('globalPlayer');
  const frame = document.getElementById('streamFrame');
  const selector = document.getElementById('seriesSelector');

  if(type === 'movie'){
    selector.style.display = 'none';
    frame.src = directUrl;
    overlay.classList.add('active');
    document.body.style.overflow = 'hidden';
    return;
  }

  // 📺 SERIES: Fetch & list EVERY Season automatically
  currentShowId = showId;
  selector.style.display = 'flex';
  overlay.classList.add('active');
  document.body.style.overflow = 'hidden';

  const seasonSelect = document.getElementById('seasonSelect');
  const episodeSelect = document.getElementById('episodeSelect');
  seasonSelect.innerHTML = '<option>Loading seasons…</option>';
  episodeSelect.innerHTML = '<option>—</option>';
  frame.src = '';

  try{
    const res = await fetch(`https://api.themoviedb.org/3/tv/${showId}?api_key=${TMDB_API_KEY}&language=en-US`);
    if(!res.ok) throw new Error('API Error');
    const data = await res.json();
    showSeasons = data.seasons?.filter(s => s.season_number > 0) || [];

    if(!showSeasons.length){
      seasonSelect.innerHTML = '<option>No seasons found</option>';
      return;
    }

    // ✅ SHOW ALL SEASONS
    seasonSelect.innerHTML = '';
    showSeasons.forEach(season => {
      const opt = document.createElement('option');
      opt.value = season.season_number;
      opt.textContent = `Season ${season.season_number} (${season.episode_count} Eps)`;
      seasonSelect.appendChild(opt);
    });
    seasonChanged(); // load eps for S1 automatically
  }catch(err){
    seasonSelect.innerHTML = `<option>⚠️ Cannot load seasons</option>`;
    console.warn('TMDB unreachable — using fallback:', err);
    // Fallback: House of the Dragon known structure
    if(showId === 94997){
      showSeasons = [{season_number:1,episode_count:10}];
      seasonSelect.innerHTML = '<option value="1">Season 1 (10 Eps)</option>';
      seasonChanged();
    }
  }
}

// ✅ When Season changes → load correct number of Episodes
function seasonChanged(){
  const selNum = parseInt(document.getElementById('seasonSelect').value);
  const season = showSeasons.find(s => s.season_number === selNum);
  const count = season?.episode_count || 1;

  const episodeSelect = document.getElementById('episodeSelect');
  episodeSelect.innerHTML = '';
  for(let e = 1; e <= count; e++){
    const opt = document.createElement('option');
    opt.value = e;
    opt.textContent = `Episode ${e}`;
    episodeSelect.appendChild(opt);
  }
  playEpisode();
}

// ✅ Build & open VidVault link: /tv/ID/SEASON/EPISODE
function playEpisode(){
  const s = document.getElementById('seasonSelect').value;
  const e = document.getElementById('episodeSelect').value;
  document.getElementById('streamFrame').src = `${VIDVAULT_TV}${currentShowId}/${s}/${e}`;
}

// ✕ CLOSE PLAYER — CLEAN EVERYTHING
function closeFullscreenPlayer(){
  const overlay = document.getElementById('globalPlayer');
  const frame = document.getElementById('streamFrame');
  const selector = document.getElementById('seriesSelector');
  overlay.classList.remove('active');
  frame.src = '';
  selector.style.display = 'none';
  document.body.style.overflow = '';
  currentShowId = null; showSeasons = [];
  if((document.fullscreenElement||document.webkitFullscreenElement||document.msFullscreenElement)){
    if(document.exitFullscreen) document.exitFullscreen();
    else if(document.webkitExitFullscreen) document.webkitExitFullscreen();
    else if(document.msExitFullscreen) document.msExitFullscreen();
  }
}

// ESC / BACKSPACE CLOSE
document.addEventListener('keydown',e=>{
  if((e.key==='Escape'||e.key==='Backspace') && document.getElementById('globalPlayer').classList.contains('active')){
    e.preventDefault(); closeFullscreenPlayer();
  }
});

// Tab Switching
const tabs=document.querySelectorAll('.tab'), cats=document.querySelectorAll('.category');
tabs.forEach(tab=>{
  tab.addEventListener('click',()=>{
    tabs.forEach(t=>t.classList.remove('active'));
    cats.forEach(c=>c.classList.remove('active'));
    tab.classList.add('active');
    document.getElementById(tab.dataset.cat).classList.add('active');
    document.querySelectorAll('.searchField').forEach(el=>el.value='');
    document.body.focus();
  });
});

function getEls(container){ return {grid:container.querySelector('.results'), loading:container.querySelector('.loading'), error:container.querySelector('.error')}; }

function renderItems(list, grid, type){
  if(!list.length){ grid.innerHTML='<p class="error">⚠️ API currently unavailable</p>'; return; }
  grid.innerHTML=list.map(m=>{
    const poster=m.poster_path? `${TMDB_IMG_BASE}${m.poster_path}`:'https://via.placeholder.com/300x420/242426/f8f9fa?text=No+Poster';
    const year=(m.release_date||m.first_air_date)? (m.release_date||m.first_air_date).substring(0,4):'TBA';
    const title=m.title||m.name||'Untitled';

    if(type==='tv'){
      return `
      <div class="card" tabindex="0" data-name="${title.toLowerCase()}">
        <div class="img-wrap" onclick="openFullscreenPlayer('tv',null,${m.id})">
          <img src="${poster}" alt="${title}" loading="lazy">
        </div>
        <div class="info">
          <h3>${title}</h3>
          <div class="desc">${year} · ⭐ ${(m.vote_average||0).toFixed(1)}<br>👆 Auto‑loads ALL Seasons</div>
          <button class="btn" onclick="openFullscreenPlayer('tv',null,${m.id})">📺 Select Season & Episode</button>
        </div>
      </div>`;
    }else{
      const streamLink=`${VIDVAULT_MOVIE}${m.id}`;
      return `
      <div class="card" tabindex="0" data-name="${title.toLowerCase()}">
        <div class="img-wrap" onclick="openFullscreenPlayer('movie','${streamLink}')">
          <img src="${poster}" alt="${title}" loading="lazy">
        </div>
        <div class="info">
          <h3>${title}</h3>
          <div class="desc">${year} · ⭐ ${(m.vote_average||0).toFixed(1)}<br>👆 Click → Full‑Screen View</div>
          <button class="btn" onclick="openFullscreenPlayer('movie','${streamLink}')">⬇️ Download / View</button>
        </div>
      </div>`;
    }
  }).join('');
}

async function loadData(url, containerEl, type){
  const {grid,loading,error}=getEls(containerEl);
  grid.innerHTML=''; loading.classList.remove('hidden'); error.classList.add('hidden');
  try{
    const res=await fetch(url);
    if(!res.ok) throw new Error('API Error');
    const data=await res.json();
    renderItems(data.results||[], grid, type);
  }catch(err){ 
    error.textContent='⚠️ TMDB API currently unreachable'; 
    error.classList.remove('hidden'); 
  }finally{ loading.classList.add('hidden'); }
}

const moviesCat=document.getElementById('movies');
const seriesCat=document.getElementById('series');

loadData(`https://api.themoviedb.org/3/movie/popular?api_key=${TMDB_API_KEY}&language=en-US`, moviesCat, 'movie');
loadData(`https://api.themoviedb.org/3/tv/popular?api_key=${TMDB_API_KEY}&language=en-US`, seriesCat, 'tv');

let timer;
document.querySelectorAll('.searchField').forEach(inp=>{
  inp.addEventListener('input',e=>{
    clearTimeout(timer);
    const q=e.target.value.trim();
    const cat=inp.closest('.category');
    const type=cat.id==='series'?'tv':'movie';
    const endpoint=q? `/search/${type}?query=${encodeURIComponent(q)}` : (type==='tv'?'/tv/popular':'/movie/popular');
    timer=setTimeout(()=> loadData(`https://api.themoviedb.org/3${endpoint}&api_key=${TMDB_API_KEY}&language=en-US`, cat, type), 400);
  });
});

// TV Remote Navigation
document.addEventListener('keydown',e=>{
  if(document.getElementById('globalPlayer').classList.contains('active')) return;
  const activeCat=document.querySelector('.category.active');
  const visibleCards=Array.from(activeCat.querySelectorAll('.card:not(.hidden)'));
  const focusable=[...Array.from(document.querySelectorAll('.tab')),...visibleCards.flatMap(c=>[c,c.querySelector('.btn')])].filter(Boolean);
  const idx=focusable.indexOf(document.activeElement);

  if(['ArrowUp','ArrowLeft'].includes(e.key)){e.preventDefault();if(idx>0)focusable[idx-1].focus()}
  else if(['ArrowDown','ArrowRight'].includes(e.key)){e.preventDefault();if(idx<focusable.length-1)focusable[idx+1].focus()}
  else if(['Enter',' '].includes(e.key)){
    e.preventDefault();
    if(document.activeElement.classList.contains('tab'))document.activeElement.click();
    else if(document.activeElement.classList.contains('img-wrap')||document.activeElement.classList.contains('btn'))document.activeElement.click();
    else if(document.activeElement.classList.contains('card'))document.activeElement.querySelector('.img-wrap')?.click()||document.activeElement.querySelector('.btn')?.focus();
  }
});
