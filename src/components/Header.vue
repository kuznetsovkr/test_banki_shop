<template>
  <header class="header">
    <div class="wrapper">
      <button class="burger" @click="toggleMenu">
        <span :class="{ open: isMenuOpen }"></span>
        <span :class="{ open: isMenuOpen }"></span>
        <span :class="{ open: isMenuOpen }"></span>
      </button>
      <nav class="nav" :class="{ open: isMenuOpen }">
        <ul class="nav-links">
          <li v-for="link in links" :key="link.name">
            <a :href="link.href">{{ link.name }}</a>
          </li>
        </ul>
      </nav>
      <div class="search">
        <input
            type="text"
            v-model="searchQuery"
            @input="updateSearch"
            placeholder="Поиск по названию картины"
            class="search-input"
        />
        <button @click="handleSearch" class="search-button">Найти</button>
      </div>
    </div>
  </header>
</template>


<script>
export default {
  name: "HeaderComponent",
  data() {
    return {
      links: [
        { name: "Каталог", href: "#catalog" },
        { name: "Доставка", href: "#delivery" },
        { name: "Оплата", href: "#payment" },
        { name: "Контакты", href: "#contacts" },
        { name: "О компании", href: "#about" },
      ],
      searchQuery: "",
      isMenuOpen: false,
    };
  },
  methods: {
    updateSearch() {
      this.$emit("update-search", this.searchQuery);
    },
    handleSearch() {
      console.log("Поиск:", this.searchQuery);
    },
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen;
    },
  },
};
</script>


