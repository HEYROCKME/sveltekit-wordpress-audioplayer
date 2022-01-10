<script context="module">
	import { APIurl } from '../../Url';
	export const prerender = true;
	const query = `getPostBySlug($slug: ID!) {
  post(id: $slug, idType: SLUG) {
    date
    title
    content
    author {
      node {
        name
      }
    }
    categories {
      nodes {
        name
      }
    }
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
}`;

	export async function load({ url, params, fetch }) {
		const response = await fetch(APIurl, {
			method: 'POST',
			headers: {
				'Content-Type': ' application/json'
			},
			body: JSON.stringify({
				query,
				variables: {
					slug: params.slug
				}
			})
		});

		if (response.ok) {
			const resObj = await response.json();
			const { post } = resObj.data;
			console.log(resObj);

			return {
				props: {
					post
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
	export let post;
	const formatDate = (date) => new Date(date).toLocaleDateString();
	const categories = post.categories?.nodes?.map((category) => category.name) ?? [];
</script>

<a href="/blog" class="blog-link">&#8592;Blog</a>
