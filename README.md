<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>宇都宮大学生協 陽東食堂 - メニュー</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header>
        <h1>🍜 宇都宮大学生協 陽東食堂</h1>
        <p>本日のメニュー</p>
    </header>

    <main>
        <div class="menu-container" id="menuContainer">
            <!-- メニューがここに表示されます -->
        </div>
    </main>

    <footer>
        <p>&copy; 2026 宇都宮大学生協 陽東食堂</p>
    </footer>

    <script src="script.js"></script>
</body>
</html>


* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: 'Arial', sans-serif;
    background-color: #f5f5f5;
    color: #333;
}

header {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    padding: 30px 20px;
    text-align: center;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

header h1 {
    font-size: 2em;
    margin-bottom: 10px;
}

header p {
    font-size: 1.1em;
    opacity: 0.9;
}

main {
    max-width: 1200px;
    margin: 30px auto;
    padding: 0 20px;
}

footer {
    background-color: #333;
    color: white;
    text-align: center;
    padding: 20px;
    margin-top: 50px;
}

.menu-container {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 20px;
}

.menu-card {
    background: white;
    border-radius: 10px;
    overflow: hidden;
    box-shadow: 0 2px 15px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.menu-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 5px 25px rgba(0, 0, 0, 0.2);
}

.menu-card img {
    width: 100%;
    height: 200px;
    object-fit: cover;
}

.menu-card-info {
    padding: 15px;
}

.menu-card-name {
    font-size: 1.2em;
    font-weight: bold;
    margin-bottom: 10px;
}

.menu-card-price {
    font-size: 1.5em;
    color: #667eea;
    font-weight: bold;
}

.login-section {
    background: white;
    padding: 30px;
    border-radius: 10px;
    box-shadow: 0 2px 15px rgba(0, 0, 0, 0.1);
    max-width: 400px;
    margin: 0 auto;
}

.login-section h2 {
    margin-bottom: 20px;
    text-align: center;
}

.login-section input {
    width: 100%;
    padding: 12px;
    margin-bottom: 15px;
    border: 1px solid #ddd;
    border-radius: 5px;
    font-size: 1em;
}

.login-section button {
    width: 100%;
    padding: 12px;
    background-color: #667eea;
    color: white;
    border: none;
    border-radius: 5px;
    font-size: 1em;
    cursor: pointer;
    transition: background-color 0.3s ease;
}

.login-section button:hover {
    background-color: #764ba2;
}

.error-message {
    color: red;
    text-align: center;
    margin-top: 10px;
}

.admin-section {
    background: white;
    padding: 30px;
    border-radius: 10px;
    box-shadow: 0 2px 15px rgba(0, 0, 0, 0.1);
}

.admin-section h2 {
    margin: 20px 0 15px 0;
    border-bottom: 2px solid #667eea;
    padding-bottom: 10px;
}

#addMenuForm {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr auto;
    gap: 10px;
    margin-bottom: 30px;
}

#addMenuForm input {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
    font-size: 0.9em;
}

#addMenuForm button {
    padding: 10px 20px;
    background-color: #667eea;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease;
}

#addMenuForm button:hover {
    background-color: #764ba2;
}

.menu-list {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    gap: 15px;
    margin-bottom: 30px;
}

.admin-menu-card {
    background: #f9f9f9;
    border: 1px solid #ddd;
    border-radius: 8px;
    padding: 15px;
    position: relative;
}

.admin-menu-card img {
    width: 100%;
    height: 150px;
    object-fit: cover;
    border-radius: 5px;
    margin-bottom: 10px;
}

.admin-menu-card-name {
    font-weight: bold;
    margin-bottom: 5px;
}

.admin-menu-card-price {
    color: #667eea;
    font-weight: bold;
    margin-bottom: 10px;
}

.delete-btn {
    width: 100%;
    padding: 8px;
    background-color: #ff6b6b;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease;
}

.delete-btn:hover {
    background-color: #ff5252;
}

.logout-btn {
    padding: 12px 20px;
    background-color: #999;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 1em;
    transition: background-color 0.3s ease;
}

.logout-btn:hover {
    background-color: #777;
}

@media (max-width: 768px) {
    #addMenuForm {
        grid-template-columns: 1fr;
    }

    .menu-container {
        grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    }
}



document.addEventListener('DOMContentLoaded', loadMenu);

