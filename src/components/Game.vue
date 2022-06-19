<template>
  <div class="game">
    <div class="forca">
      <img
        :src="`https://raw.githubusercontent.com/william-costa/wdev-hangman-game-resources/master/images/hangman/${error}.svg`"
        alt=""
      />
    </div>
    <div class="word">
      <div class="letters">
        <div class="word-letter" v-for="(letter, key) in word" :key="key">
          {{ handleLetter(letter) || step === "died" ? letter : "" }}
        </div>
      </div>
      <div>{{ tip }}</div>
      <div v-if="step === 'game'" class="keyboard">
        <button
          class="keyboard-button"
          v-for="(letter, key) in 'abcdefghijklmnopqrstuvwxyz'"
          :key="key"
          :disabled="handleLetter(letter)"
          @click="play(letter)"
        >
          {{ letter }}
        </button>
      </div>
    </div>
    <div v-if="step === 'died' || step === 'winner'">
      <div v-if="step === 'died'" :class="`message ${step}`">
        Não foi dessa vez :(
      </div>
      <div v-if="step === 'winner'" :class="`message ${step}`">Parbéns :)</div>
      <button class="play-again" @click="playAgain()">
        jogar novamente
      </button>
      <div></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Game",
  component: {},
  props: [
    "error",
    "word",
    "tip",
    "handleLetter",
    "step",
    "letters",
    "play",
    "playAgain",
  ],
};
</script>

<style>
.game {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}
.forca img {
  height: 100px;
}
.word {
  text-transform: uppercase;
  display: flex;
  flex-direction: column;
  text-align: center;
  align-items: center;
}
.letters {
  display: flex;
  margin-bottom: 20px;
}

.word-letter {
  height: 30px;
  width: 30px;
  margin: 0px 5px;
  border-bottom: 1px solid var(--color-text-light);
  display: flex;
  justify-content: center;
  align-items: center;
}

.keyboard {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  max-width: 725px;
  margin-top: 20px;
  text-transform: uppercase;
}
.keyboard-button {
  margin: 5px;
}

.message {
  margin: 20px 0px;
  font-size: 24px;
  font-weight: bold;
}

.died {
  color: var(--color-text-error);
}
.winner {
  color: var(--color-text-success);
}
</style>
