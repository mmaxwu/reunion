# Pong Game History

Be able to search up who has been playing, who is doing well in pong, and more.

<input type="text" id="searchInput" placeholder="Search..." onkeyup="search_table()">
<table id="recentGames" style="width: 100%;">
  <tr>
    <th>Player 1</th>
    <th>Player 2</th>
    <th>Player 1 Score</th>
    <th>Player 2 Score</th>
    <th>Player 1 Result</th>
    <th>Player 2 Result</th>
    <th>Date Played</th>
  </tr>
  <tbody id="pongList">
  </tbody>
</table>

<script>
  // prepare HTML result container for new output
  const resultContainer = document.getElementById("pongList");
  // prepare URL's to allow easy switch from deployment and localhost
  //const url = "http://127.0.0.1:8086/api/pong"
  const url = "https://pythonalflask.tk/api/pong"
  const read_fetch = url + '/pongList';

  // Load users on page entry
  read_games();

  // Bind search function to search input field
  document.getElementById("searchInput").addEventListener("keyup", function() {
    search_table();
  });

  function search_table() {
    // Declare variables
    var input, filter, table, tr, td, i, j, txtValue;
    input = document.getElementById("searchInput");
    filter = input.value.toUpperCase();
    table = document.getElementById("recentGames");
    tr = table.getElementsByTagName("tr");

    // Loop through all table rows, and hide those that don't match the search query
    let matchesFound = false;
    for (i = 0; i < tr.length; i++) {
      // Search only in the first 6 columns
      for (j = 0; j < 6; j++) {
        td = tr[i].getElementsByTagName("td")[j];
        if (td) {
          txtValue = td.textContent || td.innerText;
          if (txtValue.toUpperCase().indexOf(filter) > -1) {
            tr[i].style.display = "";
            matchesFound = true;
            break;
          } else {
            tr[i].style.display = "none";
          }
        }
      }
    }
  }

  // Display Game history Table, data is fetched from Backend Database
  function read_games() {
    // prepare fetch options
    const read_options = {
      method: 'GET', // *GET, POST, PUT, DELETE, etc.
      mode: 'cors', // no-cors, *cors, same-origin
      cache: 'default', // *default, no-cache, reload, force-cache, only-if-cached
      credentials: 'omit', // include, *same-origin, omit
      headers: {
        'Content-Type': 'application/json'
      },
    };

    // fetch the data from API
    fetch(read_fetch, read_options)
      // response is a RESTful "promise" on any successful fetch
      .then(response => {
        // check for response errors
        if (response.status !== 200) {
          const errorMsg = 'Database read error: ' + response.status;
          console.log(errorMsg);
          const tr = document.createElement("tr");
          const td = document.createElement("td");
          td.innerHTML = errorMsg;
          tr.appendChild(td);
          resultContainer.appendChild(tr);
          return;
        }
        // valid response will have json data
        response.json().then(data => {
          console.log(data);
          data.sort(function(a, b) {
            return new Date(b.gameDatetime) - new Date(a.gameDatetime);
          });
          for (let i = 0; i < data.length; i++) {
            const row = data[i];
            console.log(row);
            add_row(row);
          }
        })
      })
      // catch fetch errors (ie ACCESS to server blocked)
      .catch(err => {
        console.error(err);
        const tr = document.createElement("tr");
        const td = document.createElement("td");
        td.innerHTML = err;
        tr.appendChild(td);
        resultContainer.appendChild(tr);
      });
  }


  function add_row(data) {
    const tr = document.createElement("tr");
    const user1 = document.createElement("td");
    const user2 = document.createElement("td");
    const score1 = document.createElement("td");
    const score2 = document.createElement("td");
    const result1 = document.createElement("td");
    const result2 = document.createElement("td");
    const gameDatetime = document.createElement("td");

  
    // obtain data that is specific to the API
    user1.innerHTML = data.user1; 
    user2.innerHTML = data.user2; 
    score1.innerHTML = data.score1;
    score2.innerHTML = data.score2;
    result1.innerHTML = data.result1;
    result2.innerHTML = data.result2;
    gameDatetime.innerHTML = data.gameDatetime;

    // add HTML to container
    tr.appendChild(user1);
    tr.appendChild(user2);
    tr.appendChild(score1);
    tr.appendChild(score2);
    tr.appendChild(result1);
    tr.appendChild(result2);
    tr.appendChild(gameDatetime);

    resultContainer.appendChild(tr);
  }
</script>

