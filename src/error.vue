<script setup lang="ts">
import type { NuxtError } from '#app';

const props = defineProps({
	error: {
		type: Object as () => NuxtError,
		required: true
	}
});

// TODO: Add multiple Customized Error messages
const message = computed(() => {
	switch (props.error?.statusCode) {
		case 404:
			return 'Oops! We could not find this page.';
		default:
			return 'Oops! We could not find this page.';
	}
});

</script>

<template>
  <div id="root">
    <Navbar />

    <div class="wrapper">
      <div>
        <h1 class="status">
          {{ error?.statusCode }}
        </h1>
        <p class="status__message">
          {{ message }}
        </p>
      </div>
      <img
        class="shocked-bandwidth"
        src="/assets/images/shockedbandwidth.svg"
        alt="shocked bandwidth"
      >
      <Footer />
    </div>
  </div>
</template>

<style scoped lang="scss">

div.wrapper {
	margin-top: 85.76px;
	display: flex;
	flex-direction: column;
	justify-content: space-between;
	height: 100%;

	img.shocked-bandwidth {
		display: block;
		width: 234.95px;
		margin: 70px auto 0 auto;
	}
}

h1.status {
	text-align: center;
	font-size: 8rem;
	color: var(--text-shade-1);
	margin: 0;
	margin-top: 25px;
}

p.status__message {
	text-align: center;
	font-size: 1.7rem;
	color: var(--text-shade-1);
	margin: 0;
}

footer {
	margin-top: 0 !important;
}
</style>
