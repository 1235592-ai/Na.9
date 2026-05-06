<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>감정 기록장</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            background-color: #f4f4f9;
            color: #333;
            margin: 0;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        .container {
            width: 100%;
            max-width: 400px;
            background: white;
            padding: 20px;
            border-radius: 12px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
        }
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        input[type="date"] {
            border: none;
            font-size: 1.1em;
            font-weight: bold;
            color: #333;
            outline: none;
            background: transparent;
        }
        .slider-container {
            text-align: center;
            margin-bottom: 20px;
        }
        .score-display {
            font-size: 2em;
            font-weight: bold;
            margin-bottom: 10px;
            color: #555;
        }
        input[type="range"] {
            width: 100%;
            margin: 10px 0;
        }
        textarea {
            width: 100%;
            box-sizing: border-box;
            height: 80px;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 8px;
            resize: none;
            margin-bottom: 15px;
            font-family: inherit;
        }
        button {
            width: 100%;
            padding: 12px;
            background-color: #2c3e50;
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 1.1em;
            font-weight: bold;
            cursor: pointer;
        }
        button:active {
            background-color: #1a252f;
        }
        .chart-container {
            margin-top: 30px;
            width: 100%;
            height: 200px;
        }
        .history-list {
            margin-top: 20px;
            border-top: 1px solid #eee;
            padding-top: 10px;
        }
        .history-item {
            padding: 10px 0;
            border-bottom: 1px solid #f9f9f9;
            font-size: 0.9em;
        }
        .history-time { font-weight: bold; color: #777; margin-right: 10px; }
        .history-score { 
            display: inline-block; 
            width: 30px; 
            text-align: center; 
            font-weight: bold; 
            border-radius: 4px;
        }
        .score-pos { background: #e3f2fd; color: #1565c0; }
        .score-neg { background: #ffebee; color: #c62828; }
        .score-zero { background: #f5f5f5; color: #616161; }
        .history-memo { display: block; margin-top: 5px; color: #555; }
    </style>
</head>
<body>

<div class="container">
    <div class="header">
        <input type="date" id="datePicker">
    </div>

    <div class="slider-container">
        <div class="score-display" id="scoreDisplay">0</div>
        <input type="range" id="emotionSlider" min="-10" max="10" value="0">
    </div>

    <textarea id="memoInput" placeholder="지금 기분에 영향을 준 일이 있나요? (선택)"></textarea>
    <button onclick="saveRecord()">기록하기</button>

    <div class="chart-container">
        <canvas id="emotionChart"></canvas>
    </div>

    <div class="history-list" id="historyList"></div>
</div>

<script>
    const datePicker = document.getElementById('datePicker');
    const slider = document.getElementById('emotionSlider');
    const scoreDisplay = document.getElementById('scoreDisplay');
    const memoInput = document.getElementById('memoInput');
    const historyList = document.getElementById('historyList');
    let chartInstance = null;

    // 1. 날짜 초기화 (오늘 날짜)
    const today = new Date();
    const todayString = today.toISOString().split('T')[0];
    datePicker.value = todayString;

    // 날짜 변경 시 데이터 다시 불러오기
    datePicker.addEventListener('change', loadData);

    // 슬라이더 값 변경 시 숫자 업데이트 및 색상 변경
    slider.addEventListener('input', (e) => {
        const val = parseInt(e.target.value);
        scoreDisplay.innerText = val > 0 ? `+${val}` : val;
        scoreDisplay.style.color = val > 0 ? '#1565c0' : (val < 0 ? '#c62828' : '#555');
    });

    // 2. 데이터 저장
    function saveRecord() {
        const date = datePicker.value;
        const time = new Date().toLocaleTimeString('ko-KR', { hour: '2-digit', minute: '2-digit' });
        const score = parseInt(slider.value);
        const memo = memoInput.value.trim();

        const record = { time, score, memo };
        
        let allData = JSON.parse(localStorage.getItem('emotionData')) || {};
        if (!allData[date]) allData[date] = [];
        
        allData[date].push(record);
        
        // 시간순 정렬
        allData[date].sort((a, b) => a.time.localeCompare(b.time));
        
        localStorage.setItem('emotionData', JSON.stringify(allData));
        
        // 입력창 초기화
        slider.value = 0;
        scoreDisplay.innerText = '0';
        scoreDisplay.style.color = '#555';
        memoInput.value = '';
        
        loadData(); // 화면 갱신
    }

    // 3. 데이터 불러오기 및 UI 렌더링
    function loadData() {
        const date = datePicker.value;
        const allData = JSON.parse(localStorage.getItem('emotionData')) || {};
        const dayData = allData[date] || [];

        renderChart(dayData);
        renderHistory(dayData);
    }

    // 4. Chart.js 그래프 그리기
    function renderChart(data) {
        const ctx = document.getElementById('emotionChart').getContext('2d');
        
        if (chartInstance) chartInstance.destroy(); // 기존 차트 삭제

        const labels = data.map(d => d.time);
        const scores = data.map(d => d.score);

        chartInstance = new Chart(ctx, {
            type: 'line',
            data: {
                labels: labels,
                datasets: [{
                    label: '감정 수치',
                    data: scores,
                    borderColor: '#2c3e50',
                    backgroundColor: 'rgba(44, 62, 80, 0.1)',
                    borderWidth: 2,
                    pointBackgroundColor: scores.map(s => s > 0 ? '#1565c0' : (s < 0 ? '#c62828' : '#555')),
                    pointRadius: 4,
                    fill: true,
                    tension: 0.3 // 부드러운 곡선
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                scales: {
                    y: {
                        min: -10,
                        max: 10,
                        ticks: { stepSize: 5 }
                    }
                },
                plugins: {
                    legend: { display: false }
                }
            }
        });
    }

    // 5. 하단 기록 리스트 렌더링
    function renderHistory(data) {
        historyList.innerHTML = '';
        if (data.length === 0) {
            historyList.innerHTML = '<div style="text-align:center; color:#999; padding:20px;">기록이 없습니다.</div>';
            return;
        }

        // 최신 기록이 위로 오게 역순 렌더링
        [...data].reverse().forEach(d => {
            const scoreClass = d.score > 0 ? 'score-pos' : (d.score < 0 ? 'score-neg' : 'score-zero');
            const scoreText = d.score > 0 ? `+${d.score}` : d.score;
            
            const item = document.createElement('div');
            item.className = 'history-item';
            item.innerHTML = `
                <div>
                    <span class="history-time">${d.time}</span>
                    <span class="history-score ${scoreClass}">${scoreText}</span>
                </div>
                ${d.memo ? `<span class="history-memo">${d.memo}</span>` : ''}
            `;
            historyList.appendChild(item);
        });
    }

    // 앱 시작 시 데이터 로드
    loadData();
</script>

</body>
</html>