async function loadMenu() {
    try {
        const response = await fetch('menu-data.json');
        const data = await response.json();
        displayMenu(data.menu);
    } catch (error) {
        console.error('メニュー読み込みエラー:', error);
        document.getElementById('menuContainer').innerHTML = '<p>メニューの読み込みに失敗しました。</p>';
    }
}

function displayMenu(menuItems) {
    const container = document.getElementById('menuContainer');
    container.innerHTML = '';

    if (menuItems.length === 0) {
        container.innerHTML = '<p>メニューはまだ登録されていません。</p>';
        return;
    }

    menuItems.forEach(item => {
        const card = document.createElement('div');
        card.className = 'menu-card';
        card.innerHTML = `
            <img src="${item.image}" alt="${item.name}" onerror="this.src='https://via.placeholder.com/300x200?text=画像なし'">
            <div class="menu-card-info">
                <div class="menu-card-name">${item.name}</div>
                <div class="menu-card-price">¥${item.price}</div>
            </div>
        `;
        container.appendChild(card);
    });
}



<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>管理画面 - メニュー編集</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header>
        <h1>🔐 管理画面 - メニュー編集</h1>
    </header>

    <main>
        <div id="loginSection" class="login-section">
            <h2>パスワード入力</h2>
            <input type="password" id="passwordInput" placeholder="パスワードを入力してください">
            <button onclick="login()">ログイン</button>
            <p id="loginError" class="error-message"></p>
        </div>

        <div id="adminSection" class="admin-section" style="display: none;">
            <h2>メニュー追加</h2>
            <form id="addMenuForm">
                <input type="text" id="menuName" placeholder="料理の名前" required>
                <input type="number" id="menuPrice" placeholder="値段（円）" required>
                <input type="text" id="menuImage" placeholder="画像URL（例：https://example.com/image.jpg）" required>
                <button type="submit">追加</button>
            </form>

            <h2>現在のメニュー</h2>
            <div id="menuList" class="menu-list">
            </div>

            <button onclick="logout()" class="logout-btn">ログアウト</button>
        </div>
    </main>

    <footer>
        <p>&copy; 2026 宇都宮大学生協 陽東食堂</p>
    </footer>

    <script src="admin.js"></script>
</body>
</html>


const ADMIN_PASSWORD = 'admin123';

let menuData = [];

document.addEventListener('DOMContentLoaded', loadMenuData);

function login() {
    const password = document.getElementById('passwordInput').value;
    
    if (password === ADMIN_PASSWORD) {
        document.getElementById('loginSection').style.display = 'none';
        document.getElementById('adminSection').style.display = 'block';
        displayAdminMenu();
    } else {
        document.getElementById('loginError').textContent = '❌ パスワードが間違っています';
        document.getElementById('passwordInput').value = '';
    }
}

function logout() {
    document.getElementById('loginSection').style.display = 'block';
    document.getElementById('adminSection').style.display = 'none';
    document.getElementById('passwordInput').value = '';
    document.getElementById('loginError').textContent = '';
}

async function loadMenuData() {
    try {
        const response = await fetch('menu-data.json');
        const data = await response.json();
        menuData = data.menu;
    } catch (error) {
        console.error('データ読み込みエラー:', error);
        menuData = [];
    }
}

function displayAdminMenu() {
    const listContainer = document.getElementById('menuList');
    listContainer.innerHTML = '';

    if (menuData.length === 0) {
        listContainer.innerHTML = '<p>メニューがまだ登録されていません。</p>';
        return;
    }

    menuData.forEach((item, index) => {
        const card = document.createElement('div');
        card.className = 'admin-menu-card';
        card.innerHTML = `
            <img src="${item.image}" alt="${item.name}" onerror="this.src='https://via.placeholder.com/250x150?text=画像なし'">
            <div class="admin-menu-card-name">${item.name}</div>
            <div class="admin-menu-card-price">¥${item.price}</div>
            <button class="delete-btn" onclick="deleteMenu(${index})">❌ 削除</button>
        `;
        listContainer.appendChild(card);
    });
}

document.getElementById('addMenuForm')?.addEventListener('submit', function(e) {
    e.preventDefault();

    const name = document.getElementById('menuName').value;
    const price = document.getElementById('menuPrice').value;
    const image = document.getElementById('menuImage').value;

    if (name && price && image) {
        menuData.push({
            name: name,
            price: parseInt(price),
            image: image
        });

        localStorage.setItem('menuData', JSON.stringify(menuData));

        document.getElementById('addMenuForm').reset();

        displayAdminMenu();
        alert('✅ メニューが追加されました！');
    }
});

