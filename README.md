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
      width: 300px;
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

    .hidden { display: none; }
  </style>
</head>
<body>

<div class="container" id="page">

  <!-- Contenu dynamique injecté par JS -->

</div>

<script>
const page = document.getElementById('page');

// Fonction pour charger la page d'accueil
function showHome() {
  page.innerHTML = `
    <h1>Bienvenue sur le Honeypot</h1>
    <button class="login-btn" onclick="showLogin()">Se connecter</button>
    <button class="register-btn" onclick="showRegister()">Créer un compte</button>
  `;
}

// Fonction pour afficher le formulaire de connexion
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
  `;

  document.getElementById('loginForm').addEventListener('submit', e => {
    e.preventDefault();
    loginUser();
  });
}

// Fonction pour afficher le formulaire de création de compte
function showRegister() {
  page.innerHTML = `
    <h1>Créer un compte</h1>
    <button class="register-btn" onclick="registerUser()">Créer un compte</button>
    <button class="login-btn" onclick="showLogin()">Se connecter</button>
    <button class="register-btn" onclick="showHome()">Accueil</button>
  `;
}

// Fonction création de compte
function registerUser() {
  const login = prompt("Choisis un login :");
  const pass = prompt("Choisis un mot de passe :");
  
  if (!login || !pass) {
    alert("Login et mot de passe obligatoires !");
    return;
  }

  const users = JSON.parse(localStorage.getItem('users') || '{}');
  if (users[login]) {
    alert("Ce login existe déjà !");
    return;
  }

  users[login] = pass;
  localStorage.setItem('users', JSON.stringify(users));
  alert("Compte créé avec succès !");
}

// Fonction connexion
function loginUser() {
  const login = document.getElementById('login').value;
  const pass = document.getElementById('pass').value;

  const users = JSON.parse(localStorage.getItem('users') || '{}');

  if (users[login] && users[login] === pass) {
    alert(`Connexion réussie ! Bienvenue ${login}`);
    localStorage.setItem('lastLogin', login);
  } else {
    alert("Login ou mot de passe incorrect !");
  }
}

// Affiche la page d'accueil au lancement
showHome();
</script>

</body>
</html>
