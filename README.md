# Leitstelle.
Leitstelle für jeden.
<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8">
<title>Leitstelle</title>

<style>
body { font-family: Arial; background:#0b0f1a; color:white; margin:0; }
.box { width:300px; margin:100px auto; }
input, button { width:100%; padding:10px; margin:5px 0; }
button { background:#3b82f6; border:none; color:white; }
.dashboard { display:none; padding:20px; }
.card { background:#141a2a; padding:10px; margin:10px 0; border-radius:10px; }
textarea { width:100%; height:60px; background:#1c2336; color:white; }
</style>

</head>

<body>

<div id="login" class="box">
  <h2>Login</h2>
  <input id="email" placeholder="Email">
  <input id="pass" type="password" placeholder="Passwort">
  <button onclick="register()">Registrieren</button>
  <button onclick="loginUser()">Login</button>
</div>

<div id="app" class="dashboard">
  <h2>Leitstelle</h2>

  <div class="card">
    Aktueller Stand
    <textarea id="stand"></textarea>
  </div>

  <div class="card">
    Fortschritt
    <textarea id="fortschritt"></textarea>
  </div>

  <div class="card">
    Probleme
    <textarea id="probleme"></textarea>
  </div>

  <button onclick="save()">Speichern</button>
</div>

<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
import { getAuth, createUserWithEmailAndPassword, signInWithEmailAndPassword } 
from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";
import { getFirestore, doc, setDoc } 
from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

const firebaseConfig = {
  apiKey: "DEIN_API_KEY",
  authDomain: "DEIN_AUTH_DOMAIN",
  projectId: "DEIN_PROJECT_ID"
};

const app = initializeApp(firebaseConfig);
const auth = getAuth(app);
const db = getFirestore(app);

window.register = () => {
  createUserWithEmailAndPassword(auth, email.value, pass.value);
};

window.loginUser = () => {
  signInWithEmailAndPassword(auth, email.value, pass.value)
    .then(()=>{
      login.style.display="none";
      app.style.display="block";
    });
};

window.save = async () => {
  const user = auth.currentUser;
  await setDoc(doc(db,"leitstelle",user.uid), {
    stand: stand.value,
    fortschritt: fortschritt.value,
    probleme: probleme.value
  });
};
</script>

</body>
</html>
