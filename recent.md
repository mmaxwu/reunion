<div class="container">
<h2>Recent Scores</h2>

<h2>snake</h2>
<p>5 most recent results for the snake game!</p>

<ul id="recentGames"></ul>

<h2>hangman</h2>

</div>

<script>
const getScores = () => JSON.parse(localStorage.getItem("recentScores")) || []
const recentGames = document.getElementById("recentGames");
getScores().slice(-5).reverse().forEach((s) => {
    const scoreElement = document.createElement("li")

    const padL = (nr, len = 2, chr = `0`) => `${nr}`.padStart(2, chr);
    const dt = new Date(s.date)
    const str = `${padL(dt.getMonth()+1)}/${padL(dt.getDate())}/${dt.getFullYear()} ${padL(dt.getHours())}:${padL(dt.getMinutes())}:${padL(dt.getSeconds())}`

    scoreElement.innerHTML = `${str} - <b>${s.username}</b>: ${s.score}`
    recentGames.appendChild(scoreElement)
})
</script>