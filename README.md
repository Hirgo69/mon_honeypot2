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
