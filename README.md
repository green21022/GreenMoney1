<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>GreenMoney</title>
  <script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-app-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-auth-compat.js"></script>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body {
      font-family: Arial, sans-serif;
      background: #f0fff4;
      color: #2d3748;
    }
    .menu-toggle {
      position: fixed;
      top: 15px;
      left: 15px;
      background: #38a169;
      color: white;
      border: none;
      padding: 10px 15px;
      font-size: 20px;
      cursor: pointer;
      z-index: 1001;
      border-radius: 4px;
    }
    .sidebar {
      width: 220px;
      background: #38a169;
      color: white;
      height: 100vh;
      position: fixed;
      top: 0;
      left: 0;
      padding: 20px;
      transform: translateX(-100%);
      transition: transform 0.3s ease;
      z-index: 1000;
    }
    .sidebar.active {
      transform: translateX(0);
    }
    .sidebar h2 {
      text-align: center;
      margin-bottom: 20px;
    }
    .sidebar a {
      display: block;
      color: white;
      text-decoration: none;
      margin: 10px 0;
      padding: 8px;
      border-radius: 4px;
    }
    .sidebar a:hover {
      background: #2f855a;
    }
    .main-content {
      margin-left: 0;
      padding: 20px;
    }
    header, footer {
      background: #38a169;
      color: #fff;
      text-align: center;
      padding: 1rem;
      border-radius: 6px;
      margin-bottom: 20px;
    }
    .btn {
      display: inline-block;
      margin-top: 1rem;
      padding: 0.5rem 1rem;
      background: #2f855a;
      color: white;
      text-decoration: none;
      border-radius: 5px;
    }
    section {
      padding: 1rem 0;
    }
    .task-option, .reward-option {
      padding: 1rem;
      background: #ffffff;
      border: 1px solid #ccc;
      border-radius: 5px;
      margin: 1rem 0;
    }
    form {
      background: #ffffff;
      padding: 1rem;
      max-width: 400px;
      margin: 1rem 0;
      border-radius: 5px;
      box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    }
    form input {
      width: 100%;
      padding: 0.5rem;
      margin-bottom: 1rem;
      border: 1px solid #ccc;
      border-radius: 3px;
    }
    form button {
      padding: 0.5rem 1rem;
      background: #38a169;
      color: white;
      border: none;
      border-radius: 3px;
      cursor: pointer;
    }
    #payeer-input { display: none; }
    #tasks, #rewards, #login, #signup { display: none; }
    .active-section { display: block !important; }
    @media (min-width: 768px) {
      .sidebar { transform: translateX(0); }
      .menu-toggle { display: none; }
      .main-content { margin-left: 220px; }
    }
    .sticky-footer {
      position: fixed;
      bottom: 0;
      left: 0;
      width: 100%;
      background-color: #38a169;
      color: white;
      text-align: center;
      padding: 10px 0;
      z-index: 100;
    }
    .sticky-footer ul {
      list-style: none;
      display: flex;
      justify-content: center;
      margin: 0;
      padding: 0;
    }
    .sticky-footer ul li {
      margin: 0 15px;
    }
    .sticky-footer ul li a {
      text-decoration: none;
      color: white;
      font-size: 14px;
    }
    .sticky-footer ul li a:hover {
      text-decoration: underline;
    }
  </style>
</head>
<body>
  <button class="menu-toggle" onclick="toggleSidebar()">☰</button>
  <div class="sidebar" id="sidebar">
    <h2>GreenMoney</h2>
    <a href="#hero" onclick="showSection('hero')">Home</a>
    <a href="#tasks" onclick="showSection('tasks')">Tasks</a>
    <a href="#rewards" onclick="showSection('rewards')">Rewards</a>
    <a href="#login" onclick="showSection('login')">Login</a>
    <a href="#signup" onclick="showSection('signup')">Signup</a>
  </div>
  <div class="main-content">
    <header><h1>Welcome to GreenMoney</h1></header><section id="hero" class="active-section">
  <h2>Turn Time Into Cash</h2>
  <p>Earn real money by completing simple online tasks.</p>
  <a href="#signup" class="btn" onclick="showSection('signup')">Start Earning</a>
</section>

