<!DOCTYPE html>  
<html lang="nl">  
<head>  
<meta charset="UTF-8">  
<meta name="viewport" content="width=device-width, initial-scale=1.0">  
<title>GitHub Pusher</title>  
<style>  
  @import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;600;700&family=Syne:wght@400;700;800&display=swap');  
  
  :root {  
    --bg: #0d0f10;  
    --surface: #161a1d;  
    --border: #2a2f33;  
    --accent: #00e5a0;  
    --accent-dim: #00e5a020;  
    --warn: #ff6b35;  
    --text: #e8eaec;  
    --muted: #6b7280;  
    --input-bg: #1c2126;  
  }  
  
  * { box-sizing: border-box; margin: 0; padding: 0; }  
  
  body {  
    background: var(--bg);  
    color: var(--text);  
    font-family: 'JetBrains Mono', monospace;  
    min-height: 100vh;  
    padding: 24px 16px;  
  }  
  
  header {  
    display: flex;  
    align-items: baseline;  
    gap: 12px;  
    margin-bottom: 28px;  
    border-bottom: 1px solid var(--border);  
    padding-bottom: 16px;  
  }  
  
  header h1 {  
    font-family: 'Syne', sans-serif;  
    font-size: 22px;  
    font-weight: 800;  
    letter-spacing: -0.5px;  
    color: var(--accent);  
  }  
  
  header span {  
    font-size: 11px;  
    color: var(--muted);  
    letter-spacing: 1px;  
    text-transform: uppercase;  
  }  
  
  .section {  
    background: var(--surface);  
    border: 1px solid var(--border);  
    border-radius: 6px;  
    padding: 16px;  
    margin-bottom: 14px;  
  }  
  
  .section-title {  
    font-size: 10px;  
    letter-spacing: 2px;  
    text-transform: uppercase;  
    color: var(--muted);  
    margin-bottom: 12px;  
  }  
  
  .row {  
    display: flex;  
    gap: 10px;  
    margin-bottom: 10px;  
    flex-wrap: wrap;  
  }  
  
  .field {  
    display: flex;  
    flex-direction: column;  
    gap: 5px;  
    flex: 1;  
    min-width: 140px;  
  }  
  
  label {  
    font-size: 10px;  
    letter-spacing: 1.5px;  
    text-transform: uppercase;  
    color: var(--muted);  
  }  
  
  input, textarea, select {  
    background: var(--input-bg);  
    border: 1px solid var(--border);  
    color: var(--text);  
    font-family: 'JetBrains Mono', monospace;  
    font-size: 13px;  
    padding: 8px 10px;  
    border-radius: 4px;  
    outline: none;  
    transition: border-color 0.15s;  
    width: 100%;  
  }  
  
  input:focus, textarea:focus {  
    border-color: var(--accent);  
  }  
  
  input[type="password"] {  
    letter-spacing: 2px;  
  }  
  
  textarea {  
    resize: vertical;  
    min-height: 260px;  
    line-height: 1.5;  
    tab-size: 2;  
  }  
  
  .file-path-row {  
    display: flex;  
    gap: 8px;  
    align-items: flex-end;  
  }  
  
  .file-path-row .field { flex: 1; }  
  
  .commit-row {  
    display: flex;  
    gap: 10px;  
    align-items: flex-end;  
    flex-wrap: wrap;  
  }  
  
  .commit-row .field { flex: 1; min-width: 200px; }  
  
  button {  
    font-family: 'Syne', sans-serif;  
    font-weight: 700;  
    font-size: 13px;  
    letter-spacing: 1px;  
    cursor: pointer;  
    border-radius: 4px;  
    border: none;  
    padding: 10px 20px;  
    transition: all 0.15s;  
  }  
  
  .btn-push {  
    background: var(--accent);  
    color: #0d0f10;  
    white-space: nowrap;  
  }  
  
  .btn-push:hover { filter: brightness(1.1); }  
  .btn-push:active { transform: scale(0.98); }  
  .btn-push:disabled { opacity: 0.4; cursor: not-allowed; }  
  
  .btn-secondary {  
    background: var(--border);  
    color: var(--muted);  
    font-size: 11px;  
    padding: 8px 14px;  
  }  
  
  .btn-secondary:hover { background: #3a3f44; color: var(--text); }  
  
  #log {  
    background: #0a0c0d;  
    border: 1px solid var(--border);  
    border-radius: 6px;  
    padding: 14px;  
    min-height: 60px;  
    font-size: 12px;  
    line-height: 1.7;  
    white-space: pre-wrap;  
    word-break: break-all;  
    color: var(--muted);  
  }  
  
  .log-success { color: var(--accent); }  
  .log-error { color: var(--warn); }  
  .log-info { color: #60a5fa; }  
  
  .token-note {  
    font-size: 10px;  
    color: var(--muted);  
    margin-top: 6px;  
    line-height: 1.6;  
  }  
  
  .token-note a { color: var(--accent); text-decoration: none; }  
  
  .char-count {  
    font-size: 10px;  
    color: var(--muted);  
    text-align: right;  
    margin-top: 3px;  
  }  
  
  .file-list {  
    display: flex;  
    flex-wrap: wrap;  
    gap: 6px;  
    margin-top: 8px;  
  }  
  
  .file-chip {  
    background: var(--accent-dim);  
    border: 1px solid var(--accent);  
    color: var(--accent);  
    font-size: 10px;  
    padding: 3px 8px;  
    border-radius: 3px;  
    cursor: pointer;  
    transition: background 0.1s;  
  }  
  
  .file-chip:hover { background: #00e5a040; }  
  
  .spinner {  
    display: inline-block;  
    width: 10px;  
    height: 10px;  
    border: 2px solid #0d0f10;  
    border-top-color: transparent;  
    border-radius: 50%;  
    animation: spin 0.6s linear infinite;  
    margin-right: 6px;  
    vertical-align: middle;  
  }  
  
  @keyframes spin { to { transform: rotate(360deg); } }  
  
  .status-dot {  
    display: inline-block;  
    width: 6px;  
    height: 6px;  
    border-radius: 50%;  
    background: var(--muted);  
    margin-right: 6px;  
    vertical-align: middle;  
  }  
  
  .status-dot.ok { background: var(--accent); }  
  .status-dot.err { background: var(--warn); }  
</style>  
</head>  
<body>  
  
<header>  
  <h1>⬆ GitHub Pusher</h1>  
  <span>Claude Code → GitHub</span>  
</header>  
  
<!-- CONFIG -->  
<div class="section">  
  <div class="section-title">🔑 Configuratie</div>  
  <div class="row">  
    <div class="field">  
      <label>GitHub Token (PAT)</label>  
      <input type="password" id="token" placeholder="ghp_xxxxxxxxxxxx" autocomplete="off">  
    </div>  
  </div>  
  <div class="row">  
    <div class="field">  
      <label>Owner / Gebruiker</label>  
      <input type="text" id="owner" placeholder="dvgroenewoud-commits">  
    </div>  
    <div class="field">  
      <label>Repository</label>  
      <input type="text" id="repo" placeholder="Whispr-flow">  
    </div>  
    <div class="field">  
      <label>Branch</label>  
      <input type="text" id="branch" placeholder="main" style="max-width:120px">  
    </div>  
  </div>  
  <p class="token-note">  
    Token nodig? → <a href="https://github.com/settings/tokens/new" target="_blank">github.com/settings/tokens/new</a> — selecteer scope: <strong>repo</strong><br>  
    Instellingen worden lokaal opgeslagen (localStorage).  
  </p>  
  <div style="display:flex;gap:8px;margin-top:10px">  
    <button class="btn-secondary" onclick="saveConfig()">💾 Opslaan</button>  
    <button class="btn-secondary" onclick="testToken()">🔎 Token testen</button>  
  </div>  
</div>  
  
<!-- FILE -->  
<div class="section">  
  <div class="section-title">📄 Bestand</div>  
  <div class="file-path-row">  
    <div class="field">  
      <label>Bestandspad (in repo)</label>  
      <input type="text" id="filepath" placeholder="index.html  of  src/app.js">  
    </div>  
    <button class="btn-secondary" onclick="fetchFile()" style="margin-bottom:0;height:38px">⬇ Ophalen</button>  
  </div>  
  
  <div id="knownFiles" class="file-list" style="margin-bottom:8px"></div>  
  
  <div style="margin-top:10px">  
    <label>Bestandsinhoud</label>  
    <textarea id="content" placeholder="Plak hier je code..." spellcheck="false" oninput="updateCount()"></textarea>  
    <div class="char-count" id="charCount">0 tekens</div>  
  </div>  
</div>  
  
<!-- PUSH -->  
<div class="section">  
  <div class="section-title">🚀 Push naar GitHub</div>  
  <div class="commit-row">  
    <div class="field">  
      <label>Commit bericht</label>  
      <input type="text" id="commitMsg" placeholder="Update via GitHub Pusher">  
    </div>  
    <button class="btn-push" id="pushBtn" onclick="pushFile()">⬆ Push bestand</button>  
  </div>  
</div>  
  
<!-- LOG -->  
<div class="section">  
  <div class="section-title">📋 Log</div>  
  <div id="log">Wachten op actie...</div>  
</div>  
  
<script>  
const LS = {  
  get: k => localStorage.getItem('ghp_' + k) || '',  
  set: (k,v) => localStorage.setItem('ghp_' + k, v)  
};  
  
// Load saved config  
window.onload = () => {  
  document.getElementById('token').value = LS.get('token');  
  document.getElementById('owner').value = LS.get('owner');  
  document.getElementById('repo').value = LS.get('repo');  
  document.getElementById('branch').value = LS.get('branch') || 'main';  
  renderKnownFiles();  
};  
  
function saveConfig() {  
  LS.set('token', document.getElementById('token').value.trim());  
  LS.set('owner', document.getElementById('owner').value.trim());  
  LS.set('repo', document.getElementById('repo').value.trim());  
  LS.set('branch', document.getElementById('branch').value.trim());  
  log('✅ Configuratie opgeslagen.', 'success');  
}  
  
function getConfig() {  
  return {  
    token: document.getElementById('token').value.trim(),  
    owner: document.getElementById('owner').value.trim(),  
    repo: document.getElementById('repo').value.trim(),  
    branch: document.getElementById('branch').value.trim() || 'main'  
  };  
}  
  
function log(msg, type) {  
  const el = document.getElementById('log');  
  const ts = new Date().toLocaleTimeString('nl-NL');  
  const cls = type === 'success' ? 'log-success' : type === 'error' ? 'log-error' : 'log-info';  
  el.innerHTML += `<span class="${cls}">[${ts}] ${msg}</span>\n`;  
  el.scrollTop = el.scrollHeight;  
}  
  
function updateCount() {  
  const n = document.getElementById('content').value.length;  
  document.getElementById('charCount').textContent = n.toLocaleString('nl-NL') + ' tekens';  
}  
  
// Known files per repo  
function knownFilesKey() {  
  const c = getConfig();  
  return `files_${c.owner}_${c.repo}`;  
}  
  
function addKnownFile(path) {  
  let files = JSON.parse(localStorage.getItem(knownFilesKey()) || '[]');  
  if (!files.includes(path)) { files.unshift(path); files = files.slice(0, 20); }  
  localStorage.setItem(knownFilesKey(), JSON.stringify(files));  
  renderKnownFiles();  
}  
  
function renderKnownFiles() {  
  const files = JSON.parse(localStorage.getItem(knownFilesKey()) || '[]');  
  const el = document.getElementById('knownFiles');  
  el.innerHTML = files.map(f =>  
    `<span class="file-chip" onclick="quickLoad('${f}')" title="Laad ${f}">${f}</span>`  
  ).join('');  
}  
  
function quickLoad(path) {  
  document.getElementById('filepath').value = path;  
  fetchFile();  
}  
  
async function testToken() {  
  const { token, owner } = getConfig();  
  if (!token) { log('⚠️ Vul eerst een token in.', 'error'); return; }  
  log('Testen...', 'info');  
  try {  
    const r = await fetch(`https://api.github.com/user`, {  
      headers: { Authorization: `token ${token}`, Accept: 'application/vnd.github.v3+json' }  
    });  
    const d = await r.json();  
    if (r.ok) log(`✅ Token geldig — ingelogd als: ${d.login}`, 'success');  
    else log(`❌ Token ongeldig: ${d.message}`, 'error');  
  } catch(e) { log('❌ Netwerkfout: ' + e.message, 'error'); }  
}  
  
let currentSha = null;  
  
async function fetchFile() {  
  const { token, owner, repo, branch } = getConfig();  
  const path = document.getElementById('filepath').value.trim();  
  if (!path) { log('⚠️ Vul een bestandspad in.', 'error'); return; }  
  if (!token || !owner || !repo) { log('⚠️ Vul configuratie in.', 'error'); return; }  
  
  log(`⬇ Ophalen: ${path} (${branch})...`, 'info');  
  try {  
    const r = await fetch(`https://api.github.com/repos/${owner}/${repo}/contents/${path}?ref=${branch}`, {  
      headers: { Authorization: `token ${token}`, Accept: 'application/vnd.github.v3+json' }  
    });  
    const d = await r.json();  
    if (r.ok) {  
      currentSha = d.sha;  
      const decoded = decodeURIComponent(escape(atob(d.content.replace(/\n/g, ''))));  
      document.getElementById('content').value = decoded;  
      updateCount();  
      addKnownFile(path);  
      log(`✅ Bestand geladen (${decoded.length} tekens, sha: ${d.sha.slice(0,7)})`, 'success');  
    } else {  
      currentSha = null;  
      log(`⚠️ Niet gevonden (${d.message}) — nieuw bestand wordt aangemaakt bij push.`, 'info');  
    }  
  } catch(e) { log('❌ Fout: ' + e.message, 'error'); }  
}  
  
async function pushFile() {  
  const { token, owner, repo, branch } = getConfig();  
  const path = document.getElementById('filepath').value.trim();  
  const content = document.getElementById('content').value;  
  const msg = document.getElementById('commitMsg').value.trim() || 'Update via GitHub Pusher';  
  
  if (!token || !owner || !repo) { log('⚠️ Vul configuratie in en sla op.', 'error'); return; }  
  if (!path) { log('⚠️ Vul een bestandspad in.', 'error'); return; }  
  if (!content) { log('⚠️ Bestandsinhoud is leeg.', 'error'); return; }  
  
  const btn = document.getElementById('pushBtn');  
  btn.disabled = true;  
  btn.innerHTML = '<span class="spinner"></span>Pushen...';  
  
  // If no sha cached, try to fetch it first  
  if (!currentSha) {  
    try {  
      const r = await fetch(`https://api.github.com/repos/${owner}/${repo}/contents/${path}?ref=${branch}`, {  
        headers: { Authorization: `token ${token}`, Accept: 'application/vnd.github.v3+json' }  
      });  
      if (r.ok) { const d = await r.json(); currentSha = d.sha; }  
    } catch(e) {}  
  }  
  
  const encoded = btoa(unescape(encodeURIComponent(content)));  
  const body = { message: msg, content: encoded, branch };  
  if (currentSha) body.sha = currentSha;  
  
  log(`⬆ Pushen naar ${owner}/${repo}/${path} (${branch})...`, 'info');  
  
  try {  
    const r = await fetch(`https://api.github.com/repos/${owner}/${repo}/contents/${path}`, {  
      method: 'PUT',  
      headers: {  
        Authorization: `token ${token}`,  
        Accept: 'application/vnd.github.v3+json',  
        'Content-Type': 'application/json'  
      },  
      body: JSON.stringify(body)  
    });  
    const d = await r.json();  
    if (r.ok) {  
      currentSha = d.content.sha;  
      addKnownFile(path);  
      log(`✅ Gepushed! Commit: ${d.commit.sha.slice(0,7)} — "${msg}"`, 'success');  
      log(`🔗 ${d.content.html_url}`, 'success');  
    } else {  
      log(`❌ Fout: ${d.message}`, 'error');  
    }  
  } catch(e) {  
    log('❌ Netwerkfout: ' + e.message, 'error');  
  }  
  
  btn.disabled = false;  
  btn.innerHTML = '⬆ Push bestand';  
}  
</script>  
</body>  
</html>  
