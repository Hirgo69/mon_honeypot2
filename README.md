<!DOCTYPE html>
<html>
<head>
  <title>Connexion</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: url("https://images.unsplash.com/photo-1518770660439-4636190af475") no-repeat center center fixed;
      background-size: cover;
      color: white;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }

    .container {
      background: rgba(0, 0, 0, 0.85);
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

    <button class="register-btn" onclick="createAccount()">Créer un compte</button>
  </div>

  <script>
    document.getElementById('loginForm').addEventListener('submit', (e) => {
      e.preventDefault();
      const data = {
        login: document.getElementById('login').value,
        pass: document.getElementById('pass').value
      };
      localStorage.setItem('honeypot', JSON.stringify(data));
      alert('Connexion "réussie" !');
    });

    function createAccount() {
      alert("Fonction de création de compte bientôt disponible 😉");
    }
  </script>

</body>
</html>
