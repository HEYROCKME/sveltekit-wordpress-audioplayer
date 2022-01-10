<script context="module">
	export async function load({ fetch }) {
		let url;
		const response = await fetch(import.meta.env.VITE_PUBLIC_WORDPRESS_API_URL, {
			method: 'POST',
			headers: {
				'Content-type': 'application/json'
			},
			body: JSON.stringify({ fetch })
		}); //end of response

		if (response.ok) {
			const resObj = await response.json();
			const posts = resObj.data.posts.nodes;

			return {
				props: {
					posts
				}
			};
		}

		return {
			status: response.status,
			error: new Error(`Could not load ${url}`)
		};
	}
</script>

<script>
	import Postcard from '../../components/PostCard.svelte';
	let posts;
</script>

<h1>Blog</h1>

{#if posts}
	<ul>
		{#each posts as post}
			<li>
				<p>{post.title}</p>
				>
			</li>
		{/each}
	</ul>
{:else}
	<p>No Posts found</p>
{/if}

<style>
	ul {
		list-style: none;
		padding: 0;
	}
	ul li + li {
		margin-top: 2rem;
	}
</style>
