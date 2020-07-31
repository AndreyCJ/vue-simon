<template>
<div class="simon__controls">
  <div class="simon__info">
    <h2>Раунд: {{ score }}</h2>
    <button @click="$emit('changeGameState')" class="simon__start">Старт</button>
  </div>
  <div class="simon__options">
    <h2>Уровень сложности:</h2>
    <div class="simon__option">
      <label>
        <input
          @change="$emit('update:childDiff', childDiff)"
          v-model="childDiff"
          value="easy"
          type="radio"
        >
        Легкий
      </label>
    </div>
    <div class="simon__option">
      <label>
        <input
          @change="$emit('update:childDiff', childDiff)"
          v-model="childDiff"
          value="medium"
          type="radio"
        >
        Средний
      </label>
    </div>
    <div class="simon__option">
      <label>
        <input
          @change="$emit('update:childDiff', childDiff)"
          v-model="childDiff"
          value="hard"
          type="radio"
        >
        Сложный
      </label>
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: 'SimonControls',
  data() {
    return {
      childDiff: 'easy'
    }
  },
  props: {
    score: Number
  }
}
</script>

<style scoped>
.simon__options {
  margin-left: 30px;
}

.simon__info {
  margin-left: 30px;
}
.simon__controls {
  color: #333;
  margin-top: 40px;
  display: flex;
}

.simon__controls h2 {
  font-size: 1.6rem;
  margin-bottom: 10px;
}

.simon__option label {
  font-size: 1.3rem;
  cursor: pointer;
}

.simon__option label>input {
  margin-right: 10px;
}

.simon__start {
  font-size: 1.5rem;
  padding: 7px 25px;
  border: none;
  background: #3E89DD;
  border-radius: 10px;
  color: #f4f4f4;
  cursor: pointer;
  outline: none;
}

.simon__start:hover {
  background: #5fa3f1;
}
</style>