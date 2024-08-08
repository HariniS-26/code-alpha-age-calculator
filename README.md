<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Age Calculator</title>
    <style>
        html, body {
            height: 100%;
            margin: 0;
            padding: 0;
            font-family: Arial, sans-serif;
            background-color: pink; /* Light background color for the entire page */
        }
        body {
            display: flex;
            justify-content: center;
            align-items: center;
        }
        .container {
            max-width: 1000px;
            padding: 100px;
            border: 1px solid #ccc;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            background-color: #ffffff; /* White background color for the container */
        }
        .form-group {
            margin-bottom: 15px;
        }
        .form-group label {
            display: block;
            margin-bottom: 5px;
        }
        .form-group input {
            width: 100%;
            padding: 15px;
            box-sizing: border-box;
        }
        .form-group button {
            padding: 10px 30px;
            background-color: #007bff;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .form-group button:hover {
            background-color: #0056b3;
        }
        .result {
            margin-top: 20px;
            font-size: 1.2em;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Age Calculator</h1>
        <div class="form-group">
            <label for="dobDay">Day:</label>
            <input type="number" id="dobDay" min="1" max="31" placeholder="Enter day">
        </div>
        <div class="form-group">
            <label for="dobMonth">Month:</label>
            <input type="number" id="dobMonth" min="1" max="12" placeholder="Enter month">
        </div>
        <div class="form-group">
            <label for="dobYear">Year:</label>
            <input type="number" id="dobYear" placeholder="Enter year">
        </div>
        <div class="form-group">
            <button onclick="calculateAge()">Calculate Age</button>
        </div>
        <div class="result" id="result"></div>
    </div>

    <script>
        function calculateAge() {
            // Get input values
            const day = parseInt(document.getElementById('dobDay').value);
            const month = parseInt(document.getElementById('dobMonth').value) - 1; // Months are 0-based in JavaScript
            const year = parseInt(document.getElementById('dobYear').value);

            if (isNaN(day) || isNaN(month) || isNaN(year)) {
                document.getElementById('result').innerText = 'Please enter valid date values.';
                return;
            }

            const today = new Date();
            const dob = new Date(year, month, day);

            // Check if the date is valid
            if (dob > today || dob.getDate() !== day || dob.getMonth() !== month || dob.getFullYear() !== year) {
                document.getElementById('result').innerText = 'Invalid date. Please check the values.';
                return;
            }

            // Calculate the time difference in milliseconds
            const timeDiff = today - dob;

            // Convert time difference into age components
            const ageDate = new Date(timeDiff);

            const years = ageDate.getUTCFullYear() - 1970;
            const totalMonths = years * 12 + ageDate.getUTCMonth();
            const months = totalMonths % 12;
            const days = Math.floor(timeDiff / (1000 * 60 * 60 * 24)) % 30; // Approximate days in month
            const hours = Math.floor(timeDiff / (1000 * 60 * 60)) % 24;
            const minutes = Math.floor(timeDiff / (1000 * 60)) % 60;
            const seconds = Math.floor(timeDiff / 1000) % 60;

            document.getElementById('result').innerText = `You are ${years} years, ${months} months, ${days} days, ${hours} hours, ${minutes} minutes, and ${seconds} seconds old.`;
        }
    </script>
</body>
</html>
