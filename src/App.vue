<script setup>
import { ref } from 'vue'

const userChoise = ref('')
const pcChoice = ref('')
const result = ref('')
const showModal = ref(false)
const handleChoise = (val) => {
  const options = [
    { sign: 'rock', src: '/images/rock.png' },
    { sign: 'paper', src: '/images/paper.png' },
    { sign: 'scissor', src: '/images/scissor.png' },
  ]
  userChoise.value = { sign: val, src: `/images/${val}.png` }
  pcChoice.value = options[Math.floor(Math.random() * 3)]
  if (
    (userChoise.value.sign === 'rock' && pcChoice.value.sign === 'paper') ||
    (userChoise.value.sign === 'scissor' && pcChoice.value.sign === 'rock') ||
    (userChoise.value.sign === 'paper' && pcChoice.value.sign === 'scissor')
  ) {
    result.value = 'You lost!'
  } else if (userChoise.value.sign === pcChoice.value.sign) {
    result.value = 'Match Draw!'
  } else {
    result.value = 'You Win!'
  }
  showModal.value = true
}

const restart = () => {
  userChoise.value = ''
  pcChoice.value = ''
  result.value = ''
}
</script>

<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <p>{{ result }}</p>
        <button @click="showModal = false">Close</button>
      </div>
    </div>
    <h1>Rock, Paper or Scissor Game</h1>
    <div class="container">
      <div class="icon-group">
        <p v-if="!userChoise" class="query-text">
          Choose from rock, paper or scissor.
        </p>
        <div v-if="userChoise" class="user-choice">
          <img :src="userChoise.src" :alt="userChoise.sign" />
        </div>
        <div v-if="pcChoice" class="pc-choice">
          <img :src="pcChoice.src" :alt="pcChoice.sign" />
        </div>
      </div>
      <div class="btn-group">
        <button @click="handleChoise('rock')" class="rock">Rock</button>
        <button @click="handleChoise('paper')" class="paper">Paper</button>
        <button @click="handleChoise('scissor')" class="scissor">
          Scissor
        </button>
        <button @click="restart" class="restart">Restart</button>
      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.container {
  width: 400px;
  height: 200px;
  border: 2px solid gray;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  border-radius: 4px;
  box-shadow: 1px 1px 1px rgba(0, 0, 0, 0.4);
}

.icon-group {
  display: flex;
  justify-content: space-between;
  width: 300px;
}
.btn-group {
  display: flex;
  justify-content: space-between;
  width: 350px;
}
button {
  padding: 5px 12px;
  font-size: 18px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  color: #fff;
  font-weight: bold;
}

button.restart {
  background-color: #e63946;
}

button.rock {
  background-color: #6c534e;
}

button.paper {
  background-color: #3b6ae3;
}

button.scissor {
  background-color: #580aff;
}

.icon-group p {
  text-align: center;
  font-size: 20px;
  font-style: oblique;
}

.overlay {
  width: 100%;
  height: 100%;
  position: absolute;
  background-color: rgba(0, 0, 0, 0.77);
  z-index: 100;
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal {
  width: 200px;
  height: 100px;
  background-color: white;
  padding: 10px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.modal button {
  background-color: #e63946;
}

.modal p {
  font-size: 20px;
  font-style: oblique;
}

h1 {
  letter-spacing: 0.8px;
  font-style: italic;
}
</style>
