<!DOCTYPE html>
<html>
<head>
    <title>Plant Water Reminder</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #e8f5e9;
            text-align: center;
            padding: 30px;
        }

        h1 {
            color: green;
        }

        .container {
            background: white;
            padding: 20px;
            width: 350px;
            margin: auto;
            border-radius: 10px;
            box-shadow: 0 0 10px gray;
        }

        input, button {
            padding: 10px;
            margin: 10px;
            width: 90%;
        }

        button {
            background-color: green;
            color: white;
            border: none;
            cursor: pointer;
        }

        button:hover {
            background-color: darkgreen;
        }

        .plant-list {
            margin-top: 20px;
            text-align: left;
        }

        .plant-item {
            background: #f1f8e9;
            padding: 10px;
            margin: 5px 0;
            border-radius: 5px;
        }
    </style>
</head>
<body>

    <h1>🌱 Plant Water Reminder</h1>

    <div class="container">
        <input type="text" id="plantName" placeholder="Enter Plant Name">
        <input type="number" id="days" placeholder="Water Every (Days)">
        <button onclick="addPlant()">Add Plant</button>

        <div class="plant-list" id="plantList"></div>
    </div>

    <script>
        let plants = [];

        function addPlant() {
            let name = document.getElementById("plantName").value;
            let days = document.getElementById("days").value;

            if (name === "" || days === "") {
                alert("Please fill all fields");
                return;
            }

            let nextWaterDate = new Date();
            nextWaterDate.setDate(nextWaterDate.getDate() + parseInt(days));

            plants.push({
                name: name,
                days: days,
                nextWater: nextWaterDate
            });

            displayPlants();
            document.getElementById("plantName").value = "";
            document.getElementById("days").value = "";
        }

        function displayPlants() {
            let list = document.getElementById("plantList");
            list.innerHTML = "";

            plants.forEach((plant, index) => {
                let today = new Date();
                let reminder = "";

                if (today >= plant.nextWater) {
                    reminder = "⚠️ Time to Water!";
                } else {
                    reminder = "Next Watering: " + plant.nextWater.toDateString();
                }

                list.innerHTML += `
                    <div class="plant-item">
                        <strong>${plant.name}</strong><br>
                        ${reminder}
                    </div>
                `;
            });
        }
    </script>

</body>
</html>
