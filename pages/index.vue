<template>
	<div class="container">
		<div>
			<Logo />
			<h1 class="title">three-wiki</h1>
			<div class="links">
				<a
					href="/blogs"
					
					rel="noopener noreferrer"
					class="button--green"
				>
					Blogs
				</a>
				<a
					href="/admin"
					
					rel="noopener noreferrer"
					class="button--grey"
				>
					Admin
				</a>
			</div>
		</div>
	</div>
</template>

<script>
export default {
  mounted() {
	netlifyIdentity.on('init', user => console.log('init', user));
	netlifyIdentity.on('login', user => console.log('login', user));
	netlifyIdentity.on('logout', () => console.log('Logged out'));
	netlifyIdentity.on('error', err => console.error('Error', err));
	netlifyIdentity.on('open', () => console.log('Widget opened'));
	netlifyIdentity.on('close', () => console.log('Widget closed'));
  },
  async asyncData({ $content, params, error }) {
    let post;
    try {
      post = await $content("blog", params.slug).fetch();
      // OR const article = await $content(`articles/${params.slug}`).fetch()
    } catch (e) {
      error({ message: "Blog Post not found" });
    }

    return { post,     };
  },
};
</script>

<style>
.container {
	margin: 0 auto;
	min-height: 100vh;
	display: flex;
	justify-content: center;
	align-items: center;
	text-align: center;
}

.title {
	font-family: 'Quicksand', 'Source Sans Pro', -apple-system,
		BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial,
		sans-serif;
	display: block;
	font-weight: 300;
	font-size: 100px;
	color: #35495e;
	letter-spacing: 1px;
}

.subtitle {
	font-weight: 300;
	font-size: 42px;
	color: #526488;
	word-spacing: 5px;
	padding-bottom: 15px;
}

.links {
	padding-top: 15px;
}
</style>