<section id="tasks">
  <h3>Offerwalls</h3>
  <div class="task-option"><h4>OfferToro</h4><iframe src="https://www.offertoro.com/ifr/show/YOUR_APP_ID_HERE" width="100%" height="600" frameborder="0"></iframe></div>
  <div class="task-option"><h4>AdGem</h4><iframe src="https://wall.adgem.com/v1/wall?appid=YOUR_APP_ID&playerid=USER123" width="100%" height="600" frameborder="0"></iframe></div>
  <div class="task-option"><h4>UpWall</h4><iframe src="https://offerwall.upwall.io/offerwall?appid=YOUR_APP_ID&userid=USER123" width="100%" height="600" frameborder="0"></iframe></div>
  <div class="task-option"><h4>Fyber</h4><iframe src="https://www.fyber.com/offerwall/YOUR_OFFERWALL_ID" width="100%" height="600" frameborder="0"></iframe></div>
</section>

<section id="rewards">
  <h3>Redeem Your Points</h3>
  <div class="reward-option"><h4>bKash</h4><p>Redeem via bKash.</p></div>
  <div class="reward-option"><h4>PayPal</h4><p>Redeem via PayPal.</p></div>
  <div class="reward-option" onclick="showPayeerInput()"><h4>Payeer</h4><p>Redeem via Payeer</p></div>
  <div class="reward-option" id="payeer-input">
    <h4>Enter Payeer ID</h4>
    <input type="text" id="payeer-id" placeholder="Enter Payeer ID" />
    <button onclick="submitPayeer()">Submit</button>
  </div>
</section>

<section id="login">
  <h3>Login</h3>
  <form onsubmit="loginUser(event)">
    <input type="email" id="login-email" placeholder="Email" required />
    <input type="password" id="login-password" placeholder="Password" required />
    <button type="submit">Login</button>
  </form>
</section>

<section id="signup">
  <h3>Signup</h3>
  <form onsubmit="signupUser(event)">
    <input type="text" id="signup-name" placeholder="Full Name" required />
    <input type="email" id="signup-email" placeholder="Email" required />
    <input type="password" id="signup-password" placeholder="Password" required />
    <button type="submit">Signup</button>
  </form>
</section>

  </div>  <footer class="sticky-footer" id="footer">
    <ul>
      <li><a href="#">About Us</a></li>
      <li><a href="#">Contact</a></li>
      <li><a href="#">Privacy Policy</a></li>
      <li><a href="#">Terms of Service</a></li>
    </ul>
  </footer>  <script>
    const firebaseConfig = {
      apiKey: "YOUR_API_KEY",
      authDomain: "YOUR_AUTH_DOMAIN",
      projectId: "YOUR_PROJECT_ID",
      appId: "YOUR_APP_ID"
    };
    firebase.initializeApp(firebaseConfig);
    const auth = firebase.auth();

    function signupUser(event) {
      event.preventDefault();
      const email = document.getElementById("signup-email").value;
      const password = document.getElementById("signup-password").value;
      auth.createUserWithEmailAndPassword(email, password)
        .then(userCredential => {
          alert("Signup successful! You can now log in.");
          showSection('login');
        })
        .catch(error => {
          alert("Signup failed: " + error.message);
        });
    }

    function loginUser(event) {
      event.preventDefault();
      const email = document.getElementById("login-email").value;
      const password = document.getElementById("login-password").value;
      auth.signInWithEmailAndPassword(email, password)
        .then(userCredential => {
          alert("Login successful!");
          showSection('tasks');
        })
        .catch(error => {
          alert("Login failed: " + error.message);
        });
    }

    function toggleSidebar() {
      const sidebar = document.getElementById("sidebar");
      sidebar.classList.toggle("active");
    }
    function showPayeerInput() {
      document.getElementById("payeer-input").style.display = "block";
    }
    function submitPayeer() {
      const id = document.getElementById("payeer-id").value;
      if (id) alert("Payeer ID submitted: " + id);
      else alert("Please enter your Payeer ID.");
    }
    function showSection(id) {
      const sections = document.querySelectorAll("section");
      sections.forEach(section => section.classList.remove("active-section"));
      document.getElementById(id).classList.add("active-section");
      document.getElementById('footer').style.display = (id === 'hero') ? 'block' : 'none';
    }
  </script></body>
</html>
