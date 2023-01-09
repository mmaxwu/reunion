# Wildlife Tracking

<table>
  <tr>
    <th>National Park</th>
    <th>Wildlife</th>
    <th>Number</th>
  </tr>
  <tr>
    <td>Yosemite</td>
    <td>Black bears</td>
    <td id="yosemite-bears">0</td>
  </tr>
  <tr>
    <td>Joshua Tree</td>
    <td>Desert bighorn sheep</td>
    <td id="joshua-sheep">0</td>
  </tr>
  <tr>
    <td>Point Reyes</td>
    <td>Seals</td>
    <td id="point-reyes-seals">0</td>
  </tr>
</table>

<script>
  function updateWildlifeCount() {
    // Retrieve updated wildlife count data
    const yosemiteBears = retrieveUpdatedCount('yosemite-bears');
    const joshuaSheep = retrieveUpdatedCount('joshua-sheep');
    const pointReyesSeals = retrieveUpdatedCount('point-reyes-seals');

    // Update the table with the new counts
    document.getElementById('yosemite-bears').innerHTML = yosemiteBears;
    document.getElementById('joshua-sheep').innerHTML = joshuaSheep;
    document.getElementById('point-reyes-seals').innerHTML = pointReyesSeals;
  }

  // This function would be responsible for retrieving updated wildlife count data
  function retrieveUpdatedCount(id) {
    // Return placeholder data for now
    return Math.floor(Math.random() * 100);
  }

  // Update the wildlife counts every 5 seconds
  setInterval(updateWildlifeCount, 5000);
</script>
