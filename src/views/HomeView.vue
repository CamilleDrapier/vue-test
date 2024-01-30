<script setup lang="ts">
import { useRouteHelpers } from '@/components/useRouteHelpers';
import { onUnmounted, ref, watch } from 'vue';
import { useRoute, useRouter } from 'vue-router';

const { isHome } = useRouteHelpers();
const route = useRoute();

const nb = ref(0);

watch(
  route,
  () => {
    console.log('watch - isHome', isHome.value);
    if (!nb.value) {
      nb.value = 1;
      useRouter().push({ name: 'home', params: { nb:1 } });
    }
  },
);

onUnmounted(() => {
  console.log('Unmounted Home - isHome:', isHome.value);
  if(!isHome.value) console.log('To the unknown~');
})
</script>

<template>
    <div class="home">
    <h1>This is a home page</h1>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .home {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
