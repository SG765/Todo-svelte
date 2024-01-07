<!-- Loginpage.svelte -->
<script>
  import { authToken } from '../../stores/auth.js';
  
  let loginData = {
    username: '',
    password: '',
  };

  async function login() {
    try {
      const response = await fetch('https://todo-api-is14.onrender.com/login', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(loginData),
      });

      if (response.ok) {
        const { access_token } = await response.json();
        // Assuming your server returns an access_token
        alert('Login successful');
        // Redirect to the home page or any other page after successful login
        authToken.set(access_token);
        window.location.href = '/todos';
        
      } else {
        const errorData = await response.json();
        alert('Login failed:', errorData.msg);
      }
    } catch (error) {
      alert('Error during login:', error);
    }
  }
</script>

<style>
  form {
    margin: auto;
    width: fit-content;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 5px;
    place-items: center;
  }

  label{
    display: flex;
    place-items: center;
    margin:20px;
  }

  input {
    padding: 8px;
    margin: 10px;
    box-sizing: border-box;
  }

  button {
    background-color: blue;
    place-items: center;
    color: white;
    padding: 10px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }

  button:hover {
    background-color: darkblue;
  }
</style>

<!-- Include the Header component -->
<svelte:head>
  <title>Login</title>
  <meta name="description" content="Svelte demo app" />
</svelte:head>

<!-- Login form -->
<form on:submit|preventDefault={login}>
  <label>
    Username:
    <input bind:value={loginData.username} />
  </label>
  <label>
    Password:
    <input type="password" bind:value={loginData.password} />
  </label>
  <button type="submit">Login</button>
</form>
