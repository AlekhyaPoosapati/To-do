<script>
	let src = "images/todoicon.png"
	import Fa from 'svelte-fa'
     import { faPlus } from '@fortawesome/free-solid-svg-icons'
	import { faMinus } from '@fortawesome/free-solid-svg-icons'
	import { onMount } from 'svelte';
	let text = " ";
	let date = new Date(), month, day, year;
	let dateString;
	
	onMount(()=> {
        month = '' + (date.getMonth() + 1),
        day = '' + date.getDate(),
        year = date.getFullYear();

    if (month.length < 2) 
        month = '0' + month;
    if (day.length < 2) 
        day = '0' + day;

    dateString = [day, month, year].join('-');
	})
	let todos = [{id : 1 ,text : "complete cyber security course"},
	{id : 2 ,text : "complete svelte tutorials"},
	{id : 3 ,text : "complete a project"},];
	let x = todos.length;
	let color = ['#FF5147','#F9C50B','#42A0FF'];
	function add() {
		x++;
		todos = [ ...todos,{id : x , done: false ,text }];
          text = "";		
	}
	const remove = todo => {
          todos = todos.filter(i => i !== todo);
		x--;
     };
	let i = -1;
	function getColor() {
		i++;
		if (i<3)
		    return i;
		else 
		    return i%3;
	}
</script>
<body>
	<div class = "container">
		<div class = "headerpart">
			<img class = "image" src = {src} alt = "icon" />
		     <h1 class = "heading">To-do List</h1>

		</div>
		<div class = "taskcreation">
			<input class = "inputbox" bind:value = {text} placeholder="task title"/>
			<button on:click = {add} class = "icondiv"><Fa icon={ faPlus } /></button>
		</div>
		<div class = "datecount">
			<p>Tasks - {x}</p>
			<p>{dateString}</p>
		</div>
		<div class = "scrolling">
		{#each todos as todo}
			<div class = taskdiv>	 
				<div style = "background-color: {color[getColor()]}" class = "tasks"><p class = "texttodo">{todo.text}</p></div>
				<button class = "removebutton" on:click={() => {remove(todo)}}><Fa icon = { faMinus } /></button>
		     </div>
		{/each}
	</div>

	</div>


</body>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Montserrat&display=swap');
	body
	{
		margin: 0%;
		background: linear-gradient(to right, #E67ACC, #FD9EA9);
		font-family: 'Montserrat', sans-serif;
	}
	.container
	{
		margin-top: 3%;
		width: 60%;
		margin-left: 18%;
		margin-right: 20%;
		border: none;
		text-align: center;
		padding: 30px;
		background-color: black;
		border-radius: 15px;
	}
	.headerpart
	{
		display: flex;
		text-align: center;
		width: 40%;
		margin-left: 30%;
		margin-right: 30%;
		margin-bottom: 30px;
		justify-content: space-around;
		align-items: center;
	}
	.image
	{
		height: 70px;
		width: 70px;
	}
	.heading
	{
		color: white;
		font-family: 'Montserrat', sans-serif;
	}
	.inputbox
	{
		width: 45%;
		border-top-left-radius: 15px;
		border-bottom-right-radius: 15px;
		outline: none;
		border: 1px solid blueviolet;
		background-color: black;
	}
	input 
	{
          caret-color: white;
		color: white;
     }
	.icondiv
	{
		padding: 7px 10px;
		background-color: blueviolet;
		color: white;
		border: none;
		border-radius: 5px;
		cursor: pointer;
	}
	.datecount
	{
		display: flex;
		width: 40%;
		margin-left: 30%;
		margin-bottom: 10px;
		justify-content: space-between;
		color: aliceblue;
	}
	.scrolling
	{
		height: 220px;
		overflow-y: scroll;
	}
	.taskdiv
	{
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		width: 60%;
		padding: 10px;
		margin-left: 20%;
		margin-right: 20%;	
	}
	.tasks
	{
		width: 70%;
		height: 7vh;
		border: none;
		border-radius: 50px;
		padding: 5px 50px;
		overflow-x: scroll;
		overflow-y: hidden;
	}
	::-webkit-scrollbar {
          display: none;
     }
	.removebutton
	{
		padding: 7px 10px;
		margin-top: 2%;
		background-color: #FF2E45;
		border: none;
		border-radius: 70px;
		color: white;
		cursor: pointer;
	}
	.texttodo
	{
		text-align: center;
		margin-top: 3%;
		color: black;
		font-weight: bold;
	}
</style>