<template>
  <div id="app">
    <h1>Jogo da Forca</h1>
    <section v-if="view === 'start'" id="start">
      <Form
        v-if="step === 'word'"
        title="Defina a palavra"
        button="Próximo"
        :action="setWord"
      ></Form>
      <Form
        v-else
        title="Defina a dica"
        button="Iniciar Jogo"
        :action="setTip"
      ></Form>
    </section>
    <section v-else id="game">
      <game
        :error="error"
        :word="word"
        :tip="tip"
        :handleLetter="handleLetter"
        :step="step"
        :letters="letters"
        :play="play"
        :playAgain="playAgain"
      ></game>
    </section>
  </div>
</template>

<script>
import "./css/global.css";
import Form from "./components/Form.vue";
import Game from "./components/Game.vue";
export default {
  name: "App",
  components: { Form, Game },
  data() {
    return {
      view: "start",
      step: "word",
      word: "",
      tip: "",
      error: 0,
      letters: [],
    };
  },
  methods: {
    setWord(word) {
      this.word = word;
      this.step = "tip";
    },
    setTip(tip) {
      this.tip = tip;
      this.view = "game";
      this.step = "game";
    },
    handleLetter(letter) {
      return this.letters.find((x) => x.toLowerCase() == letter.toLowerCase());
    },
    play(letter) {
      this.letters.push(letter);

      this.handleError(letter);
    },
    handleError(letter) {
      if (this.word.toLowerCase().indexOf(letter.toLowerCase()) >= 0) {
        return this.handleHits();
      }

      this.error++;

      if (this.error === 6) {
        this.step = "died";
      }
    },
    handleHits() {
      let singleLetters = [...new Set(this.word.split(''))];
      console.log(singleLetters.length)
      console.log(this.letters.length)
      if (singleLetters.length === this.letters.length - this.error) {
        this.step = "winner";
      }
    },
    playAgain() {
       this.view = "start"
      this.step = "word"
      this.word = ""
      this.tip = ""
      this.error = 0
      this.letters = []
    }
  },
};
</script>

<style>
#app {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
