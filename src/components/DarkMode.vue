<template>
  <div class="darkmode-btn">
    <button class="dark-btn" ref="darkBtn" @click="setDarkMode">
      <i class="far fa-moon" v-show="darkMode"></i>
      <i class="far fa-sun" v-show="!darkMode"></i>
    </button>
  </div>
</template>

<script>
import { ref } from "@vue/reactivity";
export default {
  name: "DarkMode",
  setup() {
    const darkBtn = ref(null);
    const darkMode = ref(false);

    const setDarkMode = () => {
      darkMode.value = document.body.classList.contains("dark");
      if (darkMode.value) {
        document.body.classList.remove("dark");
        darkBtn.value.style = "background:var(--gray);color:var(--white)";
      } else {
        document.body.classList.add("dark");
        darkBtn.value.style = "background:var(--white);color:var(--gray)";
      }
    };

    return { darkMode, darkBtn, setDarkMode };
  },
};
</script>

<style>
.dark-btn {
  cursor: pointer;
  border: 0;
  outline: none;
  padding: 9px;
  border-radius: 10px;
  background: var(--gray);
  color: var(--white);
  font-weight: 500;
  font-size: 1rem;
  position: absolute;
  top: 10px;
  right: 10px;
  transition: all 0.4s ease;
}
.dark-btn:hover,
.dark-btn:focus {
  opacity: 0.8;
}
</style>
