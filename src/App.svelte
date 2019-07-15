<script>
    import TodoList from './TodoList.svelte';
</script>

<style lang="scss">
    .app{
        width: 500px;
        padding: 2rem;
        margin: 0px auto;
        flex-direction: column;
        justify-content: center;
        font: 14px 'Helvetica Neue', Helvetica, Arial, sans-serif;
        line-height: 1.4rem;

        h1{
            text-align: center;
            font-family: "Helvetica Neue", Helvetica, Arial, sans-serif; 
            font-size: 48px; 
            font-style: italic; 
            font-variant: normal; 
            font-weight: 300; 
            line-height: 52.8px; 
        }

        .paper-effect {
            /* https://css-tricks.com/snippets/css/stack-of-paper/ */ 
            background: #FFFFFF;
            box-shadow:
            /* The top layer shadow */
            0 1px 1px rgba(0,0,0,0.15),
            /* The second layer */
            0 10px 0 -5px #FFFFFF,
            /* The second layer shadow */
            0 10px 1px -4px rgba(0,0,0,0.15),
            /* The third layer */
            0 20px 0 -10px #FFFFFF,
            /* The third layer shadow */
            0 20px 1px -9px rgba(0,0,0,0.15);
            padding: 0px;
        }
    }
</style>

<div class="app">
    <h1>Svelte Todo List</h1>
    <div class="paper-effect">
        <TodoList></TodoList>
    </div>
</div>