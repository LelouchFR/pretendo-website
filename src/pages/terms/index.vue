<script setup lang="ts">
const { data: allTerms } = await useAsyncData('terms', () => queryCollection('terms').all());
</script>

<template>
  <div class="container">
    <h1>Terms</h1>
    <ul>
      <li
        v-for="terms in allTerms"
        :key="terms.id"
      >
        <a :href="terms.path">{{ terms.title }}</a>
      </li>
    </ul>
  </div>
</template>

<style>
.container {
	max-width: 1220px;
	margin: 100px auto;
}

ul li {
	color: var(--text-shade-1);
}

ul li a {
	color: var(--accent-shade-1);
	font-weight: bold;
	text-decoration: none;
}

ul li a:hover {
	text-decoration: underline;
}
</style>
