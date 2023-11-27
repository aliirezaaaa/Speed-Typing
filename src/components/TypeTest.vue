<template>
  <div class="main-wrapper">
    <div style="display: flex;align-items: flex-start;">
      <div class="q-pa-md" style="width: 90%;">
        <div style="display: flex;justify-content: space-between;">
          <div style="display: flex;width: 30%;color: white;">
            <h6 class="no-margin">Time(s):</h6>
            <q-range class="q-ml-xl" thumb-color="white" selection-color="white" v-model="timeModel" marker-labels
              :markers="10" step="10" :min="20" :max="90" />

          </div>
          <div style="display: flex;width: 30%; color: white;">
            <h6 class="no-margin">Words:</h6>
            <q-range class="q-ml-xl" thumb-color="white" selection-color="white" v-model="wordModel" marker-labels
              :markers="10" step="10" :min="20" :max="90" />
          </div>
        </div>
      </div>
    </div>

    <div class="parag ">
      <h6 style="margin: 0.5rem;padding: 1rem;">
        {{ paragraph }}
      </h6>
    </div>
    <div>
      <div style="display: flex;justify-content: space-between;">
        <h5 class="q-mx-xl q-mb-none" style="color: rgb(11, 218, 11);">time: {{ timeModel.max }}s</h5>
      </div>
      <q-input class="writingArea bg-blue-5" v-model="textareaModel" filled type="textarea" color="green-12"
        label="Start writing..." :disable="disable" />
    </div>

    <div style="display: flex;align-self: center;">
      <q-btn class="bg-green-6 q-mx-lg" style="align-self: center;" @click="finished = true, validation()">Finish</q-btn>
      <!-- <q-btn class="bg-green-6 q-mx-lg" style="align-self: center;:" @click="restart">Restart</q-btn> -->
    </div>
    <h5 :class="{ 'invisible': !timeOver && !finished, 'text-center': true, 'bg-green-6': true, 'q-mx-xl': true }"
      style="color: rgb(255, 255, 255);">accuracy: {{
        accuracy }}%
    </h5>
  </div>
</template>
<script>
import { ref, watch } from 'vue'
import { generate } from "random-words";

export default {
  setup() {

    const timeModel = ref({
      min: 20,
      max: 20
    })
    const wordModel = ref({
      min: 20,
      max: 20
    })
    let correctWords = 0;
    let accuracy = ref(0);
    let finished = ref(false)
    let timeOver = ref(false)
    let disable = ref(true)
    let textareaModel = ref('')
    let paragraph = ref('Select number of words by upper menu.')
    let allWords = ref([])

    function onTimeClick(t) {
      timeModel.value.max = t;
    }
    function onWordClick(w) {
      wordModel.value.max = w;
    }

    function validation() {
      disable.value = false
      let paragWords = paragraph.value.split(" ")
      let textareaWords = textareaModel.value.split(" ")
      for (let i = 0; i < paragWords.length; i++) {
        if (paragWords[i] == textareaWords[i]) {
          correctWords += 1
        }
      }
      accuracy.value = ((correctWords / (paragWords.length - 1)) * 100).toFixed(2)
    }

    watch(textareaModel, () => {
      if (textareaModel.value.length == 1) {
        setInterval(() => {
          if (timeModel.value.max > 0 && finished.value == false) {
            timeModel.value.max -= 1
          } else if (timeModel.value.max == 0) {
            timeOver.value = true
            disable.value = true
          }
        }, 1000);
      }
    })

    watch(timeOver, () => {
      if (timeOver.value == true) {
        validation()
      }
    })

    watch(wordModel, () => {
      allWords.value = generate(wordModel.value.max)
      paragraph.value = allWords.value.join(" ")
      disable.value = false
    })

    function restart() {
      correctWords = 0;
      accuracy.value = 0;
      wordModel.value = 0;
      disable.value = false;
      finished.value = false;
      timeOver.value = false;
      timeModel.value.max = 20;
      textareaModel.value = '';
    }

    return {
      onTimeClick,
      onWordClick,
      restart,
      validation,
      timeModel,
      finished,
      wordModel,
      textareaModel,
      paragraph,
      timeOver,
      accuracy,
      disable,
    }
  }
}
</script>
<style>
.main-wrapper {
  display: flex;
  flex-direction: column;
  margin: 0rem;
  padding: 0rem;

  background-color: #083466;
  background-image: url('../images/download.png');
}

.parag {
  display: flex;
  justify-content: center;
  color: white;
  background-color: rgba(74, 195, 243, 0.473);
  backdrop-filter: blur(5px);
  padding: 0rem;
  margin: 0rem;
  height: min-content;
}

.writingArea {
  display: flex;


  backdrop-filter: blur(5px);
  padding: 1rem;
  margin: 2rem;
  height: min-content;

}
</style>
