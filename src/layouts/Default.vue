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
  justify-content: center;
  width: 960px;
  margin: 0 auto;
  height: 100vh;
  padding-left: 20px;
  padding-right: 20px;
}

.layout > * {
  flex: 1;
}

.content {
  position: relative;
  flex: 5;
  padding-top: 55px;
  background: #fff;
  width: 100%;
  border-radius: 4px;
  overflow: hidden;
}
</style>
