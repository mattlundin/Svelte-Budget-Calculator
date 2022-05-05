<script>
	async function getUsers() {
		let userData = await fetch('https://api.github.com/users');
		let githubUsers = await userData.json();
		return githubUsers;
	}
</script>

<section>
	{#await getUsers()}
		<!-- Promise is pending -->
		<h1>Loading...</h1>
	{:then users}
		{#each users as user}
			<article class="user">
				<img src={user.avatar_url} alt={user.login} />
				<div class="user-info" />
				<h3>User: {user.login}</h3>
				<a href={user.html_url} class="btn-primary" target="_blank">
					github url
				</a>
			</article>
		{/each}
	{:catch error}
		<!-- Promise was rejected -->
		<p>Something went wrong : {error.message}</p>
	{/await}
</section>
