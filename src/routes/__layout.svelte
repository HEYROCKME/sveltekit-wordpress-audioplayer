<script context="module">
	import '../layout.css';
	import PodcastPlayer from '../components/PodcastPlayer.svelte';
</script>

<PodcastPlayer />
<main>
	<slot />
</main>

<style>
	main {
		padding: 2em;
		max-width: 800px;
		margin: 0 auto 12em;
	}
</style>
