<style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #808080;
            margin: 0;
            padding: 0;
            color: #C0C0C0;
        }
        h1, h2 {
            color: #C0C0C0;
            text-align: center;
            margin-top: 20px;
        }
        .card {
            max-width: 90%;
            margin: 20px auto;
            padding: 20px;
            border-radius: 8px;
            background-color: #000000;
            box-shadow: 3 4px 8px rgba(0, 0, 0, 0.1);
        }
        #dataTable, #predictionHistoryTable {
            width: 100%;
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            background-color: #ECA80A;
        }
        table {
            width: 100%;
            border-collapse: collapse;
        }
        th, td {
            padding: 12px;
            text-align: center;
            border-bottom: 1px solid #0AD1F9;
        }
        th {
            background-color: #C0C0C0;
            color: black;
            font-weight: bold;
        }
        td {
            background-color: #000000;
        }
        tr:nth-child(even) td {
            background-color: #808080;
        }
        tr:hover td {
            background-color: #000000;
        }
        #predictionChart {
            width: 100%;
            height: 250px; /* Fixed height */
            border: 2px solid #007bff;
            border-radius: 8px;
            background-color: #000000;
        }
        .pagination {
            display: flex;
            justify-content: center;
            margin-top: 20px;
        }
        .pagination button {
            padding: 10px 20px;
            margin: 0 5px;
            border: none;
            border-radius: 5px;
            background-color: #FFFF33;
            color: black;
            cursor: pointer;
            transition: background-color 0.3s ease, transform 0.2s ease;
        }
        .pagination button:hover {
            background-color: #FF0000;
            transform: scale(1.05);
        }
        .pagination button:disabled {
            background-color: #33FFFF;
            cursor: not-allowed;
        }
        #timeRemaining {
            font-size: 24px;
            font-weight: bold;
            text-align: center;
        }
        #predictedNumber, #predictedPremium {
            font-size: 18px;
            text-align: center;
            margin: 10px 0;
        }
        .button-group {
            display: flex;
            justify-content: center;
            margin: 20px 0;
        }
        .button-group a {
            padding: 10px 20px;
            margin: 0 10px;
            border-radius: 5px;
            cursor: pointer;
            text-decoration: none; /* Remove underline */
            color: white; /* Text color */
            display: inline-block; /* Make anchor behave like a button */
            transition: background-color 0.3s ease, transform 0.2s ease;
        }
        #registerButton {
            background-color: #007bff; /* Blue for Register */
        }
        #telegramButton {
            background-color: #dc3545; /* Red for Telegram */
        }
        .button-group a:hover {
            transform: scale(1.05);
        }
        @media (max-width: 768px) {
            .card {
                padding: 15px;
            }
            th, td {
                padding: 8px;
                font-size: 14px;
            }
            #timeRemaining {
                font-size: 20px;
            }
            #predictedNumber, #predictedPremium {
                font-size: 16px;
            }
            #predictionChart {
                height: 200px; /* Adjusted height for mobile */
            }
        }
        @media (max-width: 480px) {
            th, td {
                font-size: 12px;
            }
            #timeRemaining {
                font-size: 18px;
            }
            #predictedNumber, #predictedPremium {
                font-size: 14px;
            }
            #predictionChart {
                height: 180px; /* Further adjustment for very small screens */
            }
        }
    </style>
</head>
<body>
    <h1>RIOCHEATS VIP </h1>
    <div class="card">
        <h2>RIOCHEATS VIP SERVER</h2>
        <div class="card">
        <p id="predictedNumber">Prediction :--</p>
        <p id="predictedPremium">Enjoy: --</p>
        <h2>GAME TIMING 1MIN</h2>
        <p id="timeRemaining">--:--</p
