<template>
  <div id="nav">
    <DarkMode />
    <router-link to="/">Home</router-link>
    <router-link to="/about">About</router-link>
    <router-link to="/contact">Contact</router-link>
  </div>
  <router-view v-slot="{ Component }">
    <transition name="route" mode="out-in">
      <component :is="Component"></component>
    </transition>
  </router-view>
</template>

<script>
import DarkMode from "@/components/DarkMode.vue";
export default {
  components: { DarkMode },
};
</script>

<style>
:root {
  --green: #42b983;
  --red: rgb(226, 34, 34);
  --gray: #2c3e50;
  --white: #fff;
  --black: #292929;
}
body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: var(--gray);
  margin: 0;
  background: #f2f2f2;
  transition: background 0.5s ease;
}
a:not(:first-child) {
  margin-left: 10px;
}
a:not(:last-child)::after {
  content: "|";
  color: black;
  margin-left: 10px;
  position: absolute;
}
.container {
  width: calc(100vw - 100px);
  margin: 0 auto;
  padding-top: 20px;
}
#nav {
  padding: 30px;
}
#nav a {
  font-weight: bold;
  color: var(--gray);
  text-decoration: none;
  padding: 7px;
  text-align: center;
  border-radius: 7px;
  transition: background 0.5s ease, color 0.2s ease;
}
#nav a.router-link-exact-active,
#nav a:hover {
  color: #fff;
  background: var(--green);
}

/* ----------------Route transition: */
.route-enter-from,
.route-leave-to {
  opacity: 0;
  transform: translateX(-100px);
}
.route-enter-active,
.route-leave-active {
  transition: all 0.5s;
}
/* ------------ */
.fade-top-enter-from {
  opacity: 0;
  transform: translateY(-100px);
}
.fade-top-enter-active {
  transition: all 0.5s ease;
}
</style>
