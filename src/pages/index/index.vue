<script setup lang="ts">
import routes from '~pages'
const list = routes.filter(item => item.name !== 'index').sort((a, b) => {
  const order1 = a.meta?.order as number || 0
  const order2 = b.meta?.order as number || 0
  return order1 - order2
})
console.log(routes)
</script>
<template>
  <div>
    <ul>
      <li v-for="item in list" :key="item.name">
        <router-link :to="item.path">{{ item.name }}</router-link>
      </li>
    </ul>
  </div>
</template>


<style scoped>
</style>
