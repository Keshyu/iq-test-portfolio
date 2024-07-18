<script setup lang="ts">
import { Teleport, ref } from 'vue'
import { RouterLink, RouterView } from 'vue-router'

const sidebarOpen = ref<boolean>(false)

const navLinks: { name: string, url: string }[] = [
  { url: '/', name: 'Главная' },
  { url: '/', name: 'Информация о тесте' },
  { url: '/quiz', name: 'пройти тест' },
]

// TODO: Second nav link should lead somewhere??
</script>

<template>
    <header>
      <button id="menu-btn" @click="sidebarOpen = true">
        <img src="./assets/menu.png" />
      </button>

      <div id="navbar-title" />

      <Teleport to="body">
        <div id="sidebar" v-if="sidebarOpen">
          <button id="close-sidebar" @click="sidebarOpen = false">
            <img src="@/assets/cross.svg" />
          </button>
          <nav>
            <RouterLink
              v-for="{ url, name } in navLinks"
              :to="url" @click="sidebarOpen = false"
            >
              {{ name }}
            </RouterLink>
          </nav>
        </div>
      </Teleport>
    </header>

    <RouterView />
</template>

<style scoped>
header {
  box-shadow: 0 4px 4px rgb(0 0 0 / 0.25);
  background-color: #181818;
  position: sticky;
  top: 0;
  width: 100%;
  height: var(--navbar-height);
  z-index: 2;
  display: flex;
}

#menu-btn {
  margin: 1rem;
}

#menu-btn img {
  display: block;
}

#navbar-title {
  width: 100%;
  height: 100%;
  overflow: hidden;
}

#sidebar {
  background-color: #181818;
  box-shadow: 4px 0 4px rgb(0 0 0 / 0.25);

  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  z-index: 3;
  width: 100%;
  max-width: 40ch;

  display: flex;
  flex-direction: column;
  row-gap: 2rem;
}

#sidebar nav {
  display: flex;
  flex-direction: column;
  row-gap: 1.5rem;
  
  padding-left: 2rem;
  padding-right: 2rem;

  font-family: Roboto, sans-serif;
  font-size: 16px;
  line-height: 1.2em;
}

#sidebar nav a {
  appearance: none;
  color: inherit;
  text-decoration: none;
  text-transform: uppercase;
  font-weight: 300;
}

#sidebar nav a:hover {
  color: var(--accent);
}

#close-sidebar {
  align-self: end;
  margin: 1rem;
  width: 28px;
  height: 28px;
}

#close-sidebar img {
  display: block;
}
</style>
