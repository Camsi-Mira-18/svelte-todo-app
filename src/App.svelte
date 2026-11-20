<script>
  let newTodo = $state('');
  let todos = $state([
    { id: 1, text: 'Complete Svelte assignment', completed: false },
    { id: 2, text: 'Push code to GitHub', completed: false }
  ]);

  function addTodo(e) {
    e.preventDefault();
    if (!newTodo.trim()) return;
    todos.push({
      id: Date.now(),
      text: newTodo.trim(),
      completed: false
    });
    newTodo = '';
  }

  function removeTodo(id) {
    todos = todos.filter(todo => todo.id !== id);
  }
</script>

<main>
  <h1>My To-Do List</h1>

  <form onsubmit={addTodo}>
    <input 
      type="text" 
      bind:value={newTodo} 
      placeholder="Add a new task..." 
    />
    <button type="submit">Add</button>
  </form>

  <ul>
    {#each todos as todo (todo.id)}
      <li class:completed={todo.completed}>
        <label>
          <input type="checkbox" bind:checked={todo.completed} />
          <span>{todo.text}</span>
        </label>
        <button class="delete" onclick={() => removeTodo(todo.id)}>✕</button>
      </li>
    {/each}
  </ul>

  {#if todos.length === 0}
    <p class="empty">No tasks yet. Add one above!</p>
  {/if}
</main>

<style>
  main {
    max-width: 450px;
    margin: 3rem auto;
    padding: 2rem;
    font-family: system-ui, sans-serif;
    background: #ffffff;
    border-radius: 12px;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
  }

  h1 {
    text-align: center;
    color: #ff3e00;
    margin-bottom: 1.5rem;
  }

  form {
    display: flex;
    gap: 0.5rem;
    margin-bottom: 1.5rem;
  }

  input[type="text"] {
    flex: 1;
    padding: 0.65rem;
    border: 1px solid #ccc;
    border-radius: 6px;
    font-size: 1rem;
  }

  button[type="submit"] {
    padding: 0.65rem 1.2rem;
    background-color: #ff3e00;
    color: white;
    border: none;
    border-radius: 6px;
    font-size: 1rem;
    cursor: pointer;
  }

  button[type="submit"]:hover {
    background-color: #d93500;
  }

  ul {
    list-style: none;
    padding: 0;
    margin: 0;
  }

  li {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0.75rem;
    border-bottom: 1px solid #eee;
  }

  li label {
    display: flex;
    align-items: center;
    gap: 0.6rem;
    cursor: pointer;
    flex: 1;
  }

  .completed span {
    text-decoration: line-through;
    color: #888;
  }

  .delete {
    background: none;
    border: none;
    color: #888;
    font-size: 1.1rem;
    cursor: pointer;
  }

  .delete:hover {
    color: #e00;
  }

  .empty {
    text-align: center;
    color: #777;
  }
</style>