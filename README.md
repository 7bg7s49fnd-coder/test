
<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <title>帶狀算溝</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        /* 整體美化 */
        body {
            font-family: 'Noto Sans TC', -apple-system, BlinkMacSystemFont, sans-serif;
            background: linear-gradient(to bottom, #f5f7fa, #c3cfe2);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            padding: 20px;
        }

        .container {
            background-color: #ffffffcc;
            padding: 40px 30px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            width: 100%;
            max-width: 400px;
            text-align: center;
        }

        h2 {
            margin-bottom: 30px;
            color: #333;
            font-size: 28px;
        }

        input {
            font-size: 18px;
            padding: 12px 15px;
            width: 100%;
            margin-bottom: 20px;
            border: 2px solid #ddd;
            border-radius: 10px;
            transition: border-color 0.3s;
        }

        input:focus {
            border-color: #007aff;
            outline: none;
        }

        button {
            font-size: 18px;
            padding: 12px 15px;
            width: 100%;
            border: none;
            border-radius: 10px;
            background-color: #007aff;
            color: white;
            cursor: pointer;
            transition: background-color 0.3s, transform 0.2s;
        }

        button:hover {
            background-color: #005bb5;
            transform: translateY(-2px);
        }

        .result {
            margin-top: 25px;
            font-size: 22px;
            font-weight: bold;
            color: #007aff;
            padding: 15px;
            border-radius: 12px;
            background-color: #e0f0ff;
            min-height: 50px;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: background-color 0.3s, color 0.3s;
        }
    </style>
</head>
<body>

    <div class="container">
        <h2>帶狀算溝</h2>
        <input type="number" id="inputA" placeholder="請輸入芯數" onkeydown="checkEnter(event)">
        <button onclick="calculate()">計算</button>
        <div class="result" id="resultText">結果會顯示在這裡</div>
    </div>

    <script>
        // 按 Enter 鍵就送出
        function checkEnter(event) {
            if (event.key === "Enter") {
                calculate();
            }
        }

        function calculate() {
            const a = parseInt(document.getElementById("inputA").value);
            const result = document.getElementById("resultText");

            if (isNaN(a) || a <= 0) {
                result.textContent = "請輸入正確的數字";
                result.style.backgroundColor = "#ffe0e0";
                result.style.color = "#ff3b3b";
                return;
            }

            let g, b, color;

            if (a % 20 === 0) {
                g = a / 20;
                color = "紫粉";
            } else {
                g = Math.floor(a / 20) + 1;
                b = a % 20;

                switch (b) {
                    case 1: color = "藍"; break;
                    case 2: color = "藍1白"; break;
                    case 3: color = "藍2白"; break;
                    case 4: color = "藍粉"; break;
                    case 5: color = "黃"; break;
                    case 6: color = "黃1白"; break;
                    case 7: color = "黃2白"; break;
                    case 8: color = "黃粉"; break;
                    case 9: color = "綠"; break;
                    case 10: color = "綠1白"; break;
                    case 11: color = "綠2白"; break;
                    case 12: color = "綠粉"; break;
                    case 13: color = "紅"; break;
                    case 14: color = "紅1白"; break;
                    case 15: color = "紅2白"; break;
                    case 16: color = "紅粉"; break;
                    case 17: color = "紫"; break;
                    case 18: color = "紫1白"; break;
                    case 19: color = "紫2白"; break;
                    case 0: color = "紫粉"; break;
                }
            }

            result.textContent = g + "溝" + color;
            result.style.backgroundColor = "#e0f0ff";
            result.style.color = "#007aff";
        }
    </script>

</body>
</html>
