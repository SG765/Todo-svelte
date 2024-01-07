<!-- CreateTodo.svelte -->
<script>
  import { authToken } from '../../stores/auth.js';
  let todoText = '';

  async function saveTodo() {
    try {
      const response = await fetch('https://todo-api-is14.onrender.com/todos', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
          'Authorization': 'Bearer YOUR_JWT_TOKEN', 
        },
        body: JSON.stringify({ text: todoText }),
      });

      if (response.ok) {
        const result = await response.json();
        alert('Todo created successfully. Todo ID:', result.id);
        const newTodo = {
          title: result.todo.title, // Replace with the actual title from your backend
        };
        todos = [newTodo, ...todos];
      } else {
        const errorData = await response.json();
        console.error('Todo creation failed:', errorData.error);
        // You can display an error message or take appropriate action on failure
      }
    } catch (error) {
      console.error('Error during todo creation:', error);
      // You can display an error message or take appropriate action on failure
    }
  }
</script>

<style>
  .form-container {
    max-width: 400px;
    margin: 20px auto;
    padding: 16px;
    border: 1px solid #ccc;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    background-color: #fff;
  }

  .form-title {
    font-size: 24px;
    font-weight: bold;
    margin-bottom: 16px;
  }

  .form-subtitle {
    font-size: 18px;
    margin-bottom: 8px;
  }

  .text-field {
    width: 100%;
    padding: 8px;
    margin-bottom: 16px;
    box-sizing: border-box;
  }

  .save-button {
    background-color: #4caf50;
    color: #fff;
    padding: 10px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }

  .save-button:hover {
    background-color: #45a049;
  }
</style>

<div class="form-container">
  <div class="form-title">Create Todo</div>
  <div class="form-subtitle">Enter Todo Text:</div>
  <textarea class="text-field" bind:value={todoText} rows="4" placeholder="Enter your todo text"></textarea>
  <button class="save-button" on:click={saveTodo}>Save</button>
</div>
