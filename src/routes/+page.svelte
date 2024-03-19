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

