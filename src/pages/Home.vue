<template>
	<div class="content">
		<h3>Bienvenu.e.s sur votre site utilisateurs</h3>
		<p>{{ message }}</p>
	</div>
</template>

<script>
/* eslint-disable */
export default{
	name: "HomePage",
	data: () => {
		return {
			message: "Bienvenue, sur votre nouvelle plateforme Alumni"
		}
	}
}
</script>