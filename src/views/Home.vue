<template>
  <div class="home">
    <transition name="toast">
      <Toast v-if="showToast" @click="showToast = false" />
    </transition>
    <Todos @badValue="triggerToast" @todo-added="showLog" />
  </div>
</template>

<script>
import { ref } from "vue";
import Toast from "../components/Toast";
import Todos from "../components/Todos";

export default {
  components: { Toast, Todos },
  setup() {
    const showToast = ref(false);
    const addLog = ref(false);

    const triggerToast = () => {
      showToast.value = true;
      setTimeout(() => (showToast.value = false), 3000);
    };
    const showLog = () => {
      addLog.value = true;
      setTimeout(() => {
        addLog.value = false;
      }, 3000);
    };

    return { showToast, triggerToast, addLog, showLog };
  },
};
</script>

<style>
.toast-enter-active {
  animation: wapp 0.5s ease;
}

@keyframes wapp {
  0% {
    opacity: 0;
    transform: translateY(-100px);
  }
  50% {
    opacity: 1;
    transform: translateY(0);
  }
  60% {
    transform: translateX(-8px);
  }
  70% {
    transform: translateX(8px);
  }
  80% {
    transform: translateX(-4px);
  }
  90% {
    transform: translateX(4px);
  }
  100% {
    transform: translateX(0);
  }
}
.toast-leave-to {
  opacity: 0;
  transform: translateY(-100px);
}
.toast-leave-active {
  transition: all 0.5s ease;
}
</style>
