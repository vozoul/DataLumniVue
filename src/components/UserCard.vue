<template>
	<div class="card-container" :class="{copy: user.copy}">
		<h2 class="identity">{{ user.name?.title.replace('Copie - ', '') }} {{ user.name.first }} {{ user.name.last }}</h2>
		<div class="card-content">
			<div class="picture">
				<img :src="user.picture?.medium" />
			</div>
			<div class="profile">
				<p><label>Nationalité : </label> {{ user?.nat || 'N/A' }}</p>
				<p><label>Date de naissance : </label> {{ formatDate(user.dob.date) }}</p>
				<p><label>Ville : </label> {{ user.location?.city || 'N/A' }}</p>
				<p><label>Pays : </label> {{ user.location?.country || 'N/A' }}</p>
				<p><label>Email : </label> {{ user?.email || 'N/A' }}</p>
				<p><label>Téléphone : </label>{{ user?.phone || 'N/A' }}</p>
				<p><label>Mobile : </label>{{ user?.cell || 'N/A' }}</p>
			</div>
		</div>
		<div class="actions">
			<button @click="duplicateUser">Dupliquer</button>
			<button @click="deleteUser">Supprimer</button>
		</div>
	</div>
</template>

<script>
/* eslint-disable */
export default {
	name: "UserCard",
	props: {
		user: Object,
	},
	methods: {
		formatDate(date) {
			const d = new Date(date);
			const options = { day: 'numeric', month: 'long', year: 'numeric' };
			return d.toLocaleDateString('fr-FR', options);
		},
		duplicateUser() {
			const newUser = JSON.parse(JSON.stringify(this.user));
			newUser.id = Math.random().toString(36).substring(7);
			this.$emit("duplicate-user", newUser);
		},
		deleteUser() {
			this.$emit("delete-user", this.user);
		}
	}
};
</script>

<style scoped>
.card-container {
	width: 640px;
	height: 380px;
	background: #e6e6e6;
	border-radius: 8px;
	box-shadow: 0 0 40px -10px #000;
	margin: 50px auto;
	padding: 0;
	max-width: calc(100vw - 40px);
	box-sizing: border-box;
	font-family: 'Montserrat', sans-serif;
	align-self: center;
	justify-self: center;
}

.copy {
	background: #ffefd6 !important;
}

.identity {
	position: relative;
	
	display: flex;
	height: 50px;
	width: 640px;
	padding: 0 30px;
	
	border-radius: 8px 8px 0 0;
	line-height: 50px;
	
	background-color: rgba(0, 0, 0, 0.4);
}

.card-content {
	position: relative;
	width: 100%;
	height: calc(100% - 100px);
	padding: 20px 30px;
	display: flex;
	flex-direction: row;
	/* overflow-y: scroll; */
}

.profile {
	padding: 0 10px;
}

.profile label {
	font-weight: bold;
}

.actions{
	position: relative;
	display: flex;
	clear: both;

	width: 100%;
	bottom: .5rem;
	right: 1.1rem;
	justify-content: flex-end;
	
	
	/* padding: 20px 30px; */
	margin-right: 0;

}

button {
	padding: 8px 12px;
	margin-left: 10px;
	font-family: 'Montserrat', sans-serif;
	border: 2px solid #78788c;
	background: 0;
	color: #5a5a6e;
	cursor: pointer;
}
</style>