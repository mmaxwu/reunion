# Login Page

<form id="signup-form">
  <label for="username">Username:</label>
  <input type="text" id="signup-username" required>

  <label for="password">Password:</label>
  <input type="password" id="signup-password" required>

  <input type="submit" value="Sign Up">
</form>

<form id="login-form">
  <label for="username">Username:</label>
  <input type="text" id="login-username" required>

  <label for="password">Password:</label>
  <input type="password" id="login-password" required>

  <input type="submit" value="Login">
</form>

<script>
const signupForm = document.getElementById("signup-form");
const loginForm = document.getElementById("login-form");
const signupUsername = document.getElementById("signup-username");
const signupPassword = document.getElementById("signup-password");
const loginUsername = document.getElementById("login-username");
const loginPassword = document.getElementById("login-password");

let username = "";
let password = "";

signupForm.addEventListener("submit", function(event) {
  event.preventDefault();
  username = signupUsername.value;
  password = signupPassword.value;
});

loginForm.addEventListener("submit", function(event) {
  event.preventDefault();
  if (username === loginUsername.value && password === loginPassword.value) {
    window.location.href = "Home.html";
  } else {
    alert("Incorrect username or password.");
  }
});
</script>