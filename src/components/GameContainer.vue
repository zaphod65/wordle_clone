<template>
  <div class="hello">
    <h1>Not-Wordle</h1>
    <div class="center">
      <GuessContainer
        :guess="guesses[guessAttempt]"
        :actualWord="word"
        v-for="guessAttempt in maxGuesses"
        :key="guessAttempt"
      />
      <input placeholder="GUESS" v-on:keyup.enter="addGuess" :disabled="gameOver">
    </div>
  </div>
</template>

<script>
import GuessContainer from './GuessContainer';

export default {
  name: 'GameContainer',
  components: {
    GuessContainer,
  },
  data: function () {
    return {
      guesses: [
      ],
      currentGuess: 1,
      gameWon: false,
      gameOver: false,
      word: 'FOUND',
      maxGuesses: 6,
    };
  },
  methods: {
    addGuess: function(event) {
      const guess = event.target.value.toUpperCase();

      if (guess === this.word) {
        this.gameWon = true;
        this.gameOver = true;
      }

      this.guesses[this.currentGuess] = guess;
      event.target.value = "";
      this.currentGuess++;
    }
  }
}
</script>

<style scoped>
h1 {
  color: #fff;
}

h3 {
  margin: 40px 0 0;
}

div.center {
  margin:  0 auto;
  display: inline-block;
}

input {
  margin-top: 30px;
}
</style>
