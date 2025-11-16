<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>给欣欣的告白</title>
    <style>
        /* 页面样式，确保手机端适配 */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            width: 100vw;
            height: 100vh;
            background-color: #f8f9fa;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            font-family: "Microsoft YaHei", sans-serif;
            padding: 20px;
        }
        /* 问题文本 */
        .question {
            font-size: 24px;
            font-weight: bold;
            color: #333;
            text-align: center;
            margin-bottom: 80px;
            line-height: 1.5;
        }
        /* 选项容器（用于选项2动态定位） */
        .option-box {
            position: relative;
            width: 100%;
            max-width: 500px;
            display: flex;
            justify-content: space-around;
        }
        /* 选项通用样式 */
        .option {
            width: 140px;
            height: 60px;
            border-radius: 30px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 18px;
            font-weight: bold;
            color: white;
            cursor: pointer;
            transition: all 0.2s;
            user-select: none; /* 禁止选中文字 */
        }
        /* 选项1：愿意（可正常点击） */
        #yes {
            background-color: #e74c3c;
            position: relative;
            z-index: 1;
        }
        #yes:active {
            transform: scale(1.05);
            background-color: #c0392b;
        }
        /* 选项2：不愿意（会躲避） */
        #no {
            background-color: #95a5a6;
            position: absolute; /* 绝对定位，用于移动 */
            z-index: 2;
        }
        /* 成功弹窗（默认隐藏） */
        .modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.6);
            display: none; /* 初始隐藏 */
            align-items: center;
            justify-content: center;
            z-index: 999;
        }
        .modal-content {
            background-color: white;
            padding: 40px 20px;
            border-radius: 20px;
            text-align: center;
            max-width: 80%;
        }
        .modal-text {
            font-size: 22px;
            color: #2c3e50;
            line-height: 1.8;
            font-weight: 500;
        }
    </style>
</head>
<body>
    <!-- 问题 -->
    <div class="question">你愿意嫁给我吗小笨蛋欣欣</div>
    
    <!-- 选项容器 -->
    <div class="option-box">
        <div class="option" id="yes">1：愿意</div>
        <div class="option" id="no">2：不愿意</div>
    </div>
    
    <!-- 成功弹窗 -->
    <div class="modal" id="successModal">
        <div class="modal-content">
            <div class="modal-text">我会爱你一辈子的欣欣，爱你的李奥迪</div>
        </div>
    </div>

    <script>
        // 核心交互逻辑
        const yesBtn = document.getElementById('yes');
        const noBtn = document.getElementById('no');
        const modal = document.getElementById('successModal');
        const optionBox = document.querySelector('.option-box');
        
        // 页面加载后，初始化选项2位置（与选项1对称）
        window.onload = function() {
            const boxWidth = optionBox.offsetWidth;
            // 让选项2初始在容器右侧，与选项1对齐
            noBtn.style.left = (boxWidth - 140) + 'px'; // 140是选项宽度
            noBtn.style.top = '0px';
        };

        // 点击“愿意”：显示弹窗
        yesBtn.addEventListener('click', function() {
            modal.style.display = 'flex';
        });

        // 点击“不愿意”：随机移动（躲避点击）
        noBtn.addEventListener('click', function() {
            const boxWidth = optionBox.offsetWidth;
            const boxHeight = optionBox.offsetHeight;
            const btnWidth = noBtn.offsetWidth; // 选项2宽度
            const btnHeight = noBtn.offsetHeight; // 选项2高度
            
            // 随机生成新位置（确保不超出容器范围）
            const randomLeft = Math.floor(Math.random() * (boxWidth - btnWidth));
            const randomTop = Math.floor(Math.random() * (boxHeight - btnHeight));
            
            // 应用新位置
            noBtn.style.left = randomLeft + 'px';
            noBtn.style.top = randomTop + 'px';
        });
    </script>
</body>
</html>
