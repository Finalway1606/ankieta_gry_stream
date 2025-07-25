<!DOCTYPE html>
<html lang="pl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Ankieta - Wybierz grę do ogrania</title>
  <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@700&display=swap" rel="stylesheet" />
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" />
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
      background: #1a1a1a;
      color: #f0f0f0;
      margin: 0;
    }
    /* Górna belka dokładnie jak na finalway1606.github.io/wow */
    .top-bar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 40px;
      user-select: none;
    }
    .info-text {
      font-family: 'Orbitron', sans-serif;
      font-weight: 700;
      font-size: 1.9rem;
      color: #ffd700;
      max-width: 70%;
      line-height: 1.1;
      white-space: nowrap;
    }
    .social-icons {
      display: flex;
      gap: 18px;
      /* Ikonki po prawej */
      color: #ffd700;
      font-size: 1.6rem;
    }
    .social-icons a {
      color: #ffd700;
      transition: transform 0.2s;
      display: flex;
      align-items: center;
    }
    .social-icons a:hover,
    .social-icons svg:hover {
      transform: scale(1.2);
    }
    .social-icons svg {
      width: 24px;
      height: 24px;
      fill: #ffd700;
      transition: transform 0.2s;
    }

    h1 {
      color: #ffd700;
      margin-bottom: 20px;
    }
    .form-section {
      margin-bottom: 20px;
    }
    .checkbox-group {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
    }
    label {
      display: flex;
      align-items: center;
      gap: 5px;
      cursor: pointer;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 10px;
    }
    th, td {
      border: 1px solid #444;
      padding: 8px;
      text-align: center;
    }
    th {
      background-color: #333;
    }
    button {
      padding: 10px 20px;
      cursor: pointer;
      background-color: #444;
      color: white;
      border: none;
      margin-top: 10px;
    }
    button:hover {
      background-color: #666;
    }
    input[type='text'] {
      padding: 5px;
      margin-bottom: 10px;
      width: 200px;
    }
    .results-stats-container {
      display: flex;
      gap: 40px;
      margin-top: 20px;
      flex-wrap: wrap;
    }
    .results-container {
      flex: 1 1 400px;
      min-width: 300px;
    }
    .stats-container {
      flex: 1 1 400px;
      min-width: 300px;
    }
    #currentLeader {
      font-family: 'Orbitron', sans-serif;
      font-weight: 700;
      background-color: #ffd700;
      color: #1a1a1a;
      padding: 15px;
      border-radius: 8px;
      box-shadow: 0 0 10px #ffd700aa;
      text-align: center;
      font-size: 1.5em;
      margin-bottom: 20px;
      user-select: none;
    }
    #statsChart {
      width: 100% !important;
      height: 300px !important;
      background-color: #222;
      border-radius: 8px;
      box-shadow: 0 0 8px #444;
    }
  </style>
</head>
<body>

  <div class="top-bar">
    <div class="info-text">
      To ankieta, na podstawie której Kranik1606 będzie wybierał następną grę na stream.
    </div>
    <div class="social-icons">
      <a href="https://www.twitch.tv/kranik1606" target="_blank" title="Twitch"><i class="fab fa-twitch"></i></a>
      <a href="https://www.kick.com/kranik1606" target="_blank" title="Kick">
        <svg viewBox="0 0 512 512" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false">
          <path d="M360 85 137 194v152l65-33 98 63 60-143-58 18-23-49 61-56zM96 126v260h49v-260H96z" />
        </svg>
      </a>
      <a href="https://www.tiktok.com/@kranik1606" target="_blank" title="TikTok"><i class="fab fa-tiktok"></i></a>
      <a href="https://discord.gg/AW3kEsP2Jq" target="_blank" title="Discord"><i class="fab fa-discord"></i></a>
    </div>
  </div>

  <h1>Wybierz grę do ogrania</h1>

  <form id="selectionForm">
    <div class="form-section">
      <h3>Nick gracza:</h3>
      <input type="text" id="nickname" placeholder="Wpisz swój nick" required />
    </div>

    <div class="form-section">
      <h3>Gry:</h3>
      <div class="checkbox-group" id="gameCheckboxes"></div>
    </div>

    <button type="submit">Zapisz wybór</button>
    <button type="button" id="resetButton">Resetuj dane</button>
  </form>

  <h2>Aktualny lider głosowania:</h2>
  <div id="currentLeader">Brak głosów</div>

  <div class="results-stats-container">
    <div class="results-container">
      <h2>Wyniki:</h2>
      <table id="resultsTable">
        <thead>
          <tr>
            <th>Nick</th>
            <th>Wybrana gra</th>
          </tr>
        </thead>
        <tbody></tbody>
      </table>
    </div>

    <div class="stats-container">
      <h2>Statystyki:</h2>
      <canvas id="statsChart"></canvas>
      <ul id="statsList"></ul>
    </div>
  </div>

