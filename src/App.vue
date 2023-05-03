<template>
	<header>
		<nav class="navbar">
			<h1 class="brand-name">Brand-Name</h1>
			<ul class="nav-menu-list" >
				<li v-for="m in menu" :key="m.name" class="nav-menu" >
					<a href="#" @click.prevent="loadComponent(m.name)">
						{{ m.title }}
					</a>
				</li>
			</ul>
		</nav>
	</header>
	<main>
		<component :is="component" />
	</main>
</template>

<script>
/* eslint-disable */

export default {
	data: () => {
		return {
			component: null,
			menu: [{
				name: 'Home',
				title: 'Accueil',
			}, {
				name: 'UserList',
				title: 'Liste des Utilisateurs',
			}]
		}
	},
	created() {
		this.loadComponent('Home')
	},
	methods: {
		async loadComponent(name) {
			try {
				const component = await import(`./pages/${name}.vue`)
				this.component = component.default
			} catch (error) {
				console.error(error)
			}
		}
	}
}
</script>

<style>
* {
	margin: 0;
	padding: 0;

	box-sizing: border-box;
	list-style-type: none;
	text-decoration: none;
}

main {
	display: flex;
	flex-direction: row;
	justify-content: center;
	align-items: center;

	margin-top: 50px;
	height: calc(100vh - 50px);

	overflow: hidden;
}

.navbar{
	position: fixed;
	top: 0;
	left: 0;
	right: 0;
	height: 50px;

	display: flex;
	justify-content: space-between;
	align-items: center;
}

.nav-menu {
	display: inline-block;
	margin: 0 15px;
}

</style>