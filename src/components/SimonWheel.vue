<template>
  <div class="simon__container">
    <div class="simon__row">
      <div class="simon__box simon__box--red"
        @click="$emit('boxClick', 1)"
        :class="{ active: isBoxOneActive, '.no-pointer': !userTurn }"
      ></div>
      <div
        class="simon__box simon__box--blue"
        @click="$emit('boxClick', 2)"
        :class="{ active: isBoxTwoActive }"
      ></div>
    </div>
    <div class="simon__row">
      <div
        class="simon__box simon__box--yellow"
        @click="$emit('boxClick', 3)"
        :class="{ active: isBoxThreeActive }"
      ></div>
      <div
        class="simon__box simon__box--green"
        @click="$emit('boxClick', 4)"
        :class="{ active: isBoxFourActive }"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SimonWheel',
  props: {
    isBoxOneActive: Boolean,
    isBoxTwoActive: Boolean,
    isBoxThreeActive: Boolean,
    isBoxFourActive: Boolean,
    userTurn: Boolean
  }
}
</script>

<style scoped>
.simon__container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  height: 100%;
  width: 100%;
}

.simon__row {
  position: relative;
  display: flex;
}

.simon__box {
  width: 150px;
  height: 150px;
  font-size: 64px;
  text-align: center;
  box-shadow: 2px 4px 8px #cccccc;
  cursor: default !important;
  border: none;
  outline: none;
}

.simon__box--red {
  background-color: #FB7F7F;
  border-radius: 100% 0 0 0;
}

.simon__box--blue {
  background-color: #7FAFFB;
  border-radius: 0 100% 0 0;
}

.simon__box--green {
  background-color: #89CF5E;
  border-radius: 0 0 100% 0;
}

.simon__box--yellow {
  background-color: #FBE27F;
  border-radius: 0 0 0 100%;
}

.active {
  background-color: #00000027;
  pointer-events: none;
}
</style>