<script>
  import { writable } from 'svelte/store'
  import Todo from './Todo.svelte'

  let title = ''; 
  let todos = writable([]);
  let id = 0;

  function createTodo() {
    $todos.push({
      id,
      title
    }) // 배열에 아이템을 추가하는 것은 할당이 아님. 따라서 화면이 바뀌지 않음
    $todos = $todos; // 할당으로 반응성 유지 - svelte에서 자주 볼 코드
    title = '';
    id += 1;
  }
</script>

<input bind:value={title}
      type="text"
      on:keydown={(e) => {e.key === 'Enter' && createTodo()}}>
<button on:click={createTodo}>
	Create Todo
</button>

{#each $todos as todo}
  <Todo {todos} {todo} />
{/each}