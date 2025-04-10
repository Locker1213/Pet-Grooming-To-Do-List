<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pet Grooming To-Do List</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            margin: 0;
            padding: 0;
            background-image: url('Pet Grooming');
            background-size: cover;
            background-position: center;
            background-attachment: fixed;
            color: #333;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .overlay {
            background-color: rgba(255, 255, 255, 0.85);
            padding: 30px;
            border-radius: 15px;
            width: 90%;
            max-width: 500px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }

        .header {
            text-align: center;
            margin-bottom: 25px;
        }

        h1 {
            color: #4a6b57;
            margin-bottom: 5px;
            font-size: 28px;
        }

        .subtitle {
            color: #6d8b74;
            font-size: 18px;
            margin-bottom: 20px;
            font-weight: bold;
        }

        .task-list {
            margin: 20px 0;
        }

        .task-item {
            display: flex;
            align-items: center;
            padding: 12px 0;
            border-bottom: 1px solid #e0e0e0;
        }

        .task-item:last-child {
            border-bottom: none;
        }

        .task-checkbox {
            margin-right: 15px;
            width: 18px;
            height: 18px;
            accent-color: #4a6b57;
        }

        .task-text {
            flex-grow: 1;
            font-size: 16px;
        }

        .task-text.completed {
            text-decoration: line-through;
            color: #888;
        }

        .add-task {
            margin-top: 25px;
            display: flex;
        }

        .task-input {
            flex-grow: 1;
            padding: 12px 15px;
            border: 1px solid #ddd;
            border-radius: 8px 0 0 8px;
            font-size: 16px;
            outline: none;
        }

        .add-btn {
            background-color: #4a6b57;
            color: white;
            border: none;
            border-radius: 0 8px 8px 0;
            padding: 0 20px;
            cursor: pointer;
            font-size: 16px;
            transition: background-color 0.3s;
        }

        .add-btn:hover {
            background-color: #3a5a47;
        }
    </style>
</head>
<body>
    <div class="overlay">
        <div class="header">
            <h1>Pet Grooming</h1>
            <div class="subtitle">Add New</div>
        </div>

        <div class="task-list">
            <div class="task-item">
                <input type="checkbox" id="task1" class="task-checkbox">
                <label for="task1" class="task-text">Medicated shampooing</label>
            </div>
            <div class="task-item">
                <input type="checkbox" id="task2" class="task-checkbox">
                <label for="task2" class="task-text">Nail trimming</label>
            </div>
            <div class="task-item">
                <input type="checkbox" id="task3" class="task-checkbox">
                <label for="task3" class="task-text">Brushing</label>
            </div>
            <div class="task-item">
                <input type="checkbox" id="task4" class="task-checkbox">
                <label for="task4" class="task-text">Ear cleaning</label>
            </div>
        </div>

        <div class="add-task">
            <input type="text" class="task-input" id="newTask" placeholder="Add new task...">
            <button class="add-btn" id="addTaskBtn">+</button>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const addTaskBtn = document.getElementById('addTaskBtn');
            const newTaskInput = document.getElementById('newTask');
            const taskList = document.querySelector('.task-list');
            
            // Add new task
            addTaskBtn.addEventListener('click', addTask);
            newTaskInput.addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    addTask();
                }
            });
            
            // Checkbox functionality
            document.querySelectorAll('.task-checkbox').forEach(checkbox => {
                checkbox.addEventListener('change', function() {
                    const label = this.nextElementSibling;
                    label.classList.toggle('completed', this.checked);
                });
            });
            
            function addTask() {
                const taskText = newTaskInput.value.trim();
                if (taskText) {
                    const taskId = 'task-' + Date.now();
                    const taskItem = document.createElement('div');
                    taskItem.className = 'task-item';
                    taskItem.innerHTML = `
                        <input type="checkbox" id="${taskId}" class="task-checkbox">
                        <label for="${taskId}" class="task-text">${taskText}</label>
                    `;
                    taskList.appendChild(taskItem);
                    
                    // Add event listener to new checkbox
                    taskItem.querySelector('.task-checkbox').addEventListener('change', function() {
                        const label = this.nextElementSibling;
                        label.classList.toggle('completed', this.checked);
                    });
                    
                    newTaskInput.value = '';
                    newTaskInput.focus();
                }
            }
        });
    </script>
</body>
</html>
