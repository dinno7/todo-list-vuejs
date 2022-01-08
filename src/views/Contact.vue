<template>
  <div class="contact">
    <transition name="fade-top" appear>
      <h1>Contact</h1>
    </transition>
    <transition-group
      appear
      tag="ul"
      @enter="contactEnter"
      @before-enter="contactBeforeEnter"
    >
      <li
        class="info-box"
        v-for="(icon, index) in icons"
        :key="icon.name"
        :data-index="index"
      >
        <a :href="icon.link">
          <!-- <span class="material-icons" style="font-size: 30px;">{{
            icon.name
          }}</span> -->
          <i :class="icon.name" style="font-size: 30px;font-weight: 400;"></i>
          <div style="font-size: 16px;">{{ icon.text }}</div>
        </a>
      </li>
    </transition-group>
  </div>
</template>

<script>
import { ref } from "vue";
import gsap from "gsap";

export default {
  setup() {
    const icons = ref([
      {
        // name: "alternate_email",
        //         "local_phone"
        // "local_post_office"
        // "local_fire_department"
        name: "fas fa-at",
        text: "Email",
        link: "mailto: t.dinno7@gmail.com?subject=Vue todolist feedback",
      },
      {
        name: "fab fa-instagram",
        text: "Instagram",
        link: "https://instagram.com/DinnoLearn",
      },
      {
        name: "fab fa-telegram-plane",
        text: "Telegram",
        link: "https:t.me/DinnoLearn",
      },
      { name: "fas fa-phone", text: "Phone", link: "#" },
    ]);

    const contactBeforeEnter = (el) => {
      el.style.transform = "translateY(100px)";
      el.style.opacity = 0;
    };
    const contactEnter = (el, done) => {
      gsap.to(el, {
        y: 0,
        opacity: 1,
        duration: 0.8,
        delay: el.dataset.index / 5,
        ease: "sine.out",
        onComplete: done,
      });
    };

    return { icons, contactEnter, contactBeforeEnter };
  },
};
</script>

<style>
.contact ul {
  padding: 0;
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 20px;
  max-width: 400px;
  margin: 60px auto;
}
.contact li {
  list-style-type: none;
  background: var(--white);
  padding: 30px;
  border-radius: 10px;
  box-shadow: 1px 3px 5px rgba(0, 0, 0, 0.1);
  cursor: pointer;
  line-height: 1.5em;
  transition: all 0.2s ease;
}
.contact li:hover {
  transform: scale(1.2) !important;
  background: var(--green);
  box-shadow: 1px 3px 5px 3px rgba(0, 0, 0, 0.1);
}
.info-box a {
  text-decoration: none;
  color: var(--gray);
}
.info-box a > * {
  transition: all 0.2s ease;
}
.info-box:hover > a > * {
  transform: scale(1.2) !important;
  color: #fff;
}
/* ---------------------------------- */
</style>
