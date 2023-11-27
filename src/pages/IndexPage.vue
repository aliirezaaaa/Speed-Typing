<template>
  <div class="super-wrapper">
    <div class="main-wrapper bg-transparent">
      <div class="intro-wrapper-div">
        <q-img class="q-ma-xl bg-transparent" src="src/images/moon.png" style="height: 200px; max-width: 200px">
        </q-img>
        <div style="display: flex;flex-direction: column">
          <h3 class="typed">Test your typing skill !</h3>
          <q-btn to="/typetest" style="width: 150px;" class="bg-white text-blue-10" label="Let's start">
          </q-btn>
        </div>
      </div>
    </div>

    <q-img src="src/images/clouds3.png">
      <q-img class="bg-transparent" src="src/images/clouds2.png">
        <q-img class="bg-transparent" src="src/images/clouds1.png"></q-img>
      </q-img>
    </q-img>
  </div>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'IndexPage'
})
</script>

<style>
.super-wrapper {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 92.5vh;
  background-color: #083466;
  background-image: url('../images/download.png');
}

.bg-brand {
  background: #083669 !important;
}

.main-wrapper {
  margin-top: 5rem;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
}

.intro-wrapper-div {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: transparent;
  width: 70%;
}

.typed {
  overflow: hidden;
  white-space: nowrap;
  border-right: 2px solid;
  color: white;
  width: 0;
  animation: typing 1.5s steps(30, end) forwards, blinking 1s infinite;
}

@keyframes typing {
  from {
    width: 0
  }

  to {
    width: 100%
  }
}

@keyframes blinking {
  0% {
    border-right-color: transparent
  }

  50% {
    border-right-color: rgb(255, 255, 255)
  }

  100% {
    border-right-color: transparent
  }
}
</style>
