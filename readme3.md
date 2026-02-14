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
