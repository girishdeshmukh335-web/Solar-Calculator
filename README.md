# Solar-Calculator
<!DOCTYPE html>
<html lang="mr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>EcoGrid Solar Calculator - Smart Rooftop Solar Planner</title>
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-color: #2e7d32;
            --secondary-color: #4caf50;
            --bg-color: #f4f6f8;
            --text-color: #333333;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Poppins', sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-color);
            line-height: 1.6;
        }

        header {
            background: linear-gradient(rgba(0, 0, 0, 0.6), rgba(0, 0, 0, 0.6)), url('https://images.unsplash.com/photo-1509391365370-d86413179216?auto=format&fit=crop&w=1920&q=80') no-repeat center center/cover;
            color: white;
            text-align: center;
            padding: 80px 20px;
        }

        header h1 {
            font-size: 2.2rem;
            margin-bottom: 10px;
            color: #ffffff;
        }

        header p {
            font-size: 1.1rem;
            max-width: 600px;
            margin: 0 auto;
            color: #e0e0e0;
        }

        .container {
            max-width: 800px;
            margin: -30px auto 40px auto;
            background: white;
            padding: 30px;
            border-radius: 12px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            position: relative;
        }

        .form-group {
            margin-bottom: 20px;
        }

        label {
            display: block;
            font-weight: 500;
            margin-bottom: 8px;
            color: #444;
        }

        input, select {
            width: 100%;
            padding: 12px 15px;
            border: 1px solid #ccc;
            border-radius: 8px;
            font-size: 1rem;
            outline: none;
            transition: border-color 0.3s;
        }

        input:focus, select:focus {
            border-color: var(--primary-color);
        }

        button {
            background-color: var(--primary-color);
            color: white;
            border: none;
            padding: 14px 20px;
            width: 100%;
            font-size: 1.1rem;
            font-weight: 600;
            border-radius: 8px;
            cursor: pointer;
            transition: background 0.3s;
            margin-top: 10px;
        }

        button:hover {
            background-color: #1b5e20;
        }

        .result-box {
            margin-top: 30px;
            padding: 20px;
            background: #e8f5e9;
            border-left: 6px solid var(--primary-color);
            border-radius: 8px;
            display: none;
        }

        .result-box h3 {
            color: var(--primary-color);
            margin-bottom: 15px;
        }

        .result-item {
            margin-bottom: 10px;
            font-size: 1rem;
        }

        .result-item span {
            font-weight: 600;
            color: #1b5e20;
        }

        footer {
            text-align: center;
            padding: 20px;
            background: #263238;
            color: white;
            margin-top: 40px;
            font-size: 0.9rem;
        }
    </style>
</head>
<body>

    <header>
        <h1>EcoGrid Solar Calculator</h1>
        <p>तुमच्या घरासाठी किती किलोवॅट सोलर पॉवरची गरज आहे आणि बिलात किती बचत होईल हे तपासा!</p>
    </header>

    <div class="container">
        <form id="solarForm">
            <div class="form-group">
                <label for="bill">महिन्याचे सरासरी वीज बिल (₹ मध्ये):</label>
                <input type="number" id="bill" required placeholder="उदा. 2000">
            </div>

            <div class="form-group">
                <label for="area">उपलब्ध छताचे क्षेत्रफळ (चौकोनी फूट / Sq. Ft.):</label>
                <input type="number" id="area" required placeholder="उदा. 300">
            </div>

            <div class="form-group">
                <label for="locationType">क्षेत्राचा प्रकार:</label>
                <select id="locationType">
                    <option value="urban">शहरी भाग (Urban)</option>
                    <option value="rural">ग्रामीण भाग (Rural)</option>
                </select>
            </div>

            <button type="button" onclick="calculateSolar()">कॅल्क्युलेट करा (Calculate)</button>
        </form>

        <div class="result-box" id="resultBox">
            <h3>सोलर अंदाज (Estimation Results):</h3>
            <div class="result-item">शिफारस केलेली क्षमता (Recommended Capacity): <span id="resCapacity"></span> kW</div>
            <div class="result-item">अंदाजे मासिक वीज निर्मिती (Monthly Generation): <span id="resGeneration"></span> युनिट्स</div>
            <div class="result-item">अंदाजे बिलात बचत (Monthly Savings): ₹ <span id="resSavings"></span></div>
        </div>
    </div>

    <footer>
        <p>&copy; 2026 Seva First Innovation Challenge | Clean Energy Initiative</p>
    </footer>

    <script>
        function calculateSolar() {
            const bill = parseFloat(document.getElementById('bill').value);
            const area = parseFloat(document.getElementById('area').value);

            if (!bill || !area || bill <= 0 || area <= 0) {
                alert('कृपया सर्व माहिती योग्य प्रकारे भरा.');
                return;
            }

            let estimatedUnits = bill / 8;
            let recommendedKw = (estimatedUnits / 120).toFixed(1);
            if (recommendedKw < 1) recommendedKw = 1;

            let monthlyGeneration = (recommendedKw * 120).toFixed(0);
            let monthlySavings = (monthlyGeneration * 7).toFixed(0);

            document.getElementById('resCapacity').innerText = recommendedKw;
            document.getElementById('resGeneration').innerText = monthlyGeneration;
            document.getElementById('resSavings').innerText = monthlySavings;

            document.getElementById('resultBox').style.display = 'block';
        }
    </script>
</body>
</html>
