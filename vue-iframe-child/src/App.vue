<template>
  <RouterView />
</template>
<script setup>
import { RouterView } from 'vue-router'
import { onMounted } from 'vue'
onMounted(() => {
  if (location.search) {
    const queryString = location.search.slice(1)
    const params = queryString.split('&').reduce((acc, cur) => {
      const [key, value] = cur.split('=')
      acc[key] = value
      return acc
    }, {})

    // document.referrer 이전 페이지... 그래서 여러 페이지 왔다갔다 하는 경우 못 찾음
    // document.location.ancestorOrigins[0] 이전 페이지 array로 나옴 0번째 최초 도메인
    window.parent.postMessage({ queryString: JSON.stringify(params) }, document.location.ancestorOrigins[0])
  }
})
</script>
<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
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

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
