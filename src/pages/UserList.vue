<template>
	<div class="card-list">
		<h3>Liste des utilisateurs</h3>
		<a href="#" @click.prevent="openForm()" class="card-list-item add-user">Ajouter un utilisateur</a>
		<ul>
			<li v-for="u in users" :key="u.id" class="card-list-item"  :class="{ active: selectedUser === u, copy: u.copy}"  @click.prevent="selectUser(u)">
				{{ ((u.copy) ? 'Copie - ' : '') + u.name.title + ' ' + u.name.last + ' ' + u.name.first }}
			</li>
		</ul>
	</div>
	<div class="content">
		<UserCard class="content" v-if="selectedUser" :user="selectedUser" @duplicate-user="duplicateUser" @delete-user="deleteUser" />
		<AddUser class="content" v-if="addingUser" @add-user="addUser" />
	</div>
</template>

<script>
/* eslint-disable */
import UserCard from '../components/UserCard.vue';
import AddUser from '../components/AddUser.vue';

export default {
	name: "UserList",
	components: {
		UserCard,
		AddUser
	},
	data() {
		return {
			users: [],
			selectedUser: null,
			cpt: null,
			addingUser: false,
		}
	},
	created() {
		this.getUsers()
	},
	methods: {
		async getUsers() {
			try {
				const response = await fetch('https://randomuser.me/api/?results=10&nat=fr');
				const data = await response.json();
				this.users = data.results;
			} catch (error) {
				console.error(error);
			}
		},
		selectUser(user) {
			this.selectedUser = user;
			this.addingUser = false;
		},
		isCopy(user){
			return user.name.copy;
		},
		openForm(){
			this.selectedUser = null;
			this.addingUser = true;
		},
		addUser(user){
			this.users.push(user)
			this.selectUser(user);
		},
		duplicateUser(user) {
			const newUser = Object.assign({}, user);
			newUser.id = Math.floor(Math.random() * 1000);
			newUser.copy = true;
			this.users.push(newUser);
			this.selectUser(newUser);
		},
		deleteUser(user) {
			const index = this.users.indexOf(user);
			if (index !== -1) {
				this.users.splice(index, 1);
			}
			this.selectedUser = null;
		}
	}
};
</script>

<style scoped>
.card-list{
	max-width: 15vw;
	align-self: flex-start;
	
	height: calc(100vh - 50px);

	overflow-y: auto;
	flex: 1;
}

h3 {
	margin: 10px 0;
	padding-bottom: 10px;
	/* width: 180px; */
	width: 80%;
	color: #78788c;
	border-bottom: 3px solid #78788c
}

.card-list-item {
	padding: 8px 12px;
	margin: 10px 10px;
	font-family: 'Montserrat', sans-serif;
	border: 2px solid #78788c;
	background: #e1e1ff;
	color: #5a5a6e;
	cursor: pointer;
}

.add-user {
	border: 2px solid #788c79;
	background: #e1ffe3;
	color: #5a6e5b;
	margin: 0 10px;
}

.copy {
	background-color: #ffefd6;
}

.active {
	background: #5e5e6d;
	color: #fff
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

.card-list-item:hover {
	background: #78788c;
	color: #fff
}

.content {
	flex: 3;
}
</style>