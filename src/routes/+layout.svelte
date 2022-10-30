<script>
	import css from '$lib/app.css';
	import bg from '$lib/pokemon-bg.jpg';
</script>

<body style="background:url({bg}); background-size: cover;">
	<slot />
</body>

<style>
	body {
		height: 100vh;
	}
</style>
