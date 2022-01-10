<script context="module">
	import { APIurl } from '../../Url';

	const query = `
  query getPosts {
    posts {
      nodes {
        databaseId
		link
        uri
        title
        excerpt
        date
        featuredImage {
          node {
            sourceUrl
            altText
            mediaDetails {
              width
              height
            }
          }
        } 
      }
    }
  }
  `;

	export async function load({ fetch }) {
		const response = await fetch(APIurl, {
			method: 'POST',
			headers: {
				'Content-Type': 'application/json'
			},
			body: JSON.stringify({ query })
		}); //end of response

		if (response.ok) {
			const resObj = await response.json();
			const posts = resObj.data.posts.nodes;
			console.log(resObj);

			return {
				props: {
					posts
				}
			};
		}

		return {
			status: response.status,
			error: new Error(`Could not load `)
		};
	}
</script>

<script>
	import PostCard from '../../components/PostCard.svelte';
	export let posts;
</script>

<h1>Blog</h1>

{#if posts}
	<ul>
		{#each posts as post}
			<li>
				<PostCard {post} />
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
