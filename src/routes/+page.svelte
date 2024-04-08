

<svelte:head>
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@picocss/pico@2/css/pico.amber.min.css"/> 
</svelte:head>

<script>

	//importing transitions
	import { fly } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
	import { fade } from 'svelte/transition';
	import { blur } from 'svelte/transition';
	import { slide } from 'svelte/transition';
	import { scale } from 'svelte/transition';



	
//FUNCTIONALITY
     //import '@picocss/pico'
     import '../style.css'
	import { writable } from 'svelte/store';
     
	let toDoList = writable([]); // array of To Dos
     let textInput = "";
	let storedList, savedMode, darkMode;













//DARK AND LIGHT MODE



	function toggle() {
        darkMode = !darkMode;
	   localStorage.setItem('savedMode', darkMode);
        window.document.body.classList.toggle('dark');
	   console.log(darkMode);
    }
















	if (typeof window !== 'undefined' && typeof localStorage !== 'undefined') {
		storedList = localStorage.getItem('storedList');
		savedMode = localStorage.getItem('savedMode');
		if(storedList) {
			$toDoList = (JSON.parse(storedList));
		}
		if (savedMode && savedMode === 'true') {
			darkMode = true;
			window.document.body.classList.add('dark');
		}
		else {
			darkMode = false;
		}
	}

	function updateList() {
		return storedList = localStorage.setItem('storedList', JSON.stringify($toDoList));
	}
     function addToDo() {
        $toDoList = [...$toDoList, { content: textInput, editing: false, checked: false }];
	   //New
        updateList();
     }
     function setEditing(i, isEditing) {
        $toDoList[i].editing = isEditing; 
	   //New
        updateList();
     }
     function deleteTodo(i) {
        $toDoList.splice(i, 1);
        $toDoList = $toDoList; 
	   //New
        updateList();
     }



</script>


<div class="main">




	
	<button style="margin: 1em;" on:click={toggle}>
		{#if darkMode}
			Go Blue
		{:else}
			Go Pink
		{/if}
	</button>










<div style="margin: 0 auto; padding-top: 2em; width: 75vw;">
    <h2 style="text-align: center;">To Do List</h2>
    <p>Enter your upcoming commitments here:</p>
    <div class="inputAndAddButton" style="display: flex; margin: 0;">
        <input style="margin: 0;" type="text" bind:value={textInput}>
        <button style="margin-left: 1em; margin-right:0; width: 11em;" on:click={addToDo}>Add</button>
    </div>
</div>

{#each $toDoList as toDo, i}
    <div transition:blur={{ amount: 10 }} style="display: flex; align-items: baseline; width: 75vw; margin: 0 auto; margin-top: 1em;">
        {#if toDo.editing}
            <input type="text" bind:value={toDo.content}>
        {:else}
            <input transition:blur={{ amount: 10 }} type="checkbox" bind:checked={toDo.checked}>
            <h4 style="flex-grow: 1;">{toDo.content}</h4>
        {/if}
        <div style="display: flex">
            {#if toDo.editing}
                <button style="margin-left: 0.7em;" on:click={() => setEditing(i, false)}>Save</button>
            {:else}
                <button style="margin-left: 0.7em;" on:click={() => setEditing(i, true)}>Edit</button>
            {/if}
            <button style="margin-left: 0.7em;" on:click={() => deleteTodo(i)}>Delete</button>
        </div>
    </div>
{/each}

<div id="footer-container">
     <footer id="footer"></footer>
</div>


</div>




<style>
	:root{
		--bg-color: rgb(113, 204, 216);
		--text-color: #000000;
	}
	
	:global(body) {
		background: var(--bg-color);
		color: var(--text-color);
	}
	
	:global(body.dark) {
		--bg-color: #e393d6;
		--text-color: #ff8dec;
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