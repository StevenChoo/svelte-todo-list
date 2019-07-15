<script>
	import TodoItem from './TodoItem.svelte'

	let todos = [{ text: "Buy cookies" }, { text: "Do a little dance" }];
	let todo = "";

	function add(){
		if(todo.length === 0){
			return;
		}
		// Reactivity works based on assignment
		/* this does not work. Svelte does not see the change on the array
			todos.push({
				text:todo
			});
		*/

		// We need to assign a new array, so we just copy it
		todos = [...todos,{
			text:todo
		}];
		// Clear the text after adding the todo
		todo = "";
	}

	// Add todo when hitting enter on keyboard
	function addByEnter(event){
		if(event.key === 'Enter'){
			add();
		}
	}

	// Again we need to reassign the array for reactivity
	function remove(event){
		const todo = event.detail;
		todos = todos.filter(keep => keep !== todo)
	}

</script>

<style lang="scss">
	$border-color: 1px solid rgba(0, 0, 0, 0.1);

	.todo-list{
		display: flex;
		flex-direction: column;
		min-width: 500px;
		background: #FFFFFF;
		box-shadow: 0 -3px 10px 0 rgba(0, 0, 0, 0.1);

		* {
			margin: 0px;
			display: flex;
			flex-direction: column;
		}

		> * {
			display: flex;
			flex: 1 0;
		}

		header{

			flex-direction: row;

			input{
				flex: 1 0;
				margin: 0px;
				border: none;
				width: 100%;
				padding: 0.4rem 2.0rem;
				font-size: 24px;
				font-weight: 300;
				outline: none;
			}

			button{
				/* ripple effect - https://codepen.io/finnhvman/pen/jLXKJw */
				flex: 0 0;
				min-width: 48px;
				padding: 0rem 0.5rem;
				text-transform: uppercase;
				justify-content: center;
				align-items: center;
				color: white;
				background-color: #2196f3;
				outline: none;
				cursor: pointer;

				&.ripple {
					background-position: center;
					transition: background 0.8s;
				}
				&.ripple:hover {
					background: #47a7f5 radial-gradient(circle, transparent 1%, #47a7f5 1%) center/15000%;
				}
				&.ripple:active {
					background-color: #6eb9f7;
					background-size: 100%;
					transition: background 0s;
				}
			}
		}

		section{
			border-top: $border-color;
			min-height: 2px;
		}

		footer{
			border-top: $border-color;
			padding: 0.4rem 2rem;
			font-weight: 300;
		}
	}
</style>

<div class="todo-list">
	<header>
		<input type="text" placeholder="I need to..." bind:value={todo} on:keydown="{addByEnter}"/>
    	<button class="ripple" on:click={add}>Add</button>
	</header>
	<section>
		{#each todos as todo}
			<TodoItem on:remove={remove} bind:todo={todo}></TodoItem>
		{/each}
	</section>
	<footer>
		<div>{todos.filter(todo => !todo.done).length + ' items left'}</div>
	</footer>
</div>