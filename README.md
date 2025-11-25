<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <title>Коллекция данных</title>

  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 800px;
      margin: 0 auto;
      padding: 30px;
      background: #f0f3f7;
    }

    /* Анимация эмблемы */
    @keyframes shine {
      0% { transform: scale(1); filter: brightness(1); }
      40% { transform: scale(1.2); filter: brightness(1.5); }
      100% { transform: scale(1); filter: brightness(1); }
    }

    .logo {
      width: 60px;
      height: 60px;
      animation: shine 1.8s ease-out 1;
    }

    /* Плавное появление */
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }

    .fade-in {
      animation: fadeIn .4s ease-out;
    }

    header {
      display: flex;
      align-items: center;
      gap: 15px;
      margin-bottom: 25px;
    }

    h1 {
      margin: 0;
      font-size: 28px;
      color: #333;
    }

    /* Карточки */
    .block {
      background: white;
      padding: 18px;
      border-radius: 12px;
      margin-bottom: 18px;
      box-shadow: 0 2px 6px rgba(0,0,0,0.12);
      animation: fadeIn .4s ease-out;
    }

    input, button, select {
      padding: 8px;
      margin: 6px 0;
      border-radius: 6px;
      border: 1px solid #ccc;
    }

    button {
      background: #4A90E2;
      color: white;
      border: none;
      cursor: pointer;
      transition: background .2s;
    }
    button:hover {
      background: #3f7ec5;
    }

    .item {
      padding: 12px;
      background: #fff;
      border-radius: 10px;
      border: 1px solid #ddd;
      margin-bottom: 8px;
      box-shadow: 0 1px 3px rgba(0,0,0,0.1);
      transition: transform .25s ease, opacity .25s ease;
      animation: fadeIn .4s ease-out;
    }

    .item:hover {
      transform: scale(1.02);
    }

    .delete-btn {
      background: #d9534f;
      float: right;
    }
    .delete-btn:hover {
      background: #c64541;
    }
  </style>
</head>

<body>

  <header>
    <svg class="logo" viewBox="0 0 100 100">
      <circle cx="50" cy="50" r="45" fill="#4A90E2"></circle>
      <text x="50" y="60" text-anchor="middle" font-size="42" fill="white">C</text>
    </svg>
    <h1>Коллекция данных</h1>
  </header>

  <div class="block">
    <h3>Добавить элемент</h3>
    <input id="nameInput" placeholder="Название" />
    <input id="valueInput" placeholder="Значение" />
    <button onclick="addItem()">Добавить</button>
  </div>

  <div class="block">
    <h3>Поиск</h3>
    <input id="searchInput" placeholder="Введите строку" oninput="searchItems()" />
  </div>

  <div class="block">
    <h3>Сортировка</h3>
    <select id="sortSelect" onchange="sortItems()">
      <option value="name">По названию</option>
      <option value="value">По значению</option>
    </select>
  </div>

  <h3>Список элементов</h3>
  <div id="list"></div>

  <script>
    let items = [];

    function render(list = items) {
      const container = document.getElementById('list');
      container.innerHTML = '';
      list.forEach((item, index) => {
        const div = document.createElement('div');
        div.className = 'item';
        div.innerHTML = `${item.name} — ${item.value}
          <button class="delete-btn" onclick="deleteItem(${index})">Удалить</button>`;
        container.appendChild(div);
      });
    }

    function addItem() {
      const name = document.getElementById('nameInput').value.trim();
      const value = document.getElementById('valueInput').value.trim();
      if (!name || !value) return;
      items.push({ name, value });
      render();
      document.getElementById('nameInput').value = '';
      document.getElementById('valueInput').value = '';
    }

    function deleteItem(index) {
      items.splice(index, 1);
      render();
    }

    function searchItems() {
      const q = document.getElementById('searchInput').value.toLowerCase();
      const filtered = items.filter(i =>
        i.name.toLowerCase().includes(q) || i.value.toLowerCase().includes(q)
      );
      render(filtered);
    }

    function sortItems() {
      const field = document.getElementById('sortSelect').value;
      items.sort((a, b) => a[field].localeCompare(b[field]));
      render();
    }
  </script>

</body>
</html>
