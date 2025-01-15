<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>상환 능력 평가</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            background-color: #f8f9fa;
            color: #333;
        }
        h1 {
            text-align: center;
            color: #4CAF50;
        }
        .container {
            max-width: 600px;
            margin: 0 auto;
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        label {
            display: block;
            margin: 10px 0 5px;
            font-weight: bold;
        }
        input[type="number"] {
            width: 100%;
            padding: 10px;
            margin: 5px 0 15px;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        button {
            width: 100%;
            padding: 10px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
        }
        button:hover {
            background-color: #45a049;
        }
        .result {
            margin-top: 20px;
            padding: 10px;
            background-color: #e7f3e9;
            border: 1px solid #4CAF50;
            border-radius: 4px;
        }
        .error {
            color: red;
            font-size: 14px;
            margin-top: -10px;
            margin-bottom: 10px;
        }
    </style>
</head>
<body>
    <h1>상환 능력 평가</h1>
    <div class="container">
        <form id="evaluationForm">
            <label for="loanAmount">대출 금액 (원):</label>
            <input type="number" id="loanAmount" placeholder="대출 금액을 입력하세요" required>

            <label for="annualIncome">연소득 (원):</label>
            <input type="number" id="annualIncome" placeholder="연소득을 입력하세요" required>

            <label for="debtAmount">부채 금액 (원):</label>
            <input type="number" id="debtAmount" placeholder="부채 금액을 입력하세요" required>

            <div id="error" class="error" style="display: none;">모든 값을 정확히 입력하세요.</div>

            <button type="button" onclick="evaluateLoanCapacity()">평가하기</button>
        </form>

        <div id="result" class="result" style="display: none;">
            <h3>평가 결과</h3>
            <p id="dtiResult"></p>
            <p id="dsrResult"></p>
        </div>
    </div>

    <script>
        function evaluateLoanCapacity() {
            // 사용자 입력값 가져오기
            const loanAmount = parseFloat(document.getElementById("loanAmount").value);
            const annualIncome = parseFloat(document.getElementById("annualIncome").value);
            const debtAmount = parseFloat(document.getElementById("debtAmount").value);

            // 오류 메시지 숨기기
            const errorElement = document.getElementById("error");
            errorElement.style.display = "none";

            // 입력값 유효성 검사
            if (isNaN(loanAmount) || isNaN(annualIncome) || isNaN(debtAmount) || annualIncome <= 0) {
                errorElement.style.display = "block";
                return;
            }

            // DTI 및 DSR 계산
            const dti = ((loanAmount / annualIncome) * 100).toFixed(2);
            const dsr = (((loanAmount + debtAmount) / annualIncome) * 100).toFixed(2);

            // 결과 표시
            document.getElementById("result").style.display = "block";
            document.getElementById("dtiResult").innerText = `DTI (총부채상환비율): ${dti}%`;
            document.getElementById("dsrResult").innerText = `DSR (총원리금상환비율): ${dsr}%`;
        }
    </script>
</body>
</html>
