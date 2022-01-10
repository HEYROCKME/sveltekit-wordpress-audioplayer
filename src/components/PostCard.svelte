<script>
	export let post;
</script>

<article>
	<img class="feature-image bloglist" src={post.featuredImage.node.sourceUrl} alt="" srcset="" />
	<h2>
		<a href={`/blog${post.uri}`}>{post.title}</a>
	</h2>
	{post.uri}
	{@html post.excerpt}

	<a href={`/blog${post.uri}`}>read more...</a>
</article>

<style>
	.bloglist {
		width: 100%;
	}
</style>
