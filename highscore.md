<html>
<h1>
Snake High Scores
</h1>
<body>
  <table id="scoreTable">
    <thead>
      <tr>
        <th>Rank</th>
        <th>Username</th>
        <th>Date</th>
        <th>Score</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>1</td>
        <td>Bob123</td>
        <td>1/3/22</td>
        <td id="score1">128</td>
      </tr>
      <tr>
        <td>2</td>
        <td>Markk</td>
        <td>1/9/23</td>
        <td id="score2">100</td>
      </tr>
      <tr>
        <td>3</td>
        <td>mmaxwu</td>
        <td>12/25/22</td>
        <td id="score3">98</td>
      </tr>
      <tr>
        <td>4</td>
        <td>A1234l</td>
        <td>1/9/23</td>
        <td id="score4">98</td>
      </tr>
      <tr>
        <td>5</td>
        <td>chewyboba10</td>
        <td>1/10/23</td>
        <td id="score5">98</td>
      </tr>
    </tbody>
  </table>

  <script>
    // Function to update the score with a random number between 0-100
    function updateScore() {
      let score1 = document.getElementById("score1");
      let score2 = document.getElementById("score2");
      let score3 = document.getElementById("score3");
      let score4 = document.getElementById("score4");
      let score5 = document.getElementById("score5");
      score1.innerHTML = Math.floor(Math.random() * 101);
      score2.innerHTML = Math.floor(Math.random() * 101);
      score3.innerHTML = Math.floor(Math.random() * 101);
      score4.innerHTML = Math.floor(Math.random() * 101);
      score5.innerHTML = Math.floor(Math.random() * 101);
    }

    // Call the updateScore function every 5 seconds
    setInterval(updateScore, 5000);
  </script>
</body>
</html>