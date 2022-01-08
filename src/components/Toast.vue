<template>
  <div class="toast-wrapper">
    <div class="toast">
      You must enter a value for the todo
    </div>
  </div>
</template>

<style scope>
.toast-wrapper {
  position: fixed;
  width: 93%;
  top: 20px;
}
.toast {
  padding: 20px;
  color: white;
  background: #ff0062;
  border-radius: 10px;
  box-shadow: 1px 3px 5px rgba(0, 0, 0, 0.2);
  max-width: 400px;
  margin: 0 auto;
}
@media only screen and (max-width: 768px) {
  .toast-wrapper {
    width: 79%;
  }
}
</style>
