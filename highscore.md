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
        <td>BOB</td>
        <td>1/3/22</td>
        <td id="score1">128</td>
      </tr>
      <tr>
        <td>2</td>
        <td>ADD</td>
        <td>1/9/23</td>
        <td id="score2">100</td>
      </tr>
      <tr>
        <td>3</td>
        <td>MAX</td>
        <td>12/25/22</td>
        <td id="score3">98</td>
      </tr>
      <tr>
        <td>4</td>
        <td>ALA</td>
        <td>1/9/23</td>
        <td id="score4">98</td>
      </tr>
      <tr>
        <td>5</td>
        <td>EVA</td>
        <td>1/10/23</td>
        <td id="score5">98</td>
      </tr>
    </tbody>
  </table>
  <table>
    <thead>
    <tr>
      <th>User ID</th>
      <th>Score</th>
      <th>Date of Score</th>
    </tr>
    </thead>
    <tbody id="result">
      <!-- javascript generated data -->
    </tbody>
  </table>

  
  <script>
      // prepare HTML result container for new output
  const resultContainer = document.getElementById("result");
  // prepare URL's to allow easy switch from deployment and localhost
  //const url needed
  const url = "http://172.28.227.245:8086/api/score"
  const create_fetch = url + '/addScore';
  const read_fetch = url + '/scoresList';

  // Load users on page entry
// Load users on page entry
  read_users();


  // Display User Table, data is fetched from Backend Database
  function read_users() {
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
            for (let row in data) {
              console.log(data[row]);
              add_row(data[row]);
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
  

    // obtain data that is specific to the API 
    username.innerHTML = data.username; 
    score.innerHTML = data.score;
    dos.innerHTML = data.dos; 


    // add HTML to container
    tr.appendChild(username);
    tr.appendChild(score);
    tr.appendChild(dos);

    resultContainer.appendChild(tr);
  }
  </script>
</body>
</html>