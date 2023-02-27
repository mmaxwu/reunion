# Game History

<table id="recentGames" style="width: 100%;">
  <tr>
    <th>Black Username</th>
    <th>Black Result</th>
    <th>Red Username</th>
    <th>Red Result</th>
    <th>Date & Time</th>
  </tr>
  <tbody id="checkersList">
  </tbody>
</table>

<script>
 // prepare HTML result container for new output
  const resultContainer = document.getElementById("checkersList");
  // prepare URL's to allow easy switch from deployment and localhost
  //const url = "http://localhost:8086/api/users"
  const url = "https://pythonalflask.tk/api/checkers"
  const read_fetch = url + '/checkersList';

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
          data.sort(function(a, b) {
            return new Date(b.dogame) - new Date(a.dogame);
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
    const uidB = document.createElement("td");
    const resultB = document.createElement("td");
    const uidR = document.createElement("td");
    const resultR = document.createElement("td");
    const dogame = document.createElement("td")
  
    // obtain data that is specific to the API
    uidB.innerHTML = data.uidB; 
    resultB.innerHTML = data.resultB; 
    uidR.innerHTML = data.uidR; 
    resultR.innerHTML = data.resultR; 
    dogame.innerHTML = data.dogame;

    // add HTML to container
    tr.appendChild(uidB);
    tr.appendChild(resultB)
    tr.appendChild(uidR);
    tr.appendChild(resultR)
    tr.appendChild(dogame);

    resultContainer.appendChild(tr);
  }
</script>

