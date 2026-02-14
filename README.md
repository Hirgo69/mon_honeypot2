<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Honeypot</title>
  <style>
    body {
      margin: 0;
      font-family: 'Courier New', monospace;
      background: url("https://images.unsplash.com/photo-1518770660439-4636190af475") no-repeat center center fixed;
      background-size: cover;
      color: #00ffcc;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }

    .container {
      background: rgba(0, 0, 0, 0.9);
      padding: 30px;
      border-radius: 10px;
      width: 350px;
      text-align: center;
      box-shadow: 0 0 20px #00ffcc;
    }

    input {
      width: 100%;
      padding: 10px;
      margin: 8px 0;
      border: none;
      border-radius: 5px;
      background-color: #111;
      color: #00ffcc;
    }

    button {
      width: 100%;
      padding: 10px;
      margin-top: 10px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      font-weight: bold;
    }

    .login-btn {
      background-color: #00ffcc;
      color: black;
    }

    .register-btn {
      background-color: transparent;
      border: 1px solid #00ffcc;
      color: #00ffcc;
    }

    .register-btn:hover {
      background-color: #00ffcc;
      color: black;
    }

    h1 {
      margin-bottom: 20px;
    }

    .message {
      margin-top: 10px;
      color: #ff5555;
      font-weight: bold;
    }

  </style>
</head>
<body>

<div class="container" id="page"></div>

<script>
const page = document.getElementById('page');

// PAGE D'ACCUEIL
function showHome() {
  page.innerHTML = `
    <h1>Bienvenue sur le Honeypot</h1>
    <button class="login-btn" onclick="showLogin()">Se connecter</button>
    <button class="register-btn" onclick="showRegister()">Créer un compte</button>
  `;
}

// PAGE CONNEXION
function showLogin() {
  page.innerHTML = `
    <h1>Connexion</h1>
    <form id="loginForm">
      <input type="text" id="login" placeholder="Login" required>
      <input type="password" id="pass" placeholder="Password" required>
      <button type="submit" class="login-btn">Se connecter</button>
    </form>
    <button class="register-btn" onclick="showRegister()">Créer un compte</button>
    <button class="register-btn" onclick="showHome()">Accueil</button>
    <div class="message" id="loginMessage"></div>
  `;

  document.getElementById('loginForm').addEventListener('submit', e => {
    e.preventDefault();
    loginUser();
  });
}

// PAGE CREATION COMPTE
function showRegister() {
  page.innerHTML = `
    <h1>Créer un compte</h1>
    <form id="registerForm">
      <input type="text" id="regLogin" placeholder="Login" required>
      <input type="password" id="regPass" placeholder="Password" required>
      <button type="submit" class="register-btn">Créer un compte</button>
    </form>
    <button class="login-btn" onclick="showLogin()">Se connecter</button>
    <button class="register-btn" onclick="showHome()">Accueil</button>
    <div class="message" id="registerMessage"></div>
  `;

  document.getElementById('registerForm').addEventListener('submit', e => {
    e.preventDefault();
    registerUser();
  });
}

// PAGE BIENVENUE APRES CONNEXION
function showWelcome(user) {
  page.innerHTML = `
    <h1>Bienvenue, ${user} !</h1>
    <p>Tu es maintenant connecté sur ton honeypot simulé 😎</p>
    <button class="register-btn" onclick="logout()">Se déconnecter</button>
  `;
}

// CREATION COMPTE
function registerUser() {
  const login = document.getElementById('regLogin').value.trim();
  const pass = document.getElementById('regPass').value.trim();
  const message = document.getElementById('registerMessage');

  if (!login || !pass) {
    message.textContent = "Login et mot de passe obligatoires !";
    return;
  }

  const users = JSON.parse(localStorage.getItem('users') || '{}');
  if (users[login]) {
    message.textContent = "Ce login existe déjà !";
    return;
  }

  users[login] = pass;
  localStorage.setItem('users', JSON.stringify(users));
  message.style.color = "#00ffcc";
  message.textContent = "Compte créé avec succès !";
}

// CONNEXION
function loginUser() {
  const login = document.getElementById('login').value.trim();
  const pass = document.getElementById('pass').value.trim();
  const message = document.getElementById('loginMessage');

  const users = JSON.parse(localStorage.getItem('users') || '{}');

  if (users[login] && users[login] === pass) {
    localStorage.setItem('lastLogin', login);
    showWelcome(login);
  } else {
    message.textContent = "Login ou mot de passe incorrect !";
  }
}

// DECONNEXION
function logout() {
  localStorage.removeItem('lastLogin');
  showHome();
}

// Au lancement, vérifier si l'utilisateur était déjà connecté
const lastUser = localStorage.getItem('lastLogin');
if (lastUser) {
  showWelcome(lastUser);
} else {
  showHome();
}
</script>

</body>
</html>
