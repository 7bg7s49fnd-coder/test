沒人贊助ˊˋ
<html lang="zh-TW">
<head>
<meta charset="UTF-8">
<title>線芯顏色計算</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
body {
    font-family: "Microsoft JhengHei", "微軟正黑體",
                 -apple-system, BlinkMacSystemFont,
                 "PingFang TC", "Heiti TC", sans-serif;
    background: radial-gradient(circle at top, #1b1f2a, #000000);
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    margin: 0;
    color: #ffffff;
}
.container {
    background: rgba(20, 24, 36, 0.9);
    backdrop-filter: blur(10px);
    padding: 35px 30px;
    border-radius: 22px;
    width: 100%;
    max-width: 430px;
    box-shadow:
        0 0 0 1px rgba(0,122,255,0.25),
        0 15px 40px rgba(0,0,0,0.8),
        inset 0 0 30px rgba(0,122,255,0.08);
    text-align: center;
}

h2 {
    margin-bottom: 25px;
    font-size: 26px;
    letter-spacing: 2px;
    color: #e6f1ff;
    text-shadow: 0 0 12px rgba(0,122,255,0.6);
}

input, select {
    width: 100%;
    padding: 13px 15px;
    margin-bottom: 15px;
    font-size: 16px;
    border-radius: 12px;
    border: 1px solid rgba(0,122,255,0.4);
    background: #0d111c;
    color: #ffffff;
    outline: none;
}

button {
    width: 100%;
    padding: 14px;
    font-size: 18px;
    border-radius: 14px;
    border: none;
    cursor: pointer;
    background: linear-gradient(135deg, #007aff, #00c6ff);
    color: white;
    font-weight: bold;
}

.result {
    margin-top: 25px;
    padding: 18px;
    border-radius: 16px;
    font-size: 22px;
    font-weight: bold;
    background: linear-gradient(135deg, #0a1a33, #08101f);
    color: #7ec8ff;
    min-height: 60px;
    display: flex;
    align-items: center;
    justify-content: center;
}
</style>
</head>

<body>
<div class="container">
    <h2>線芯顏色計算</h2>

    <select id="mode">
        <option value="20"> 帶狀(溝槽型) </option>
        <option value="24"> 24C（6C×4）</option>
        <option value="48"> 48C（6C×8）</option>
        <option value="96"> 96C（8C×12）</option>
        <option value="216"> 216C（12C×18）</option>
    </select>

    <input type="number" id="startCore" value="1" placeholder="起始芯數">
    <input type="number" id="inputCore" placeholder="請輸入芯數">

    <button onclick="calculate()">計算</button>

    <div class="result" id="resultText">結果顯示</div>
</div>

<script>
function calculate() {
    const mode = document.getElementById("mode").value;
    const start = parseInt(document.getElementById("startCore").value);
    const input = parseInt(document.getElementById("inputCore").value);
    const result = document.getElementById("resultText");

    if (isNaN(start) || isNaN(input) || start <= 0 || input <= 0) {
        result.textContent = "請輸入正確數字";
        return;
    }

    const a = start + input - 1;

    /* ===== 20 芯 ===== */
    if (mode === "20") {
        const colors = [
            "紫粉","藍","藍1白","藍2白","藍粉",
            "黃","黃1白","黃2白","黃粉",
            "綠","綠1白","綠2白","綠粉",
            "紅","紅1白","紅2白","紅粉",
            "紫","紫1白","紫2白"
        ];

        let g, color;
        if (a % 20 === 0) {
            g = a / 20;
            color = "紫粉";
        } else {
            g = Math.floor(a / 20) + 1;
            color = colors[a % 20];
        }

        result.textContent = `第 ${a} 芯 → 第 ${g} 溝 ${color}`;
        return;
    }

    /* ===== 24 / 48 ===== */
    if (mode === "24" && a > 24 || mode === "48" && a > 48) {
        result.textContent = "超出範圍";
        return;
    }

    if (mode === "24" || mode === "48") {
        const core6 = ["藍","黃","綠","紅","紫","白"];
        const tube24 = ["藍","黃","綠","紅"];
        const tube48 = ["藍","黃","綠","紅","紫","白","黑","橘"];

        const tubeIndex = Math.floor((a - 1) / 6);
        const coreIndex = (a - 1) % 6;
        const tubeColor = mode === "48" ? tube48[tubeIndex] : tube24[tubeIndex];

        result.textContent = `第 ${a} 芯 → ${tubeColor}管 ${core6[coreIndex]}芯線`;
        return;
    }

    /* ===== 96 ===== */
    if (mode === "96") {
        if (a > 96) {
            result.textContent = "超過 96 芯範圍";
            return;
        }

        const core8 = ["藍","黃","綠","紅","紫","白","棕","黑"];
        const tube96 = ["藍","黃","綠","紅","紫","白","棕","黑","青","橙","粉","灰"];

        const tubeIndex = Math.floor((a - 1) / 8);
        const coreIndex = (a - 1) % 8;

        result.textContent = `第 ${a} 芯 → ${tube96[tubeIndex]}管 ${core8[coreIndex]}芯線`;
        return;
    }

    /* ===== 216（12 芯 × 18 管）===== */
    if (mode === "216") {
        if (a > 216) {
            result.textContent = "超過 216 芯範圍";
            return;
        }

        const core12 = ["藍","黃","綠","紅","紫","白","棕","黑","青","橙","粉","灰"];
        const tube216 = [
            "內藍","內黃","內綠","內紅","內紫","內白",
            "外藍","外黃","外綠","外紅","外紫","外白",
            "外棕","外黑","外青","外橙","外粉","外灰"
        ];

        const tubeIndex = Math.floor((a - 1) / 12);
        const coreIndex = (a - 1) % 12;

        result.textContent = `第 ${a} 芯 → ${tube216[tubeIndex]}管 ${core12[coreIndex]}芯線`;
    }
}
document.addEventListener("keydown", function (e) {
    if (e.key === "Enter") {
        calculate();
    }
});
</script>
</body>
</html>
