<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Data Table</title>
  <style>
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 20px;
    }

    th, td {
      border: 1px solid #ddd;
      padding: 8px;
      text-align: left;
    }

    th {
      background-color: #f2f2f2;
    }

    .pagination {
      display: flex;
      list-style: none;
      margin-top: 20px;
    }

    .pagination li {
      margin-right: 10px;
      cursor: pointer;
    }
  </style>
</head>
<body>

  <input type="text" id="searchInput" placeholder="Search by name or location">
  <select id="sortOption">
    <option value="date">Sort by Date</option>
    <option value="time">Sort by Time</option>
  </select>

  <table id="dataTable">
    <thead>
      <tr>
        <th>Sno</th>
        <th>Customer Name</th>
        <th>Age</th>
        <th>Phone</th>
        <th>Location</th>
        <th>Date</th>
        <th>Time</th>
      </tr>
    </thead>
    <tbody>
      <!-- Table rows for the first 20 records -->
    </tbody>
  </table>

  <ul class="pagination"></ul>

  <script>
    const dummyData = [
      { sno: 1, name: 'John ', age: 20, phone: '12345678', location: 'City A', created_at: '2024-02-29T11:10:00' },
      // Add 19 more records here
 { sno: 1, name: 'stive', age: 21, phone: '23456789', location: 'City a', created_at: '2024-02-29T09:40:00' },
      // Add 19 more records here
 { sno: 2, name: 'Roshan', age: 22, phone: '34567891', location: 'City b', created_at: '2024-02-29T03:56:00' },
      // Add 19 more records here
 { sno: 3, name: 'Hrithik', age: 23, phone: '45678912', location: 'City c', created_at: '2024-02-29T11:50:00' },
      // Add 19 more records here
 { sno: 4, name: 'ankith', age: 24, phone: '567891234', location: 'City d', created_at: '2024-02-29T02:20:00' },
      // Add 19 more records here
 { sno: 5, name: 'singh', age: 25, phone: '678912345', location: 'City e', created_at: '2024-02-29T09:00:00' },
      // Add 19 more records here
 { sno: 6, name: 'zimmy', age: 26, phone: '789123456', location: 'City f', created_at: '2024-02-29T06:00:00' },
      // Add 19 more records here
 { sno: 7, name: 'gopi', age: 27, phone: '891234567', location: 'City g', created_at: '2024-01-29T04:40:00' },
      // Add 19 more records here
 { sno: 8, name: 'karthi', age: 28, phone: '912345678', location: 'City h', created_at: '2024-02-03T08:00:00' },
      // Add 19 more records here
 { sno: 9, name: 'sammu', age: 29, phone: '938765435', location: 'City i', created_at: '2024-06-05T11:00:00' },
      // Add 19 more records here
 { sno: 10, name: 'asrith', age: 30, phone: '8764675443', location: 'City j', created_at: '2024-07-09T03:30:00' },
      // Add 19 more records here
 { sno: 11, name: 'sirii', age: 31, phone: '7636779578', location: 'City k', created_at: '2024-09-15T04:30:00' },
      // Add 19 more records here
 { sno: 12, name: 'bhavs', age: 32, phone: '8654433567', location: 'City l', created_at: '2024-02-10T05:30:00' },
      // Add 19 more records here
 { sno: 13, name: 'chits', age: 33, phone: '1245684890', location: 'City m', created_at: '2024-08-19T12:30:00' },
      // Add 19 more records here
 { sno: 14, name: 'abhi', age: 34, phone: '2288976557', location: 'City n', created_at: '2024-07-28T01:30:00' },
      // Add 19 more records here
 { sno: 15, name: 'rahul', age: 35, phone: '5676443897', location: 'City o', created_at: '2024-03-25T06:30:00' },
      // Add 19 more records here
 { sno: 16, name: 'giri', age: 36, phone: '4578646790', location: 'City p', created_at: '2024-02-22T07:30:00' },
      // Add 19 more records here
 { sno: 17, name: 'kiran', age: 37, phone: '3456777545', location: 'City q', created_at: '2024-11-19T08:30:00' },
      // Add 19 more records here
 { sno: 18, name: 'rajesh', age: 38, phone: '8757544356', location: 'City r', created_at: '2024-10-11T09:30:00' },
      // Add 19 more records th
 { sno: 19, name: 'teja', age: 39, phone: '4574356644', location: 'City s', created_at: '2024-12-12T11:30:00' },
      // Add 19 more records here
 { sno: 20, name: 'srinu', age: 40, phone: '7685645475', location: 'City t', created_at: '2024-02-13T10:30:00' },
      // Add 19 more records here
    ];

    displayData(dummyData.slice(0, 20));

    function displayData(data) {
      const tableBody = document.querySelector('#dataTable tbody');
      tableBody.innerHTML = '';

      data.forEach(record => {
        const [date, time] = record.created_at.split('T');
        const newRow = `
          <tr>
            <td>${record.sno}</td>
            <td>${record.name}</td>
            <td>${record.age}</td>
            <td>${record.phone}</td>
            <td>${record.location}</td>
            <td>${date}</td>
            <td>${time}</td>
          </tr>
        `;
        tableBody.innerHTML += newRow;
      });
    }

    // Pagination logic
    const itemsPerPage = 20;
    const totalPages = Math.ceil(dummyData.length / itemsPerPage);
    const pagination = document.querySelector('.pagination');

    for (let i = 1; i <= totalPages; i++) {
      const li = document.createElement('li');
      li.textContent = i;
      li.addEventListener('click', () => paginate(i));
      pagination.appendChild(li);
    }

    function paginate(pageNumber) {
      const startIndex = (pageNumber - 1) * itemsPerPage;
      const endIndex = startIndex + itemsPerPage;
      const displayedData = dummyData.slice(startIndex, endIndex);
      displayData(displayedData);
    }
  </script>

</body>
</html>
