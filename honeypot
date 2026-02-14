<?php
// honeypot.php
if ($_SERVER['REQUEST_METHOD'] == 'POST') {
  $log = fopen('honeypot_log.txt', 'a');
  fwrite($log, "IP: " . $_SERVER['REMOTE_ADDR'] . "\n");
  fwrite($log, "User-Agent: " . $_SERVER['HTTP_USER_AGENT'] . "\n");
  fwrite($log, "Data: " . json_encode($_POST) . "\n\n");
  fclose($log);
  header('Location: https://example.com'); // Redirige vers un site "normal"
  exit;
}
?>
<html><body>
  <form method="post">
    <input type="text" name="login" placeholder="Login">
    <input type="password" name="pass" placeholder="Password">
    <input type="submit">
  </form>
</body></html>

