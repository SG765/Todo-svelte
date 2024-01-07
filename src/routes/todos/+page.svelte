<script>
  import Card from './card.svelte';
  import CreateTodo from './createTodo.svelte';
  import todos from './createTodo.svelte';
  import { authToken } from '../../stores/auth.js';
  import onMount from 'svelte';

  onMount(async () => {
    // Fetch user's todos using the access token from the store
    const token = $authToken; // Use $ prefix to access the current value of the store
    alert(token)
    await fetchUserTodos(token);
  });

  async function fetchUserTodos(token) {
    try {
      const response = await fetch('https://todo-api-is14.onrender.com/todos', {
        method: 'GET',
        headers: {
          'Authorization': `Bearer ${token}`,
        },
      });

      if (response.ok) {
        const userTodos = await response.json();
        $todos = userTodos;
      } else {
        const errorData = await response.json();
        alert('Error fetching user todos:', errorData.error);
      }
    } catch (error) {
      alert('Error during fetchUserTodos:', error);
    }
  }
  
</script>

<main>
<h1>User Todos</h1>
<CreateTodo />
<Card/>
</main>