function deleteMenu(index) {
    if (confirm('このメニューを削除してもよろしいですか？')) {
        menuData.splice(index, 1);
        localStorage.setItem('menuData', JSON.stringify(menuData));
        displayAdminMenu();
        alert('✅ メニューが削除されました！');
    }
}

window.addEventListener('load', function() {
    const savedData = localStorage.getItem('menuData');
    if (savedData) {
        menuData = JSON.parse(savedData);
    }
});


{
  "menu": [
    {"name": "豚カツ丼", "price": 850, "image": "https://via.placeholder.com/300x200?text=豚カツ丼"},
    {"name": "唐揚げ定食", "price": 900, "image": "https://via.placeholder.com/300x200?text=唐揚げ定食"},
    {"name": "天ぷら盛り合わせ", "price": 750, "image": "https://via.placeholder.com/300x200?text=天ぷら"},
    {"name": "焼肉定食", "price": 950, "image": "https://via.placeholder.com/300x200?text=焼肉定食"},
    {"name": "味噌ラーメン", "price": 650, "image": "https://via.placeholder.com/300x200?text=味噌ラーメン"},
    {"name": "醤油ラーメン", "price": 620, "image": "https://via.placeholder.com/300x200?text=醤油ラーメン"},
    {"name": "豚骨ラーメン", "price": 700, "image": "https://via.placeholder.com/300x200?text=豚骨ラーメン"},
    {"name": "野菜炒め", "price": 550, "image": "https://via.placeholder.com/300x200?text=野菜炒め"},
    {"name": "ぎょうざ（6個）", "price": 400, "image": "https://via.placeholder.com/300x200?text=ぎょうざ"},
    {"name": "春巻き（4個）", "price": 380, "image": "https://via.placeholder.com/300x200?text=春巻き"},
    {"name": "鶏唐揚げ弁当", "price": 750, "image": "https://via.placeholder.com/300x200?text=唐揚げ弁当"},
    {"name": "親子丼", "price": 800, "image": "https://via.placeholder.com/300x200?text=親子丼"},
    {"name": "カレーライス", "price": 700, "image": "https://via.placeholder.com/300x200?text=カレーライス"},
    {"name": "オムライス", "price": 850, "image": "https://via.placeholder.com/300x200?text=オムライス"},
    {"name": "卵焼き定食", "price": 650, "image": "https://via.placeholder.com/300x200?text=卵焼き定食"},
    {"name": "肉うどん", "price": 700, "image": "https://via.placeholder.com/300x200?text=肉うどん"},
    {"name": "きつねうどん", "price": 600, "image": "https://via.placeholder.com/300x200?text=きつねうどん"},
    {"name": "天ぷらうどん", "price": 750, "image": "https://via.placeholder.com/300x200?text=天ぷらうどん"},
    {"name": "冷やし中華", "price": 650, "image": "https://via.placeholder.com/300x200?text=冷やし中華"},
    {"name": "焼きそば", "price": 600, "image": "https://via.placeholder.com/300x200?text=焼きそば"},
    {"name": "お好み焼き", "price": 700, "image": "https://via.placeholder.com/300x200?text=お好み焼き"},
    {"name": "たこ焼き（8個）", "price": 500, "image": "https://via.placeholder.com/300x200?text=たこ焼き"},
    {"name": "フライドポテト", "price": 350, "image": "https://via.placeholder.com/300x200?text=フライドポテト"},
    {"name": "から揚げ弁当（大盛）", "price": 900, "image": "https://via.placeholder.com/300x200?text=唐揚げ大盛"},
    {"name": "コロッケ定食", "price": 700, "image": "https://via.placeholder.com/300x200?text=コロッケ定食"},
    {"name": "メンチカツ定食", "price": 850, "image": "https://via.placeholder.com/300x200?text=メンチカツ"},
    {"name": "白身魚フライ定食", "price": 800, "image": "https://via.placeholder.com/300x200?text=白身魚フライ"},
    {"name": "エビフライ定食", "price": 950, "image": "https://via.placeholder.com/300x200?text=エビフライ"},
    {"name": "マグロ刺身定食", "price": 1050, "image": "https://via.placeholder.com/300x200?text=マグロ刺身"},
    {"name": "唐揚げ＆フライセット", "price": 1000, "image": "https://via.placeholder.com/300x200?text=セット"}
  ]
}


