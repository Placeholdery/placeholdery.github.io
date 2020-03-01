<template>
  <div class="layout">
    <app-header></app-header>
    <section class="content">
      <slot />
    </section>
    <app-footer></app-footer>
  </div>
</template>

<script>
import Header from "../components/Header.vue";
import Footer from "../components/Footer.vue";

export default {
  components: {
    AppHeader: Header,
    AppFooter: Footer
  }
};
</script>

<style>
body {
  font-family: -apple-system, system-ui, BlinkMacSystemFont, "Segoe UI", Roboto,
    "Helvetica Neue", Arial, sans-serif;
  margin: 0;
  padding: 0;
  line-height: 1.5;
}

.layout {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  width: 960px;
  max-height: 100vh;
  margin: 0 auto;
  padding-left: 20px;
  padding-right: 20px;
}

.content {
  flex: 1;
  background: #fff;
  padding: 45px;
  border-radius: 4px;
  overflow-y: auto;
}
</style>
