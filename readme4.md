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
