<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Honeypot - Accueil</title>
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
      background: rgba(0,0,0,0.9);
      padding: 30px;
      border-radius: 10px;
      width: 350px;
      text-align: center;
      box-shadow: 0 0 20px #00ffcc;
    }
    button {
      width: 100%;
      padding: 10px;
      margin: 10px 0;
      border: none;
      border-radius: 5px;
      font-weight: bold;
      cursor: pointer;
    }
    .login-btn { background-color: #00ffcc; color:black; }
    .register-btn { background-color: transparent; border: 1px solid #00ffcc; color:#00ffcc; }
    .register-btn:hover { background-color: #00ffcc; color:black; }
  </style>
</head>
<body>
  <div class="container">
    <h1>Bienvenue sur le Honeypot</h1>
    <button class="login-btn" onclick="window.location.href='login.html'">Se connecter</button>
    <button class="register-btn" onclick="window.location.href='register.html'">Créer un compte</button>
  </div>
</body>
</html>
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Créer un compte</title>
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
      background: rgba(0,0,0,0.9);
      padding: 30px;
      border-radius: 10px;
      width: 350px;
      text-align: center;
      box-shadow: 0 0 20px #00ffcc;
    }
    input { width: 100%; padding: 10px; margin: 8px 0; border:none; border-radius:5px; background-color:#111; color:#00ffcc; }
    button { width: 100%; padding: 10px; margin-top: 10px; border:none; border-radius:5px; font-weight:bold; cursor:pointer; }
    .login-btn { background-color: #00ffcc; color:black; }
    .register-btn { background-color: transparent; border: 1px solid #00ffcc; color:#00ffcc; }
    .register-btn:hover { background-color:#00ffcc; color:black; }
    .message { margin-top:10px; font-weight:bold; color:#ff5555; }
  </style>
</head>
<body>
<div class="container">
  <h1>Créer un compte</h1>
  <form id="registerForm">
    <input type="text" id="regLogin" placeholder="Login" required>
    <input type="password" id="regPass" placeholder="Password" required>
    <button type="submit" class="register-btn">Créer un compte</button>
  </form>
  <button class="login-btn" onclick="window.location.href='login.html'">Se connecter</button>
  <div class="message" id="registerMessage"></div>
</div>

<script>
document.getElementById('registerForm').addEventListener('submit', function(e){
  e.preventDefault();
  const login = document.getElementById('regLogin').value.trim();
  const pass = document.getElementById('regPass').value.trim();
  const message = document.getElementById('registerMessage');

  if(!login || !pass){ message.textContent="Login et mot de passe obligatoires !"; return; }

  const users = JSON.parse(localStorage.getItem('users')||'{}');
  if(users[login]){ message.textContent="Ce login existe déjà !"; return; }

  users[login] = pass;
  localStorage.setItem('users', JSON.stringify(users));
  message.style.color="#00ffcc";
  message.textContent="Compte créé avec succès !";
});
</script>
</body>
</html>
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Connexion</title>
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
      background: rgba(0,0,0,0.9);
      padding: 30px;
      border-radius: 10px;
      width: 350px;
      text-align: center;
      box-shadow: 0 0 20px #00ffcc;
    }
    input { width: 100%; padding: 10px; margin: 8px 0; border:none; border-radius:5px; background-color:#111; color:#00ffcc; }
    button { width: 100%; padding: 10px; margin-top: 10px; border:none; border-radius:5px; font-weight:bold; cursor:pointer; }
    .login-btn { background-color: #00ffcc; color:black; }
    .register-btn { background-color: transparent; border: 1px solid #00ffcc; color:#00ffcc; }
    .register-btn:hover { background-color:#00ffcc; color:black; }
    .message { margin-top:10px; font-weight:bold; color:#ff5555; }
  </style>
</head>
<body>
<div class="container">
  <h1>Connexion</h1>
  <form id="loginForm">
    <input type="text" id="login" placeholder="Login" required>
    <input type="password" id="pass" placeholder="Password" required>
    <button type="submit" class="login-btn">Se connecter</button>
  </form>
  <button class="register-btn" onclick="window.location.href='register.html'">Créer un compte</button>
  <div class="message" id="loginMessage"></div>
</div>

<script>
document.getElementById('loginForm').addEventListener('submit', function(e){
  e.preventDefault();
  const login = document.getElementById('login').value.trim();
  const pass = document.getElementById('pass').value.trim();
  const message = document.getElementById('loginMessage');
  const users = JSON.parse(localStorage.getItem('users')||'{}');

  if(users[login] && users[login] === pass){
    localStorage.setItem('lastLogin', login);
    window.location.href = 'welcome.html'; // redirection vers page bienvenue
  } else {
    message.textContent = "Login ou mot de passe incorrect !";
  }
});
</script>
</body>
</html>
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Bienvenue</title>
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
      background: rgba(0,0,0,0.9);
      padding: 30px;
      border-radius: 10px;
      width: 350px;
      text-align: center;
      box-shadow: 0 0 20px #00ffcc;
    }
    button { width: 100%; padding: 10px; margin-top: 20px; border:none; border-radius:5px; font-weight:bold; cursor:pointer; }
    .logout-btn { background-color: #ff5555; color:white; }
  </style>
</head>
<body>
<div class="container">
  <h1 id="welcomeMsg">Bienvenue !</h1>
  <p>Tu es maintenant connecté sur ton honeypot simulé 😎</p>
  <button class="logout-btn" onclick="logout()">Se déconnecter</button>
</div>

<script>
function logout(){
  localStorage.removeItem('lastLogin');
  window.location.href = 'index.html';
}

// afficher le login stocké
const user = localStorage.getItem('lastLogin');
if(user){
  document.getElementById('welcomeMsg').textContent = "Bienvenue, " + user + " !";
} else {
  window.location.href = 'index.html'; // si pas connecté, retour accueil
}
</script>
</body>
</html>
