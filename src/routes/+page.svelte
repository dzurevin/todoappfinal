<!--


<svelte:head>
	<link rel="stylesheet" href="https://unpkg.com/@picocss/pico@latest/css/pico.min.css">
</svelte:head>

<script>
	let toDoList = [{content: "Watch this video!", editing: false}]; //array of ToDos

</script>

<div style="margin: 0 auto; padding: 20px; width: 700px;">
	<h2 style="text-align: center;">ToDo List</h2>
	<p>Enter your ToDo here</p>
	<div>
		<input type="text">
		<button style="width: 200px;">Add</button>
	</div>
</div>

{#each toDoList as toDo, i}
<div style="display: flex; align-items: baseline; width: 700px; margin: 0 auto;">
	<input type="checkbox">
	<h4 styles="flex-grow: 1">Watch Cooper Codes</h4>
	<div style="display: flex">
		<button>Edit</button>
		<button>Delete</button>
	</div>
</div>
{#each }


-->





























<script>
     import '../style.css';
     let todoItem = '';
     let urgent, someday;
     let todoList = [];
     $: isDone = todoList.filter(item => item.done);
     $: somedayList = todoList.filter(item => item.someday)
     function addToArray() {
          if (todoItem == '') {
               return;
          }
          todoList = [...todoList, {
               text: todoItem,
               done: false,
               done: false,
               urgent: urgent,
               someday: someday
          }];
          console.log(todoList);
          todoItem = '';
          todoList.splice(index, 1);
          todoList = todoList;
     }
     function clearDone() {
          todoList = todoList.filter(item => !item.done)
     }
</script>

<h1>Todo!</h1>

<form on:submit|preventDefault={addToArray}>
     <input type="text" bind:value={todoItem}>
     <button type="submit">Add</button>
     <p>Choose Category:</p>
     <input type="checkbox" name="urgent" id="urgent" bind:checked={urgent}>
     <label for="urgent">Urgent</label>
     <input type="checkbox" name="someday" id="someday" bind:checked={someday}>
     <label for="someday">Some Day</label>
     <div>
          <button type="submit">Add</button>
     </div>
</form>

<ul>
     {#each todoList as item, index}
          <li>
               <input type="checkbox" bind:checked={item.done}>

               <span class:done={item.done} >{item.text}</span>
               <span on:click={() => removeThis(index)} class="remove" role="button" tabindex="0">&times;</span>
          </li>
     {/each}
</ul>
{#if somedayList.length > 0}
     <h2>Someday</h2>
     <ul>
          {#each somedayList as item, index}
               <li>{item.text}</li>
          {/each}
     </ul>
{/if}
{#if isDone.length > 0}
<button on:click={clearDone}>Remove Done</button>
{/if}

<style>
     ul {
          list-style: none;
     }
     li {
          font-size: 1.3rem;
     }
     .done {
          color: #ccc;
          text-decoration: line-through;
     }
     .remove {
          color: darkred;
          cursor: pointer;
     }
</style>















<!-- 
<script>
	import '../style.css'
	let todoitem = '';
	let todolist = [];

	function addToArray() {
		if (todoitem == '') {
			return;
		}
		todolist = [...todolist, {
			text: todoitem,
			done: false
		}];
		console.log(todolist);
		todoitem = '';
	}



	function removeThis(index){
		todolist.splice(index, 1);
		todolist = todolist;
	}

</script>

<h1>To Do List Ferda!</h1>

<form on:submit|preventDefault={addToArray}>
	<input type="text" bind:value={todoitem}>
	<button type="submit">Add</button>
</form>

<ul>
	{#each todolist as item, index}
		<li>
			<input type="checkbox" bind:checked={item.done}>
			<span class:done={item.done} >{item.text}</span>
			<span on:click={() => removeThis(index)} class="remove" role="button" tabindex="0">&times;</span>
		</li>
	{/each}
</ul>

	<style>
		ul {
			list-style: none;
		}
		li{
			font-size: 1.3rem;
		}
		.done {
			color: grey;
			text-decoration: line-through;
		}
		.remove{
			color: darkred;
			cursor:pointer;
		}

	</style>

-->