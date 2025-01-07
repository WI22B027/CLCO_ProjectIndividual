<template>
  <div id="app">
    <header>
      <h1>Cloud File Upload Tool</h1>
      <p>
        Ein einfacher Weg, Dateien hochzuladen, zu teilen und automatisch zu
        löschen.
      </p>
    </header>
    <main>
      <UploadSection />
    </main>
    <footer>
      <p>&copy; 2025 Cloud File Upload Tool</p>
    </footer>
  </div>
</template>

<script>
import UploadSection from './components/UploadSection.vue';

export default {
  name: 'App',
  components: {
    UploadSection,
  },
};
</script>

<style>
@import './assets/style.css';
</style>
