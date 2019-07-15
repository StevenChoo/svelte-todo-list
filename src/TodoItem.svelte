<script>
	// Import other components
	import TodoCheckBox from './TodoCheckBox.svelte';
	import { createEventDispatcher } from 'svelte';

	// Component properties need to be exported to be available
	export let todo;

	// Event dispatcher to pass event to parent
	const dispatch = createEventDispatcher();

	// Local property
	let done = false;

	// https://svelte.dev/docs#3_$_marks_a_statement_as_reactive
	// Reactive statement using Javascript labels
	// the property done of the todo object is changed reactively
	$: todo.done = done;

	// You can also do
	// The console.log will react on the changed variable 'done'
	$: console.log("State of checked item: ", done);

	function checked(){
		debugger;
	}

	function remove(todo){
		dispatch('remove',todo);
	}

</script>

<style lang="scss">
	.todo-item {
		display: flex;
		flex: 1 0;
		flex-direction: row;
		border-bottom: 1px solid rgba(0, 0, 0, 0.1);

		&:last-child{
			border-bottom: none;
		}

		* {
			margin: 0px;
			display: flex;
		}

		.todo-check{
			width: 2rem;
			justify-content: center;
			align-items: center;
			line-height: 0px;
		}

		.todo-text{
			flex: 1 0;
			
			input{
				font-size: 24px;
				font-weight: 300;
				padding: 0.4rem 0rem;
				outline: none;
			}
		}

		.todo-remove{
			width: 48px;
			align-items: center;
			justify-content: center;
			font-size: 20px;
			outline: none;
			color: rgba(0,0,0,0.7);

			&:hover{
				color:#2196f3;	
			}

			&:active{
				color:#6eb9f7;
			}
			
		}

		.strikethrough {
			display: inline-block;
			position: relative;
			transition: all 0.5s cubic-bezier(.55, 0, .1, 1);
		}

		.strikethrough:after {
			content: '';
			flex: 0 0;
			position: absolute;
			display: block;
			width: 100%;
			height: 1px;
			box-shadow: 0 1px rgba(255,255,255,0.6);
			margin-top: -21px;
			background: black;
		}
	}
</style>


<div class="todo-item">
	<div class="todo-check">
		<TodoCheckBox bind:checked={done} on:input={checked} ></TodoCheckBox>
	</div>
	<div class="todo-text {done ? 'strikethrough' : ''}">
		<input type="text" bind:value={todo.text}/>
	</div>
	<button class="todo-remove" on:click={() => remove(todo)}>×</button>
</div>