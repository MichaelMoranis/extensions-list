<script setup lang="ts">
import AreaExtensions from "./components/AreaExtensions.vue"
import { CardData } from "@types"



</script>

<template>
  <main>
    <section class="header">
      <div class="logo">
        <img class="logo-img" src="/assets/images/logo.svg" alt="logo">
      </div>
      <div class="icon-container">
        <img class="img-sun" src="/assets/images/icon-sun.svg" alt="icon-sun">
      </div>
    </section>
    <h1 class="list">
      Extension List
      <FilterButton />
    </h1>
    <AreaExtensions />
  </main>
</template>

<style scoped>
main {
  max-width: 1200px;
  margin: 1rem auto;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 2px;
  max-width: 83%;
  margin: 1rem auto;
  background-color: var(--neutral-700);
  border-radius: 20px;
}

.logo {
  margin: .25rem;
}

.logo-img {
  color: white;
}

.icon-container {
  margin: 6px;
  border-radius: 10px;
  background-color: var(--neutral-600);
}

.img-sun {
  padding: 12px;
}

.list {
  display: flex;
  align-items: center;
  justify-content: space-between;
  max-width: 83%;
  padding: 2px;
  margin: 1rem auto;
  color: var(--neutral-200);
}

.button-container {
  display: flex;
  justify-content: end;
  gap: 0.5rem;
}
</style>
