# Ex03 To-Do List using JavaScript
## Date:

## AIM
To create a To-do Application with all features using JavaScript.

## ALGORITHM
### STEP 1
Build the HTML structure (index.html).

### STEP 2
Style the App (style.css).

### STEP 3
Plan the features the To-Do App should have.

### STEP 4
Create a To-do application using Javascript.

### STEP 5
Add functionalities.

### STEP 6
Test the App.

### STEP 7
Open the HTML file in a browser to check layout and functionality.

### STEP 8
Fix styling issues and refine content placement.

### STEP 9
Deploy the website.

### STEP 10
Upload to GitHub Pages for free hosting.

## PROGRAM

## HTML
```

<!DOCTYPE html>
<html>
<head>
    <title>Todo Application</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

    <div class="container">
        <h1>My Todo Application</h1>

        <div class="input-section">
            <input type="text" id="taskInput"
                   placeholder="Enter your task">
            <button onclick="addTask()">Add Task</button>
        </div>

        <input type="text" id="searchInput"
               placeholder="Search tasks..."
               oninput="displayTasks()">

        <div class="filters">
            <button onclick="setFilter('all')">All</button>
            <button onclick="setFilter('pending')">Pending</button>
            <button onclick="setFilter('completed')">Completed</button>
        </div>

        <ul id="taskList"></ul>

        <footer>
            Name: Your Name | Register Number: Your Register Number
        </footer>
    </div>

    <script src="script.js"></script>
</body>
</html>

```
## CSS
```

body {
    font-family: Arial, sans-serif;
    background: #e8f0f7;
    margin: 0;
    padding: 30px;
}

.container {
    background: white;
    max-width: 600px;
    margin: auto;
    padding: 25px;
    border-radius: 10px;
    box-shadow: 0 0 10px gray;
}

h1 {
    text-align: center;
    color: #17365d;
}

input {
    padding: 12px;
    margin: 8px 0;
    width: 65%;
    border: 1px solid gray;
    border-radius: 5px;
}

button {
    padding: 10px;
    margin: 4px;
    background: #17365d;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

button:hover {
    background: #2874a6;
}

.filters {
    margin: 15px 0;
    text-align: center;
}

ul {
    padding: 0;
}

li {
    list-style: none;
    background: #edf2f7;
    padding: 12px;
    margin: 8px 0;
    border-radius: 5px;
}

.completed {
    text-decoration: line-through;
    color: gray;
}

footer {
    text-align: center;
    margin-top: 30px;
    font-size: 14px;
    color: #17365d;
}

```
## JAVASCRIPT
```

let tasks = JSON.parse(localStorage.getItem("tasks")) || [];
let currentFilter = "all";

function saveTasks() {
    localStorage.setItem("tasks", JSON.stringify(tasks));
}

function addTask() {
    let input = document.getElementById("taskInput");
    let task = input.value.trim();

    if (task === "") {
        alert("Please enter a task!");
        return;
    }

    tasks.push({
        id: Date.now(),
        name: task,
        completed: false
    });

    input.value = "";
    saveTasks();
    displayTasks();
}

function displayTasks() {
    let list = document.getElementById("taskList");
    let search = document.getElementById("searchInput")
                      .value.toLowerCase();

    list.innerHTML = "";

    let filteredTasks = tasks.filter(task => {
        let matchesSearch = task.name.toLowerCase().includes(search);

        let matchesFilter =
            currentFilter === "all" ||
            (currentFilter === "pending" && !task.completed) ||
            (currentFilter === "completed" && task.completed);

        return matchesSearch && matchesFilter;
    });

    filteredTasks.forEach(task => {
        let li = document.createElement("li");

        if (task.completed) {
            li.classList.add("completed");
        }

        let name = document.createElement("span");
        name.textContent = task.name;

        let completeBtn = document.createElement("button");
        completeBtn.textContent = task.completed ? "Undo" : "Complete";
        completeBtn.onclick = () => toggleTask(task.id);

        let editBtn = document.createElement("button");
        editBtn.textContent = "Edit";
        editBtn.onclick = () => editTask(task.id);

        let deleteBtn = document.createElement("button");
        deleteBtn.textContent = "Delete";
        deleteBtn.onclick = () => deleteTask(task.id);

        li.append(name, completeBtn, editBtn, deleteBtn);
        list.appendChild(li);
    });
}

function toggleTask(id) {
    tasks = tasks.map(task =>
        task.id === id
            ? {...task, completed: !task.completed}
            : task
    );

    saveTasks();
    displayTasks();
}

function editTask(id) {
    let task = tasks.find(task => task.id === id);
    let newName = prompt("Edit your task:", task.name);

    if (newName !== null && newName.trim() !== "") {
        task.name = newName.trim();
        saveTasks();
        displayTasks();
    }
}

function deleteTask(id) {
    if (confirm("Are you sure you want to delete this task?")) {
        tasks = tasks.filter(task => task.id !== id);
        saveTasks();
        displayTasks();
    }
}

function setFilter(filter) {
    currentFilter = filter;
    displayTasks();
}

displayTasks();

```

## OUTPUT

<img width="1795" height="948" alt="image" src="https://github.com/user-attachments/assets/2be53403-74f1-4188-bbb4-5c24350fab8d" />

## RESULT
The program for creating To-do list using JavaScript is executed successfully.
