<!-- card.svelte -->
<style>
  .card {
    border: 1px solid #ccc;
    border-radius: 8px;
    padding: 16px;
    margin: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    background-color: #fff;
  }

  .title {
    font-size: 18px;
    font-weight: bold;
    margin-bottom: 8px;
  }

  .description {
    font-size: 14px;
    color: #555;
  }
</style>

<script>
  export let todo = {};

  // Todo data structure:
  // {
  //   title: 'Todo Title',
  //   description: 'Todo Description',
  // }
</script>

<div class="card">
  <div class="title">{todo.title}</div>
  <div class="description">{todo.description}</div>
  <!-- Additional content or actions related to the todo item can be added here -->
</div>
