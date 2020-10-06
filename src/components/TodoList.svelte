<script>
  let todos = [];
  $: sortedTodos = todos.sort((a, b) => a.priority >= b.priority && a.value.toLowerCase() >= b.value.toLowerCase());
  $: priorityOptions = todos.map((todo, index) => index + 1);
  let value = '';

  function addTodo({ key }) {
    if (key === 'Enter' && value.length && !todos.find(({ value: todoValue }) => todoValue === value)) {
      todos = [...todos, { complete: false, priority: todos.length + 1, value }];
      value = '';
    }
  };

  function setTodoProperty(updatedObj, index) {
    if (todos[index] && updatedObj && Object.keys(updatedObj).length) {
      todos[index] = {
        ...todos[index],
        ...updatedObj,
      };
    }
  };

  function removeTodo(index) {
    if (index > -1) {
      todos = [...todos.slice(0, index), ...todos.slice(index + 1)];
    }
  };

  function fetchPriorityCount(priorityInteger) {
    return todos.filter(({ priority }) => priority === priorityInteger).length;
  }
</script>

<div class="container">
  <div class="field has-addons">
    <p class="control">
      <input bind:value class="input is-medium" class:is-danger={!!todos.find(({ value: todoValue }) => todoValue === value)} on:keypress={addTodo} placeholder="Add a new task...">
    </p>
  </div>

  <nav class="level">
    {#each priorityOptions as priorityOption}
      <div class="level-item has-text-centered">
        <div>
          <p class="heading">Priority #{priorityOption} Items</p>
          <p class="title">{fetchPriorityCount(priorityOption)}</p>
        </div>
      </div>
    {/each}
  </nav>
  <table class="table is-hoverable is-fullwidth">
    <thead>
      <tr>
        <th>Priority</th>
        <th>Title</th>
        <th>Actions</th>
      </tr>
    </thead>
    <tbody>
      {#each sortedTodos as { value, complete, priority }, index (index)}
        <tr>
          <th>
            <div class="control">
              <div class="select">
                <select bind:value={priority}>
                  {#each priorityOptions as priorityOption}
                    <option>{priorityOption}</option>
                  {/each}
                </select>
              </div>
            </div>
          </th>
          <th on:click={() => setTodoProperty({ complete: !complete }, index)} class="is-clickable">
            <span class:complete>{value}</span>
          </th>
          <th>
            <button class="delete" on:click={() => removeTodo(index)}></button>
          </th>
        </tr>
      {/each}
    </tbody>
  </table>
</div>

<style type="text/scss">
  @import 'bulma/bulma';
  .complete {
    text-decoration: line-through;
  }
  .delete {
    padding: 0;
  }
</style>