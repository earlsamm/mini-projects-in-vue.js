<script setup>
import { ref } from 'vue'

let theme = ref('light')
let pages = ref([
  { link: { name: 'Home', url: '#' } },
  { link: { name: 'About', url: '#' } },
  { link: { name: 'Services', url: '#' } },
  { link: { name: 'Contact', url: '#' } },
])
let activePage = ref(0)

let changeTheme = () => {
  theme.value = theme.value === 'light' ? 'dark' : 'light'
}

let navLinkClick = (index) => {
  activePage.value = index
}
</script>
<template>
  <nav
    class=""
    :class="[`navbar-${theme}`, `bg-${theme}`, 'navbar', 'navbar-expand-lg']"
    id="navbar"
  >
    <div class="container-fluid">
      <a class="navbar-brand" href="#">VueApp</a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li v-for="(page, index) in pages" class="nav-item" :key="index">
            <a
              class="nav-link"
              :class="{ active: activePage == index }"
              aria-current="page"
              :href="page.link.url"
              :title="`This linq goes tp ${page.link.name}`"
              v-on:click.prevent="navLinkClick(index)"
              >{{ page.link.name }}
            </a>
          </li>
        </ul>
        <form class="d-flex" role="search">
          <input class="form-control" type="search" placeholder="Search" aria-label="Search" />
          <button class="btn btn-outline-success" @click.prevent="changeTheme()">Theme</button>
        </form>
      </div>
    </div>
  </nav>
</template>

<style scoped></style>
