<html>
<head>
  <title>Login Page</title>
</head>
<body>
  <h1>Login Page</h1>
  <form action="">
    <label for="username">Username:</label>
    <input type="text" id="username" name="username"><br><br>
    <label for="password">Password:</label>
    <input type="password" id="password" name="password"><br><br>
    <input type="submit" value="Submit">
  </form>

  <script>
    const form = document.querySelector("form");
    form.addEventListener("submit", function(event) {
      event.preventDefault();
      const username = document.querySelector("#username").value;
      const password = document.querySelector("#password").value;

      // Here is the code to check if the login is successful
      if (username === "admin" && password === "password") {
        // Redirect to the index page if the login is successful
        window.location.href = "index.html";
      } else {
        alert("Invalid username or password. Please try again.");
      }
    });
  </script>
</body>
</html>
