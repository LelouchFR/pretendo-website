<script setup lang="ts">
const slug = useRoute().params.slug;
const { data: term } = await useAsyncData(`terms-${slug}`, () => {
	return queryCollection('terms').path(`/terms/${slug}`).first();
});

if (!term.value) {
	throw createError({ statusCode: 404, statusMessage: 'Page Not Found' });
}

useHead({
	title: `${term.value.title} | Pretendo Network Blog`,
	meta: [
		{ property: 'description', content: term.value.caption },
		{ property: 'og:title', content: `${term.value.title} | Pretendo Network Blog` },
		{ property: 'og:description', content: term.value.caption },
		{ property: 'og:type', content: 'website' },
		{ property: 'og:url', content: 'https://pretendo.network/' },
		{ property: 'og:image', content: term.value.cover_image },
		{ property: 'og:image:alt', content: 'Pretendo Network' },
		{ property: 'og:site_name', content: 'Pretendo Network' },
		{ name: 'twitter:url', content: 'https://pretendo.network/' },
		{ name: 'twitter:card', content: 'summary_large_image' },
		{ name: 'twitter:site', content: '@PretendoNetwork' },
		{ name: 'twitter:title', content: `${term.value.title} | Pretendo Network Blog` },
		{ name: 'twitter:description', content: term.value.caption },
		{ name: 'twitter:image', content: term.value.cover_image }
	]
});
</script>

<template>
  <div class="container">
    <article v-if="term">
      <h1>{{ term.title }}</h1>
      <h2>Last updated: {{ term.date }}</h2>

      <ContentRenderer :value="term" />
    </article>
  </div>
</template>

<style>
.container {
	max-width: 1220px;
	margin: 100px auto;
}

article {
	margin: 50px auto;
	padding: 60px;
	background-color: var(--bg-shade-0);
	border-radius: 10px;
}

article h1 {
	font-size: 32px;
}

article h1, article h2, article h3, article h4 {
	margin: 40px 0 10px 0;
}

article h1 a, article h2 a, article h3 a, article h4 a {
	color: var(--text-shade-3);
	text-decoration: none;
}

article p, article ul li, article ol li {
	color: var(--text-shade-1);
}

article * a:not(:where(article h1, article h2, article h3, article h4)) {
	color: var(--accent-shade-1);
	font-weight: bold;
	text-decoration: none;
}

article * a:not(:where(article h1, article h2, article h3, article h4)):hover {
	text-decoration: underline;
}

article ul li strong, article ol li strong, article p strong {
	color: var(--text-shade-3);
}

article table {
	border-radius: 4px;
	border-collapse: collapse;
	background-color: var(--bg-shade-3);
	margin-bottom: 30px;
	overflow: hidden;
	color: var(--text-shade-1);

}

article table thead tr th, article table tbody tr td {
	padding: 8px 12px;
	vertical-align: top;
}

article table thead tr th {
	color: var(--text-shade-3);
	background-color: var(--bg-shade-4);
}

article table tbody tr:nth-child(2n) td {
	background-color: var(--bg-shade-2);
}
</style>
