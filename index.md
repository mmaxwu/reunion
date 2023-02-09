## Welcome!
Welcome to our website! 

## Mini Arcade
Welcome to our website where we host multiple retro mini games with a leader board! 
## Snake Leaderboard
> This table displays the top 5 current leaders in the maximum score for Snake

<table id="recentGames" style="width: 100%;">
  <tr>
    <th>Date & Time</th>
    <th>Username</th>
    <th>Score</th>
  </tr>
  <tbody id="scoreList">
  </tbody>
</table>

<script>
const getScores = () => JSON.parse(localStorage.getItem("recentScores")) || []
const scoreList = document.getElementById("scoreList");
getScores().slice(-5).sort((a, b) => b.score - a.score).forEach((s) => {
    const scoreElement = document.createElement("tr")

    const padL = (nr, len = 2, chr = `0`) => `${nr}`.padStart(2, chr);
    const dt = new Date(s.date)
    const str = `${padL(dt.getMonth()+1)}/${padL(dt.getDate())}/${dt.getFullYear()} ${padL(dt.getHours())}:${padL(dt.getMinutes())}:${padL(dt.getSeconds())}`

    scoreElement.innerHTML = `<td>${str}</td><td><b>${s.username}</b></td><td>${s.score}</td>`
    scoreList.appendChild(scoreElement)
})
</script>