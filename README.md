# karname
<!DOCTYPE html>
<html lang="fa">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>کارنامه دانشجو</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 20px;
        }
        
        .container {
            max-width: 600px;
            margin: auto;
            background: #fff;
            padding: 20px;
            border-radius: 5px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        
        h1 {
            text-align: center;
            color: #333;
        }
    
        .input-group {
            margin-bottom: 15px;
        }
        
        label {
            display: block;
            margin-bottom: 5px;
        }
        
        input[type="text"],
        input[type="password"],
        input[type="number"] {
            width: 100%;
            padding: 8px;
            border: 1px solid #cf0d0d;
            border-radius: 4px;
        }
        
        button {
            padding: 10px 15px;
            background-color: #e65d0d;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        
        button:hover {
            background-color: #04853a;
        }
        
        .result {
            margin-top: 20px;
            font-size: 24px;
            text-align: center;
            color: #199fd4;
        }
    </style>
</head>

<body>

    <div class="container" id="loginContainer">
        <h1>ورود به سیستم</h1>
        <div class="input-group">
            <label for="username">نام کاربری:</label>
            <input type="text" id="username">
        </div>
        <div class="input-group">
            <label for="password">رمز عبور:</label>
            <input type="password" id="password">
        </div>
        <button onclick="login()">ورود</button>
    </div>

    <div class="container" id="gradesContainer" style="display:none;">
        <h1>محاسبه معدل دانشجو</h1>
        <div id="courses"></div>
        <button onclick="calculateGPA()">محاسبه معدل</button>
        <div class="result" id="result"></div>

        <script>
            const correctUsername = "daemi";
            const correctPassword = "123456";

            function login() {
                const username = document.getElementById('username').value;
                const password = document.getElementById('password').value;

                if (username === correctUsername && password === correctPassword) {
                    document.getElementById('loginContainer').style.display = 'none';
                    document.getElementById('gradesContainer').style.display = 'block';
                    displayCourses();
                } else {
                    alert('نام کاربری یا رمز عبور نادرست است.');
                }
            }

            function displayCourses() {
                const coursesDiv = document.getElementById('courses');
                coursesDiv.innerHTML = '';

                for (let i = 1; i <= 3; i++) {
                    coursesDiv.innerHTML += `
                        <div class="input-group">
                            <label for="grade${i}">نمره درس ${i}:</label>
                            <input type="number" id="grade${i}" min="0" max="20" step="0.01">
                            <label for="unit${i}">واحد درس ${i}:</label>
                            <input type="number" id="unit${i}" min="1" max="3">
                        </div>`;
                }
            }

            function calculateGPA() {
                let totalGradePoints = 0;
                let totalUnits = 0;
                let validInput = true;

                for (let i = 1; i <= 3; i++) {
                    const grade = parseFloat(document.getElementById(`grade${i}`).value);
                    const units = parseFloat(document.getElementById(`unit${i}`).value);

                    if (isNaN(grade) || grade < 0 || grade > 20) {
                        alert(`نمره درس ${i} باید بین 0 تا 20 باشد.`);
                        validInput = false;
                        break; // Exit the loop on first error
                    }

                    if (isNaN(units) || units < 1 || units > 3) {
                        alert(`واحد درس ${i} باید بین 1 تا 3 باشد.`);
                        validInput = false;
                        break; // Exit the loop on first error
                    }

                    totalGradePoints += grade * units;
                    totalUnits += units;
                }

                if (validInput) {
                    const average = totalUnits > 0 ? totalGradePoints / totalUnits : 0;
                    let resultText = `نمره معدل شما: ${average.toFixed(2)}\nکارنامه \n`;
                    document.getElementById('result').innerText = resultText;
                }
            }
        </script>


</body>

</html>
