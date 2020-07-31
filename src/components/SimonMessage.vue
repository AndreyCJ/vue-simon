<template>
  <div class="simon__message-container" :class="{'--hidden': !message}">
    <span class="simon__message-text" >{{ message }}</span>
  </div>
</template>

<script>
export default {
  props: {
    message: String,
  }
}
</script>

<style scoped>
.simon__message-text {
  font-size: 1.2rem;
}

.simon__message-container {
  display: block;
  margin-top: 20px;
  padding: 20px;
  background: #7FAFFB;
}

</style>