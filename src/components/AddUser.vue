<template>
	<form class="form" @submit.prevent="submitForm">
		<h2>Ajouter un utilisateur</h2>
		<p>
			<label for="lastName">Civilité:</label>
			<select type="text" id="lastName" placeholder="nom de famille" v-model="form.name.title" >
				<option value="M.">Monsieur</option>
				<option value="Mme">Madame</option>
			</select>
		</p>
		<p>
			<label for="lastName">Nom:</label>
			<input type="text" id="lastName" placeholder="nom de famille" v-model="form.name.last" required />
		</p>
		<p>
			<label for="firstName">Prénom:</label>
			<input type="text" id="firstName" placeholder="prénom" v-model="form.name.first" required />
		</p>
		<p>
			<label for="nationality">Nationnalité:</label>
			<input type="text" id="nationality" placeholder="prénom" v-model="form.nationality" />
		</p>
		<p>
			<label for="dob">Date de naissance:</label>
			<input type="date" id="dob" placeholder="prénom" v-model="form.dob.date" required />
		</p>
		<p>
			<label for="email">Email:</label>
			<input type="email" id="email" placeholder="" v-model="form.email"
				required />
		</p>
		<button type="submit">Ajouter</button>
	</form>
</template>
  
<script>
export default {
	data() {
		return {
			form: {
				name: {
					title: '',
					first: '',
					last: '',
				},
				nationality: '',
				picture: {
					medium: null,
				},
				dob: {date: ''},
				email: '',
				message: ''
			}
		};
	},
	methods: {
		submitForm() {
			const newUser = JSON.parse(JSON.stringify(this.form));
			newUser.id = Math.random().toString(36).substring(7);
			this.$emit("add-user", newUser);
		}
	}
};
</script>

<style scoped>
body {
	background: #59ABE3;
	margin: 0
}

.form {
	width: 64vw;
	height: 52vh;
	background: #e6e6e6;
	border-radius: 8px;
	box-shadow: 0 0 40px -10px #000;
	margin: 50px auto;
	padding: 20px 30px;
	max-width: calc(100vw - 40px);
	box-sizing: border-box;
	font-family: 'Montserrat', sans-serif;
	position: relative;

	overflow-y: scroll;
}

h2 {
	margin: 10px 0;
	padding-bottom: 10px;
	/* width: 180px; */
	width: 50%;
	color: #78788c;
	border-bottom: 3px solid #78788c
}

input {
	width: 100%;
	padding: 10px;
	box-sizing: border-box;
	background: none;
	outline: none;
	resize: none;
	border: 0;
	font-family: 'Montserrat', sans-serif;
	transition: all .3s;
	border-bottom: 2px solid #bebed2
}

input:focus {
	border-bottom: 2px solid #78788c
}

p:before {
	content: attr(type);
	display: block;
	margin: 28px 0 0;
	font-size: 14px;
	color: #5a5a5a
}

button {
	float: right;
	padding: 8px 12px;
	margin: 8px 0 0;
	font-family: 'Montserrat', sans-serif;
	border: 2px solid #78788c;
	background: 0;
	color: #5a5a6e;
	cursor: pointer;
	transition: all .3s
}

button:hover {
	background: #78788c;
	color: #fff
}

div {
	content: 'Hi';
	position: absolute;
	bottom: -15px;
	right: -20px;
	background: #50505a;
	color: #fff;
	width: 320px;
	padding: 16px 4px 16px 0;
	border-radius: 6px;
	font-size: 13px;
	box-shadow: 10px 10px 40px -14px #000
}

span {
	margin: 0 5px 0 15px
}</style>