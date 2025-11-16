<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>BMI Calculator</title>
    <style>
        body {
            background-color: #004040;
            font-family: 'Segoe UI Semibold', sans-serif;
            color: #000000;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        .container {
            background-color: #2f5959;
            border: 5px solid #90c1c1;
            padding: 30px 40px;
            border-radius: 8px;
            width: 400px;
            box-sizing: border-box;
        }
        h1 {
            text-align: center;
            font-weight: 900;
            margin-bottom: 25px;
            color: black;
        }
        label {
            font-weight: 700;
            display: block;
            margin-bottom: 6px;
        }
        input[type=text], input[type=number], select {
            width: 100%;
            padding: 8px 10px;
            margin-bottom: 16px;
            border: none;
            border-radius: 4px;
            font-size: 14px;
        }
        select {
            cursor: pointer;
        }
        button {
            background-color: #005050;
            color: #000;
            padding: 8px 16px;
            margin-right: 15px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-weight: 600;
            transition: background-color 0.3s ease;
        }
        button:hover {
            background-color: #008080;
            color: white;
        }
        .buttons {
            display: flex;
            justify-content: flex-start;
        }
        #result {
            margin-top: 20px;
            padding: 12px;
            background-color: #cce6e6;
            border-radius: 6px;
            font-weight: 700;
            color: #003333;
            display: none;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>BMI CALCULATOR</h1>

        <label for="name">Nama :</label>
        <input type="text" id="name" placeholder="Masukkan nama anda" />

        <label for="age">Usia :</label>
        <input type="number" id="age" min="0" placeholder="Masukkan usia anda" />

        <label for="gender">Jenis Kelamin :</label>
        <select id="gender">
            <option value="" disabled selected>Pilih Jenis Kelamin</option>
            <option value="Laki-laki">Laki-laki</option>
            <option value="Perempuan">Perempuan</option>
            <option value="Lainnya">Lainnya</option>
        </select>

        <label for="height">Tinggi Badan (cm) :</label>
        <input type="number" id="height" min="0" placeholder="Masukkan tinggi badan anda dalam cm" />

        <label for="weight">Berat Badan (kg) :</label>
        <input type="number" id="weight" min="0" placeholder="Masukkan berat badan anda dalam kg" />

        <div class="buttons">
            <button type="button" onclick="calculateBMI()">Hitung BMI</button>
            <button type="button" onclick="resetForm()">Reset</button>
        </div>

        <div id="result"></div>
    </div>

    <script>
        function calculateBMI() {
            const name = document.getElementById('name').value.trim();
            const age = Number(document.getElementById('age').value);
            const gender = document.getElementById('gender').value;
            const heightCm = Number(document.getElementById('height').value);
            const weightKg = Number(document.getElementById('weight').value);
            const resultDiv = document.getElementById('result');

            // Validasi input
            if (!name) {
                alert('Mohon masukkan nama anda.');
                return;
            }
            if (!age || age <= 0) {
                alert('Mohon masukkan usia yang valid.');
                return;
            }
            if (!gender) {
                alert('Mohon pilih jenis kelamin.');
                return;
            }
            if (!heightCm || heightCm <= 0) {
                alert('Mohon masukkan tinggi badan yang valid.');
                return;
            }
            if (!weightKg || weightKg <= 0) {
                alert('Mohon masukkan berat badan yang valid.');
                return;
            }

            const heightM = heightCm / 100;
            const bmi = weightKg / (heightM * heightM);
            const bmiRounded = bmi.toFixed(2);

            let status = '';
            if (bmi < 18.5) {
                status = 'Kurus';
            } else if (bmi < 25) {
                status = 'Normal';
            } else if (bmi < 30) {
                status = 'Kelebihan berat badan';
            } else {
                status = 'Obesitas';
            }

            resultDiv.style.display = 'block';
            resultDiv.innerHTML = `
                Halo <strong>${name}</strong>! <br />
                Usia: ${age} tahun, Jenis Kelamin: ${gender} <br />
                BMI Anda adalah <strong>${bmiRounded}</strong>, Status: <strong>${status}</strong>.
            `;
        }

        function resetForm() {
            document.getElementById('name').value = '';
            document.getElementById('age').value = '';
            document.getElementById('gender').selectedIndex = 0;
            document.getElementById('height').value = '';
            document.getElementById('weight').value = '';
            document.getElementById('result').style.display = 'none';
        }
    </script>
</body>
</html>