<script>
document.addEventListener('DOMContentLoaded', function() {
    const tableBody = document.querySelector('#dataTable tbody');
    const predictedNumberElement = document.getElementById('predictedNumber');
    const predictedPremiumElement = document.getElementById('predictedPremium');
    const timerElement = document.getElementById('timeRemaining');
    const historyTableBody = document.querySelector('#predictionHistoryTable tbody');
    const prevPageButton = document.getElementById('prevPage');
    const nextPageButton = document.getElementById('nextPage');
    let predictionHistory = JSON.parse(localStorage.getItem('predictionHistory')) || [];
    let lastPrediction = JSON.parse(localStorage.getItem('lastPrediction'));
    let currentPrediction = JSON.parse(localStorage.getItem('currentPrediction'));
    let currentPage = 0;
    const itemsPerPage = 10;
    let timerInterval;

    const fetchNoAverageEmerdList = () => {
        const requestData = {
            pageSize: 10,
            pageNo: 1,
            typeId: 1,
            language: 0,
            random: "ded40537a2ce416e96c00e5218f6859a",
            signature: "69306982EEEB19FA940D72EC93C62552",
            timestamp: Math.floor(Date.now() / 1000)
        };

        return fetch('https://api.bdg88zf.com/api/webapi/GetNoaverageEmerdList', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json;charset=UTF-8',
                'Accept': 'application/json, text/plain, */*'
            },
            body: JSON.stringify(requestData)
        })
        .then(response => response.json())
        .catch(error => console.error('Error fetching no average EMERD list data:', error));
    };

    const fetchGameIssue = () => {
        const requestData = {
            typeId: 1,
            language: 0,
            random: "f8dcb5c527814db68800e3946a2b60e8",
            signature: "08CF7FF3339ED58D4743F4B650FCBEA9",
            timestamp: Math.floor(Date.now() / 1000)
        };

        return fetch('https://api.bdg88zf.com/api/webapi/GetGameIssue', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json;charset=UTF-8',
                'Accept': 'application/json, text/plain, */*'
            },
            body: JSON.stringify(requestData)
        })
        .then(response => response.json())
        .catch(error => console.error('Error fetching game issue:', error));
    };

    const categorizeNumber = (number) => {
        if (number >= 0 && number <= 4) return 'SMALL';
        if (number >= 5 && number <= 9) return 'BIG';
        return 'Unknown';
    };

    const generateRandomPrediction = () => {
        const randomNumber = Math.floor(Math.random() * 10);
        const randomCategory = categorizeNumber(randomNumber);
        return { number: randomNumber, category: randomCategory };
    };

    const updateDataAndPrediction = () => {
        fetchNoAverageEmerdList()
            .then(data => {
                const list = data.data.list;
                tableBody.innerHTML = '';
                list.forEach(item => {
                    const numberCategory = categorizeNumber(Number(item.number));
                    const row = document.createElement('tr');
                    row.innerHTML = `
                        <td>${item.issueNumber}</td>
                        <td>${item.number} (${numberCategory})</td>
                        <td>${item.colour}</td>
                        <td>${item.premium}</td>
                    `;
                    tableBody.appendChild(row);
                });

                const latestIssue = list[0].issueNumber;
                const latestActual = Number(list[0].number);
                const actualCategory = categorizeNumber(latestActual);

                if (!lastPrediction || lastPrediction.issueNumber !== latestIssue) {
                    if (lastPrediction) {
                        const result = (lastPrediction.category === actualCategory) ? 'WIN' : 'LOSS';
                        predictionHistory.unshift({
                            issueNumber: latestIssue,
                            predictedNumber: lastPrediction.number,
                            actualNumber: latestActual,
                            result: result
                        });
                        localStorage.setItem('predictionHistory', JSON.stringify(predictionHistory));
                    }

                    currentPrediction = generateRandomPrediction();
                    currentPrediction.issueNumber = latestIssue;
                    localStorage.setItem('currentPrediction', JSON.stringify(currentPrediction));
                }

                predictedNumberElement.textContent = `PREDICTION : ${currentPrediction.number} (${currentPrediction.category})`;
                predictedPremiumElement.textContent = `RIO VIP`;

                lastPrediction = {
                    issueNumber: latestIssue,
                    number: currentPrediction.number,
                    category: currentPrediction.category
                };
                localStorage.setItem('lastPrediction', JSON.stringify(lastPrediction));

                updatePredictionHistoryTable();
            })
            .catch(error => console.error('Error updating data and prediction:', error));
    };

    const updatePredictionHistoryTable = () => {
        historyTableBody.innerHTML = '';

        const start = currentPage * itemsPerPage;
        const end = start + itemsPerPage;
        const paginatedHistory = predictionHistory.slice(start, end);

        paginatedHistory.forEach(entry => {
            const row = document.createElement('tr');
            row.innerHTML = `
                <td>${entry.issueNumber}</td>
                <td>${entry.predictedNumber}</td>
                <td>${entry.actualNumber}</td>
                <td>${entry.result}</td>
            `;
            historyTableBody.appendChild(row);
        });

        prevPageButton.disabled = currentPage === 0;
        nextPageButton.disabled = end >= predictionHistory.length;
    };

    const updateTimer = () => {
        fetchGameIssue()
            .then(data => {
                const { endTime } = data.data;
                const endDate = new Date(endTime);
                const now = new Date();
                const remainingTimeMs = endDate - now;

                if (remainingTimeMs <= 0) {
                    timerElement.textContent = "Time Remaining: 00:00:00";
                    clearInterval(timerInterval);
                    updateDataAndPrediction();
                    updateTimer();
                } else {
                    const hours = String(Math.floor(remainingTimeMs / (1000 * 60 * 60))).padStart(2, '0');
                    const minutes = String(Math.floor((remainingTimeMs % (1000 * 60 * 60)) / (1000 * 60))).padStart(2, '0');
                    const seconds = String(Math.floor((remainingTimeMs % (1000 * 60)) / 1000)).padStart(2, '0');
                    timerElement.textContent = `TIME IS RUNNING : ${hours}:${minutes}:${seconds}`;
                }
            })
            .catch(error => console.error('Error fetching game issue for timer:', error));
    };

    // Pagination controls
    prevPageButton.addEventListener('click', () => {
        if (currentPage > 0) {
            currentPage--;
            updatePredictionHistoryTable();
        }
    });

    nextPageButton.addEventListener('click', () => {
        if ((currentPage + 1) * itemsPerPage < predictionHistory.length) {
            currentPage++;
            updatePredictionHistoryTable();
        }
    });

    // Initialize data and start the timer
    updateDataAndPrediction();
    updateTimer();
    timerInterval = setInterval(() => {
        updateTimer();
        updateDataAndPrediction();
    }, 1000); // Update every 10 seconds

    // Load initial prediction history table
    updatePredictionHistoryTable();
});
</script>

  
</div></body></html>