<script>
  const BIN_ID = '68839875f7e7a370d1edd472';
  const SECRET_KEY = '$2a$10$0wgbqWh8esrHLuiDPFo.q.O5/Zr8kDX/oT7sd5.QnMiGqFWYDsjnm';

  const games = [
    'Elden Ring',
    'Cyberpunk 2077',
    'Minecraft',
    'The Witcher 3',
    'Hades',
    'Among Us',
    'Valorant',
    'Stardew Valley'
  ];

  let stats = {};
  let users = [];

  const gameContainer = document.getElementById('gameCheckboxes');
  const statsList = document.getElementById('statsList');
  const resultsTable = document.querySelector('#resultsTable tbody');
  const currentLeaderDiv = document.getElementById('currentLeader');

  const ctx = document.getElementById('statsChart').getContext('2d');
  let chart = new Chart(ctx, {
    type: 'bar',
    data: {
      labels: [],
      datasets: [{
        label: 'Liczba głosów',
        data: [],
        backgroundColor: 'rgba(255, 215, 0, 0.7)',
        borderColor: 'rgba(255, 215, 0, 1)',
        borderWidth: 1,
        borderRadius: 5,
      }]
    },
    options: {
      responsive: true,
      scales: {
        y: {
          beginAtZero: true,
          ticks: { color: '#f0f0f0' },
          grid: { color: '#444' }
        },
        x: {
          ticks: { color: '#f0f0f0', maxRotation: 90, minRotation: 45 },
          grid: { display: false }
        }
      },
      plugins: {
        legend: {
          labels: { color: '#ffd700' }
        }
      }
    }
  });

  function createCheckbox(name) {
    const label = document.createElement('label');
    const checkbox = document.createElement('input');
    checkbox.type = 'checkbox';
    checkbox.name = 'game';
    checkbox.value = name;
    checkbox.addEventListener('change', () => enforceSingleSelection('game'));
    label.appendChild(checkbox);
    label.appendChild(document.createTextNode(name));
    return label;
  }

  function enforceSingleSelection(groupName) {
    const checkboxes = document.querySelectorAll(`input[name='${groupName}']`);
    checkboxes.forEach(cb => {
      if (cb !== event.target) cb.checked = false;
    });
  }

  function updateStatsDisplay() {
    statsList.innerHTML = '';
    Object.entries(stats).forEach(([key, count]) => {
      const li = document.createElement('li');
      li.textContent = `${key} - ${count}`;
      statsList.appendChild(li);
    });

    const labels = Object.keys(stats);
    const data = Object.values(stats);
    chart.data.labels = labels;
    chart.data.datasets[0].data = data;
    chart.update();

    updateLeader();
  }

  function loadResultsTable() {
    resultsTable.innerHTML = '';
    users.forEach(({ nickname, game }) => {
      const row = document.createElement('tr');
      row.innerHTML = `<td>${nickname}</td><td>${game}</td>`;
      resultsTable.appendChild(row);
    });
  }

  function updateLeader() {
    if (Object.keys(stats).length === 0) {
      currentLeaderDiv.textContent = 'Brak głosów';
      return;
    }
    let maxVotes = 0;
    let leader = '';
    for (const [game, count] of Object.entries(stats)) {
      if (count > maxVotes) {
        maxVotes = count;
        leader = game;
      }
    }
    currentLeaderDiv.textContent = `${leader} z ${maxVotes} głosami`;
  }

  games.forEach(game => gameContainer.appendChild(createCheckbox(game)));

  async function loadSharedData() {
    try {
      const res = await fetch(`https://api.jsonbin.io/v3/b/${BIN_ID}/latest`, {
        headers: { 'X-Master-Key': SECRET_KEY }
      });
      const json = await res.json();
      const record = json.record || {};
      stats = record.stats || {};
      users = record.users || [];
      updateStatsDisplay();
      loadResultsTable();
    } catch (e) {
      console.error('Błąd przy ładowaniu danych:', e);
    }
  }

  async function syncSharedData() {
    try {
      await fetch(`https://api.jsonbin.io/v3/b/${BIN_ID}`, {
        method: 'PUT',
        headers: {
          'Content-Type': 'application/json',
          'X-Master-Key': SECRET_KEY,
          'X-Bin-Versioning': 'false'
        },
        body: JSON.stringify({ stats, users })
      });
    } catch (e) {
      console.error('Błąd przy zapisywaniu danych:', e);
    }
  }

  document.getElementById('selectionForm').addEventListener('submit', async (e) => {
    e.preventDefault();
    const nicknameInput = document.getElementById('nickname');
    const nickname = nicknameInput.value.trim();
    const selectedGameInput = document.querySelector("input[name='game']:checked");

    if (!nickname) {
      alert('Podaj swój nick.');
      return;
    }
    if (!selectedGameInput) {
      alert('Wybierz jedną grę.');
      return;
    }
    const game = selectedGameInput.value;

    const existingUserIndex = users.findIndex(u => u.nickname.toLowerCase() === nickname.toLowerCase());
    if (existingUserIndex !== -1) {
      const prevGame = users[existingUserIndex].game;
      stats[prevGame] = (stats[prevGame] || 1) - 1;
      if (stats[prevGame] <= 0) delete stats[prevGame];
      users.splice(existingUserIndex, 1);
    }

    users.push({ nickname, game });
    stats[game] = (stats[game] || 0) + 1;

    updateStatsDisplay();
    loadResultsTable();
    await syncSharedData();

    nicknameInput.value = '';
    selectedGameInput.checked = false;
    alert('Twój wybór został zapisany!');
  });

  document.getElementById('resetButton').addEventListener('click', async () => {
    const pass = prompt('Podaj hasło do resetu:');
    if (pass !== 'kranikreset') {
      alert('Niepoprawne hasło. Reset anulowany.');
      return;
    }
    if (!confirm('Na pewno chcesz zresetować wszystkie dane?')) return;

    stats = {};
    users = [];
    updateStatsDisplay();
    loadResultsTable();
    await syncSharedData();
  });

  loadSharedData();
</script>

</body>
</html>
