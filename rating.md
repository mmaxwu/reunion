<h2>Recent Rating</h2>

<h2>Snake</h2>
<p>A list of the recent ratings for snake!</p>

<!-- <body> -->
<table>
  <thead>
  <tr>
    <th>Username</th>
    <th>Rating</th>
    <th>Comment</th>
  </tr>
  </thead>
  <tbody id="dataTable">

  </tbody>
</table>

<script>
  // prepare HTML result container for new output
  const addTable = document.getElementById("dataTable");
  // prepare URL's to allow easy switch from deployment and localhost
  //const url = "http://localhost:8086/api/users"
  const url = "https://pythonalflask.tk/api/rating"
  const fetchCreate = url + '/createRating';
  const fetchRead = url + '/ratingList';
  // Load users on page entry
  read();
  // Display User Table, data is fetched from Backend Database
  function read() {
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
    fetch(fetchRead, read_options)
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
            addTable.appendChild(tr);
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
      addTable.appendChild(tr);
    });
  }
// create function moved to snake game
  // function create_user(){
  //   //Validate Password (must be 6-20 characters in len)
  //   //verifyPassword("click");
  //   const body = {
  //       username: document.getElementById("user").value,
  //       score: document.getElementById("score_value").value
  //   };
  //   const requestOptions = {
  //       method: 'POST',
  //       body: JSON.stringify(body),
  //       headers: {
  //           "content-type": "application/json",
  //           'Authorization': 'Bearer my-token',
  //       },
  //   };
  //   // URL for Create API
  //   // Fetch API call to the database to create a new user
  //   fetch(fetchCreate, requestOptions)
  //     .then(response => {
  //       // trap error response from Web API
  //       if (response.status !== 200) {
  //         const errorMsg = 'Database create error: ' + response.status;
  //         console.log(errorMsg);
  //         const tr = document.createElement("tr");
  //         const td = document.createElement("td");
  //         td.innerHTML = errorMsg;
  //         tr.appendChild(td);
  //         addTable.appendChild(tr);
  //         return;
  //       }
  //       // response contains valid result
  //       response.json().then(data => {
  //           console.log(data);
  //           //add a table row for the new/created userid
  //           add_row(data);
  //       })
  //   })
  // }
  function add_row(data) {
    const tr = document.createElement("tr");
    const username = document.createElement("td");
    const rating = document.createElement("td");
    const comment = document.createElement("td");
    // obtain data that is specific to the API
    username.innerHTML = data.username; 
    rating.innerHTML = data.rating; 
    comment.innerHTML = data.comment;
    tos.innerHTML = data.tos; 
    // add HTML to container
    tr.appendChild(username);
    tr.appendChild(rating);
    tr.appendChild(comment);
    addTable.appendChild(tr);
  }
// const getScores = () => JSON.parse(localStorage.getItem("recentScores")) || []
// const recentGames = document.getElementById("recentGames");
// getScores().slice(-5).reverse().forEach((s) => {
//     const scoreElement = document.createElement("li")
//     const padL = (nr, len = 2, chr = `0`) => `${nr}`.padStart(2, chr);
//     const dt = new Date(s.date)
//     const str = `${padL(dt.getMonth()+1)}/${padL(dt.getDate())}/${dt.getFullYear()} ${padL(dt.getHours())}:${padL(dt.getMinutes())}:${padL(dt.getSeconds())}`
//     scoreElement.innerHTML = `${str} - <b>${s.username}</b>: ${s.score}`
//     recentGames.appendChild(scoreElement)
// })
</script>