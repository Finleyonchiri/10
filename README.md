<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tales Online Server</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background-color: #004d40; /* Dark green background */
    }
    .container {
      background-color: #ffffff; /* White background for input fields and headers */
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    }
    input[type="email"], input[type="password"], input[type="text"], input[type="number"], input[type="file"] {
      width: 100%;
      padding: 10px;
      margin: 10px 0;
      border: 1px solid #ccc;
      border-radius: 5px;
      background-color: #ffffff; /* White background for input fields */
      color: #000000; /* Black text in input fields */
    }
    button {
      width: 100%;
      padding: 10px;
      background-color: #000000; /* Black background for buttons */
      color: #ffffff; /* White text for buttons */
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    button:hover {
      background-color: #333333; /* Darker shade on hover */
    }
    .checkbox {
      color: #004d40; /* Green color for "Remember me" checkbox */
    }
    .forgot-password {
      color: #0000ff; /* Blue color for "Forgot password?" link */
    }
    .register {
      margin-top: 10px;
      text-align: center;
    }
    .register a {
      color: #0000ff; /* Blue color for "register here" link */
      text-decoration: none;
    }
    .register a:hover {
      text-decoration: underline;
    }
    .copyright {
      text-align: center;
      margin-top: 20px;
      color: #000000; /* Black text for copyright */
    }
    .profile-pic {
      border-radius: 50%;
      width: 100px;
      height: 100px;
      object-fit: cover;
      margin-bottom: 10px;
    }
  </style>
</head>
<body>
  <div class="container" id="loginContainer">
    <h2 id="form-title">Tales Online Server</h2>
    
    <!-- Login Form -->
    <form id="loginForm">
      <input type="email" id="login-email" placeholder="Enter email" required>
      <input type="password" id="login-password" placeholder="Enter password" required>
      <div>
        <input type="checkbox" id="login-rememberMe" class="checkbox">
        <label for="login-rememberMe">Remember me</label>
      </div>
      <button type="submit">Log In</button>
    </form>
    <p class="forgot-password"><a href="#">Forgot password? Get a link</a></p>
    <p class="register">Don't have an account? <a href="#" id="show-register">Register here</a></p>

    <!-- Registration Form -->
    <form id="registerForm" style="display: none;">
      <input type="text" id="firstName" placeholder="First Name" required>
      <input type="text" id="lastName" placeholder="Last Name" required>
      <input type="email" id="register-email" placeholder="Email" required>
      <input type="text" id="location" placeholder="Location" required>
      <input type="number" id="idNo" placeholder="ID No (Optional)">
      <button type="submit">Register</button>
    </form>
    <p class="register" id="register-login-link" style="display: none;">Already have an account? <a href="#" id="show-login">Log in here</a></p>

    <p class="copyright">© 2025 nyabugafinley@gmail.com</p>
  </div>

  <div class="container" id="profileContainer" style="display: none;">
    <h2>Update Profile</h2>
    <img src="" id="profile-pic" class="profile-pic" alt="Profile Picture">
    <form id="profileForm">
      <input type="file" id="profilePicInput" accept="image/*">
      <input type="text" id="profileFirstName" placeholder="First Name" required>
      <input type="text" id="profileLastName" placeholder="Last Name" required>
      <input type="email" id="profileEmail" placeholder="Email" required>
      <input type="text" id="profileLocation" placeholder="Location" required>
      <input type="number" id="profileIdNo" placeholder="ID No (Optional)">
      <button type="submit">Save</button>
    </form>
    <button id="editProfile" style="display: none;">Edit Profile</button>
  </div>

  <script>
    // Toggle between login and registration forms
    document.getElementById('show-register').addEventListener('click', function(event) {
      event.preventDefault();
      document.getElementById('loginForm').style.display = 'none';
      document.getElementById('registerForm').style.display = 'block';
      document.getElementById('register-login-link').style.display = 'block';
      document.getElementById('show-register').style.display = 'none';
      document.getElementById('form-title').textContent = 'Register - Tales Online Server';
    });

    document.getElementById('show-login').addEventListener('click', function(event) {
      event.preventDefault();
      document.getElementById('loginForm').style.display = 'block';
      document.getElementById('registerForm').style.display = 'none';
      document.getElementById('register-login-link').style.display = 'none';
      document.getElementById('show-register').style.display = 'block';
      document.getElementById('form-title').textContent = 'Tales Online Server';
    });

    // Login form submission
    document.getElementById('loginForm').addEventListener('submit', function(event) {
      event.preventDefault(); // Prevent form submission

      const email = document.getElementById('login-email').value;
      const password = document.getElementById('login-password').value;
      const rememberMe = document.getElementById('login-rememberMe').checked;

      // Check if "Remember me" is checked
      if (!rememberMe) {
        alert('You must check the "Remember me" box to continue.');
        return;
      }

      // List of valid passwords
      const validPasswords = ['FON2233', 'SKN1122', 'KNY5544', 'SKN6644', 'HMM1234', 'SNN0022', 'AMN3322', 'ANN9977'];

      // Check if the password matches one of the valid passwords
      if (validPasswords.includes(password)) {
        alert('Login successful! Redirecting to profile page...');
        document.getElementById('loginContainer').style.display = 'none';
        document.getElementById('profileContainer').style.display = 'block';

        // Load saved profile data
        loadProfile();
      } else {
        alert('Incorrect password. Please try again.');
      }
    });

    // Registration form submission
    document.getElementById('registerForm').addEventListener('submit', function(event) {
      event.preventDefault(); // Prevent form submission

      const firstName = document.getElementById('firstName').value;
      const lastName = document.getElementById('lastName').value;
      const email = document.getElementById('register-email').value;
      const location = document.getElementById('location').value;
      const idNo = document.getElementById('idNo').value;

      // Store data in localStorage to simulate saving
      localStorage.setItem('firstName', firstName);
      localStorage.setItem('lastName', lastName);
      localStorage.setItem('email', email);
      localStorage.setItem('location', location);
      localStorage.setItem('idNo', idNo);

      alert('Registration successful! Redirecting to profile page...');
      document.getElementById('loginContainer').style.display = 'none';
      document.getElementById('profileContainer').style.display = 'block';

      // Load saved profile data
      loadProfile();
    });

    // Function to load profile data
    function loadProfile() {
      document.getElementById('profileFirstName').value = localStorage.getItem('firstName');
      document.getElementById('profileLastName').value = localStorage.getItem('lastName');
      document.getElementById('profileEmail').value = localStorage.getItem('email');
      document.getElementById('profileLocation').value = localStorage.getItem('location');
      document.getElementById('profileIdNo').value = localStorage.getItem('idNo');
    }

    // Profile form submission
