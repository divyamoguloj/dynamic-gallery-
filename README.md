<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Dynamic Gallery</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      margin: 0;
      padding: 0;
      background: #111;
      color: #eee;
    }

    .container {
      width: 95%;
      margin: 30px auto;
      background: #1a1a1a;
      padding: 20px;
      border-radius: 12px;
      box-shadow: 0 10px 20px rgba(255, 0, 0, 0.3);
      display: flex;
      flex-wrap: wrap;
    }

    .task-list {
      flex: 1 1 220px;
      background: linear-gradient(135deg, #8b0000, #000000);
      border-radius: 12px;
      padding: 20px;
      margin-right: 20px;
      color: #fff;
      box-shadow: 0 6px 12px rgba(255, 0, 0, 0.4);
    }

    .task-list h1 {
      font-size: 24px;
      margin-bottom: 20px;
      text-align: center;
      color: #ff4444;
      font-weight: bold;
    }

    ul {
      list-style: none;
      padding: 0;
      margin: 0;
    }

    li {
      padding: 12px 16px;
      margin-bottom: 10px;
      border-radius: 8px;
      background-color: rgba(255, 255, 255, 0.05);
      color: #fff;
      cursor: pointer;
      transition: background-color 0.3s ease, transform 0.3s ease;
    }

    li:hover {
      background-color: rgba(255, 68, 68, 0.2);
      transform: scale(1.03);
    }

    li.active {
      background-color: #ff4444;
      color: #000;
      font-weight: bold;
      box-shadow: 0 4px 12px rgba(255, 0, 0, 0.3);
    }

    .content-area {
      flex: 3 1 600px;
      padding: 20px;
      border-radius: 12px;
      background-color: #000;
      border: 1px solid #ff4444;
      box-shadow: 0 4px 12px rgba(255, 0, 0, 0.3);
      min-height: 520px;
      position: relative;
      overflow: hidden;
    }

    iframe {
      width: 100%;
      height: 500px;
      border: none;
      border-radius: 8px;
      background-color: #111;
    }

    /* Transitions */
    .transition-flip { animation: flip 0.7s ease forwards; }
    .transition-zoom { animation: zoomIn 0.7s ease forwards; }
    .transition-slide-blur { animation: slideBlur 0.8s ease forwards; }
    .transition-fade-scale { animation: fadeScale 0.6s ease forwards; }

    @keyframes flip {
      0% { opacity: 0; transform: rotateY(90deg) scale(0.8); }
      100% { opacity: 1; transform: rotateY(0deg) scale(1); }
    }

    @keyframes zoomIn {
      0% { opacity: 0; transform: scale(0.4) rotate(-10deg); }
      100% { opacity: 1; transform: scale(1) rotate(0); }
    }

    @keyframes slideBlur {
      0% { opacity: 0; transform: translateX(80px); filter: blur(5px); }
      100% { opacity: 1; transform: translateX(0); filter: blur(0); }
    }

    @keyframes fadeScale {
      0% { opacity: 0; transform: scale(1.2) rotate(3deg); }
      100% { opacity: 1; transform: scale(1) rotate(0); }
    }

    @media (max-width: 768px) {
      .container { flex-direction: column; }
      .task-list { margin-right: 0; margin-bottom: 20px; }
      .content-area { margin-left: 0; }
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="task-list">
      <h1>Dynamic Gallery</h1>
      <ul id="taskList"></ul>
    </div>
    <div class="content-area" id="contentArea">
      <p>Select a task to view its content.</p>
    </div>
  </div>

  <!-- 🔊 Audio element for click sound -->
  <audio id="clickSound" preload="auto">
    <source src="click.mp3" type="audio/mpeg">
    <!-- Alternative fallback -->
    <source src="click.ogg" type="audio/ogg">
    Your browser does not support audio.
  </audio>

  <script>
    const tasks = [
      { name: "Task 1", file: "workspace/task1.html" },
      { name: "Task 2", file: "workspace/task2.html" },
      { name: "Task 3", file: "workspace/task3.html" },
      { name: "Task 4", file: "workspace/task4.html" },
      { name: "Task 5", file: "workspace/task5.html" },
      { name: "Task 6", file: "workspace/task6.html" },
      { name: "Task 7", file: "workspace/task7.html" },
      { name: "Task 8", file: "workspace/task8.html" },
      { name: "Task 9", file: "workspace/task9.html" },
      { name: "Task 10", file: "workspace/task10.html" },
      { name: "Task 11", file: "workspace/task11.html" },
      { name: "Task 12", file: "workspace/task12.html" },
      { name: "Task 13", file: "workspace/task13.html" },
      { name: "Task 14", file: "workspace/task14.html" },
      { name: "Task 15", file: "workspace/task15.html" },
      { name: "Task 16", file: "workspace/task16.html" }
    ];

    const taskList = document.getElementById('taskList');
    const contentArea = document.getElementById('contentArea');
    const clickSound = document.getElementById('clickSound');
    const transitions = ['transition-flip', 'transition-zoom', 'transition-slide-blur', 'transition-fade-scale'];

    tasks.forEach(task => {
      const listItem = document.createElement('li');
      listItem.textContent = task.name;

      listItem.addEventListener('click', () => {
        document.querySelectorAll('#taskList li').forEach(li => li.classList.remove('active'));
        listItem.classList.add('active');

        // Play sound
        clickSound.currentTime = 0;
        clickSound.play();

        // Remove existing transition
        contentArea.classList.remove(...transitions);

        const chosenTransition = transitions[Math.floor(Math.random() * transitions.length)];

        contentArea.style.opacity = 0;
        setTimeout(() => {
          contentArea.innerHTML = `<iframe src="${task.file}"></iframe>`;
          contentArea.classList.add(chosenTransition);
          contentArea.style.opacity = 1;
        }, 300);
      });

      taskList.appendChild(listItem);
    });
  </script>
</body>
</html>
