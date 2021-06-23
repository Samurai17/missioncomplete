<script>

	let input1 = "";
	let input2 = "";
	let input3 = "";
	let input4 = "";
	let input5 = "";
	let input6 = "";
	let input7 = "";
	let input8 = "";
	let input9 = "";
	let input10 = "";
	let input11 = "";
	let input12 = "";
	let input13 = "";
	let input14 = "";
	let input15 = "";

	let users = [];

	async function adduser() {
		let user = {
			id: Number(input1), 
			firstname: input2,
			lastname: input3, 
			email: input4, 
			pwd: input5
		}
		console.log( {user} )
		const r = await fetch('http://localhost:7000/api/users' , {
			method: 'POST',
			cache: 'no-cache',
			credentials: 'same-origin',
			headers: {
				'Content-Type': 'application/json'
			},
			body: JSON.stringify( {user} )
		});
	}

	async function upuser() {
		let user = {
			id: Number(input6), 
			firstname: input7,
			lastname: input8, 
			email: input9, 
			pwd: input10
		}
		const r = await fetch('http://localhost:7000/api/users' , {
			method: 'PUT',
			cache: 'no-cache',
			credentials: 'same-origin',
			headers: {
				'Content-Type': 'application/json'
			},
			body: JSON.stringify( {user} )
		});
	}

	async function deluser() {
		let user = {
			id: Number(input11)
		}
		const d = await fetch('http://localhost:7000/api/users', {
 		 method: 'DELETE',
		cache: 'no-cache',
		credentials: 'same-origin',
		headers: {
				'Content-Type': 'application/json'
			},
		 body: JSON.stringify(user)
		})
		.then(res => res.text())
		.then(res => console.log(res))
	}

	async function getResponse() {
		let response = await fetch('http://localhost:7000/api/users')
		let content = await response.json()
		console.log(content)
		users = Object.values(content);
	}
getResponse()


</script>
<main>

	<form class="form1" on:submit|preventDefault={adduser}>
		<h2>Заявка</h2>
		<input bind:value={input1} type="number" placeholder="Ваш ID">
		<input bind:value={input2} type="text" placeholder="Введите имя">
		<input bind:value={input3} type="text" placeholder="Введите фамилию">
		<input bind:value={input4} type="email" placeholder="Введите емейл">
		<input bind:value={input5} placeholder="Введите пароль" type = 'password'>
		<br><button> Подтвердить </button>
	</form>
	<form class="form2" on:submit|preventDefault={upuser}>
		<h2>Заявка на изменение</h2>
		<input bind:value={input6} type="number" placeholder="Ваш ID">
		<input bind:value={input7} type="text" placeholder="Введите имя">
		<input bind:value={input8} type="text" placeholder="Введите фамилию">
		<input bind:value={input9} type="email" placeholder="Введите емейл">
		<input bind:value={input10} placeholder="Введите пароль" type = 'password'>
		<br><button> Подтвердить </button>
	</form>
	<form class="form2" on:submit|preventDefault={deluser}>
		<h2>Заявка на удаление</h2>
		<input bind:value={input11} type="number" placeholder="Ваш ID">
		<!-- <input bind:value={input12} type="text" placeholder="Введите имя">
		<input bind:value={input13} type="text" placeholder="Введите фамилию">
		<input bind:value={input14} type="email" placeholder="Введите емейл">
		<input bind:value={input15} placeholder="Введите пароль" type = 'password'> -->
		<br><button> Подтвердить </button>
	</form>
	<div class = 'tab'>
		<table class="users" cellspacing = "0">
		<caption>Список заявок</caption>
		<tr>
		<th>ID</th><th class = 'f_name'>Имя</th><th class = 'tag'>Фамилия</th><th class = 'date'>Электронная почта</th><th class = 'date'>Пароль</th>
		</tr>
		<tr>
			<td><span>{#each users as user} {user.id} <br>{/each}</span></td>
			<td><span>{#each users as user} {user.firstname}<br> {/each}</span></td>
			<td><span>{#each users as user} {user.lastname} <br>{/each}</span></td>
			<td><span id="em">{#each users as user}{user.email}<br>{/each}</span></td>
			<td><span>{#each users as user}{user.pwd}<br>{/each}</span></td>
		</tr>
		</table>
	</div>
</main>

<style>
	main {
	text-align: center;
	max-width: 100%;
	margin: 0 auto;
	}


	table {
		margin: auto;
		width: 1200px;
		border: 1px solid black;
		margin: 15px;
	}

	caption {
		font-weight: bold;
		font-size: 25px;
		margin-bottom: 10px;
	}

	.tab {
		width: 100%;
		text-align: center;
	}
	th {
	font-size: 15px;
	color: #777;
	border: 1px solid black;
	}
	
	td {
	border: 1px solid black;
	}
	
	tr {
	border: 1px solid black;
	}
	
	#em {
	color: blue;
	}
	
	input {
	border: 2px solid black;
	border-radius: 15px;
	width: 300px;
	}
	
	button {
	background: #fff;
	color: #000;
	border-radius: 15px;
	border: 2px solid #000;
	}

	button:hover {
		background: #000;
		color: #fff;
	}
	</style>