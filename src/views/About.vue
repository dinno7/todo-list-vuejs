<template>
  <div class="about">
    <transition appear @before-enter="aboutBeforeEnter" @enter="aboutEnter">
      <h1>About</h1>
    </transition>
    <div class="texts">

    <ul>
      <li>
        <p>
          I did not make all this todo list's <strong>CSS codes</strong> i just
          developed some
          <strong>
            <a href="https://vuejs.org/v2/api/#transition" target="_blank">Transition</a>
          </strong>
          and
          <strong
            ><a href="https://vuejs.org/v2/api/#transition" target="_blank"
              >Animation</a
            ></strong
          >
          by built-in
          <strong><a href="https://vuejs.org" target="_blank">Vue js</a></strong> component and
          <strong
            ><a href="https://greensock.com/gsap/" target="_blank"
              >GSAP libarery</a
            > </strong
          >. also i added some <strong>CSS codes</strong> and
          <strong>Features</strong> to this project.
        </p>
      </li>
      <li>
        <p>
          I made it more usfull by adding your todos to
          <strong>Local storage</strong> in your browser.when you add new todo
          it is save automaticlly in Local storage of your browser and it means
          that your todos will save even if you refresh the page.
        </p>
      </li>
      <li>
        <p>Something that used in this project:
          <ul style="display:grid;grid-template-columns:repeat(2,1fr)">
            <li style="list-style-type:square"><p><strong>Vue js v3</strong></p></li>
            <li style="list-style-type:square"><p><strong>Vue router</strong></p></li>
            <li style="list-style-type:square"><p><strong>Gsap</strong></p></li>
            <li style="list-style-type:square"><p><strong>Local storage</strong></p></li>
          </ul>
        </p>
      </li>
    </ul>
    <i style="font-size: 15px;float:left">--Dinno</i>
    </div>
  </div>
</template>

<script>
import gsap from "gsap";

export default {
  setup() {
    const aboutBeforeEnter = (el) => {
      el.style.opacity = 0;
      el.style.transform = "translateY(-150px)";
    };
    const aboutEnter = (el) => {
      gsap.to(el, {
        opacity: 1,
        y: 0,
        duration: 1,
        ease: "bounce.out",
      });
    };

    return { aboutBeforeEnter, aboutEnter };
  },
};
</script>

<style scoped>
.about {
  max-width: 600px;
  margin: 20px auto;
}
.about p {
  text-align: justify;
  font-weight: 500;
  font-size: 18px;
  color: rgba(0, 0, 0, 0.836);
}
strong a {
  text-decoration: none;
  color: #339267;
}
strong a:hover {
  color: var(--green);
}
@media only screen and (max-width: 768px) {
.texts ul {
    transform: translateX(-6%);
  }
}
</style>
