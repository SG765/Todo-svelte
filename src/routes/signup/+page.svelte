<!-- Signup.svelte -->
<script>
  import { onMount } from 'svelte';

  let signupData = {
    username: '',
    email: '',
    password: '',
  };

  // Function to handle form submission
  async function signupaction() {
    try {
      const response = await fetch('https://todo-api-is14.onrender.com/signup', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(signupData),
      });

      if (response.ok) {
        // Signup successful
        alert("Sign up Successful")
        redirectToLogin();
      } else {
        // Signup failed
        const errorData = await response.json();
        console.error('Signup failed:', errorData.error);
        // You can display an error message or toast here
      }
    } catch (error) {
      console.error('Error during signup:', error);
    }
  }

  // Optional: Function to redirect to the login page
  function redirectToLogin() {
     window.location.href = '/login';
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

<main>
  <h1>Signup Page</h1>
  <form on:submit|preventDefault={signupaction}>
    <label>
      Username:
      <input bind:value={signupData.username} />
    </label>
    <label>
      Email:
      <input type="email" bind:value={signupData.email} />
    </label>
    <label>
      Password:
      <input type="password" bind:value={signupData.password} />
    </label>
    <button type="submit">Sign Up</button>
  </form>
</main>
