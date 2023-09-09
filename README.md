<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Kanban Board</title>

    <link rel="stylesheet" href="styles.css" />
    <script src="drag.js" defer></script>
    <script src="todo.js" defer></script>
  </head>
  <body>
    <div class="board">
      <form id="todo-form">
        <input type="text" placeholder="New TODO..." id="todo-input" />
        <button type="submit">Add +</button>
      </form>

      <div class="lanes">
        <div class="swim-lane" id="todo-lane">
          <h3 class="heading">TODO</h3>

          <p class="task" draggable="true">Clean Room</p>
          <p class="task" draggable="true">Cook</p>
          <p class="task" draggable="true">Study</p>
        </div>

        <div class="swim-lane">
          <h3 class="heading">Doing</h3>

          <p class="task" draggable="true">making Bed</p>
        </div>

        <div class="swim-lane">
          <h3 class="heading">Done</h3>

          <p class="task" draggable="true">
            Singing Practice
          </p>
        </div>
      </div>
    </div>
    <script>
      // Function to handle the drag start event
      function dragStart(event) {
          event.dataTransfer.setData("text/plain", event.target.id);
      }

      // Function to allow dropping a task
      function allowDrop(event) {
          event.preventDefault();
      }

      // Function to handle the drop event
      function drop(event, targetColumnId) {
          event.preventDefault();
          const taskId = event.dataTransfer.getData("text/plain");
          const targetColumn = document.getElementById(targetColumnId);
          const task = document.getElementById(taskId);

          // Check if the target is a column div
          if (targetColumn.classList.contains("column")) {
              targetColumn.appendChild(task);
              enableEditAndDelete(task);
          }
      }

      // Function to enable edit and delete for a task
      function enableEditAndDelete(task) {
          task.addEventListener("dblclick", () => {
              const newText = prompt("Edit task:", task.textContent);
              if (newText !== null) {
                  task.textContent = newText;
              }
          });

          const deleteButton = document.createElement("button");
          deleteButton.className = "delete-button";
          deleteButton.textContent = "Delete";
          deleteButton.addEventListener("click", () => {
              if (confirm("Delete this task?")) {
                  task.remove();
              }
          });

          task.appendChild(deleteButton);
      }

      // Function to add a new task
      function addTask(columnId) {
          const column = document.getElementById(columnId);
          const task = document.createElement("div");
          task.className = "task";
          task.textContent = "New Task";
          task.setAttribute("draggable", "true");
          task.id = `task-${Date.now()}`;
          
          enableEditAndDelete(task);

          task.addEventListener("dragstart", dragStart);

          column.appendChild(task);
      }
  </script>
  </body>
</html># Yashashree
