<script setup lang="ts">
import { ref, onMounted, watch } from 'vue';
import { Theme } from './ThemeModel';

const theme = ref < Theme > (0);

const toggleTheme = () => {
  theme.value = theme.value === Theme.light ? Theme.dark : Theme.light;
};


watch(theme, (newTheme) => {

  const key = Object.keys(Theme).filter((key) => isNaN(Number(key)))[newTheme];
  document.documentElement.setAttribute('data-theme', key);
}, { immediate: true });


onMounted(() => {
  const savedTheme = localStorage.getItem('theme') as string;
  if (savedTheme) {

    theme.value = Theme[savedTheme];
  } else {
    theme.value = Theme.light;
  }
});


watch(theme, (newTheme) => {
  localStorage.setItem('theme', Theme[newTheme]);
});
</script>

<template>
  <div class="container">
    <h1>Theme Switcher</h1>
    <button v-on:click="toggleTheme">
      Switch to {{ theme === Theme.light ? 'DARK' : 'LIGHT' }} Theme
    </button>


    <div class="content-box">
      <h2>Welcome!</h2>
      <p>Lorem Ipsum is simply dummy text of the printing and typesetting industry.
        Lorem Ipsum has been the industry's standard dummy text ever since the 1500s,
        when an unknown printer took a galley of type and scrambled it to make a type specimen book.
        It has survived not only five centuries, but also the leap into electronic typesetting,
        remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing
        Lorem Ipsum passages,
        and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.</p>

      <ul>
        <li>Item 1</li>
        <li>Item 2</li>
        <li>Item 3</li>
      </ul>
    </div>
  </div>
</template>
