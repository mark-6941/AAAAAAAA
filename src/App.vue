<script setup>
import PolicyForm from './components/PolicyForm.vue'
</script>

<template>
  <main>
    <PolicyForm />
  </main>
</template>

<style scoped>
/*
 * 這裡可以保留或移除舊有的樣式，
 * 這些樣式主要影響舊的 header 和 logo。
 * 由於我們移除了這些內容，它們可能不再需要。
 */
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>