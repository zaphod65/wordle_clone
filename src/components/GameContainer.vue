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
      <input placeholder="GUESS" v-on:keyup.enter="addGuess" :disabled="gameOver" maxlength="5">
      <button v-on:click="resetGame">Reset?</button>
      <h3>Guess chain of: <span :class="chainClass">{{guessChain}}</span> correct</h3>
    </div>
  </div>
</template>

<script>
import GuessContainer from './GuessContainer';
import randomWord from 'random-word-by-length';

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
      word: this.newWord(),
      maxGuesses: 6,
      guessChain: 0,
    };
  },
  computed: {
    chainClass: function() {
      if (this.guessChain > 10) {
        return 'guessBig';
      } else if (this.guessChain >= 5) {
        return 'guessMedium';
      } else if (this.guessChain >= 1) {
        return 'guessSmall';
      }
      return 'guessNone';
    },
  },
  methods: {
    newWord: function () {
      let newWord = randomWord(5);
      while (newWord.length !== 5) {
        newWord = randomWord(5);
      }
      return newWord;
    },
    addGuess: function(event) {
      const guess = event.target.value.toUpperCase();

      if (guess.length !== 5) {
        return;
      }

      if (guess === this.word) {
        this.gameWon = true;
        this.gameOver = true;
        this.guessChain++;
      }

      if (this.currentGuess === this.maxGuesses) {
        this.gameOver = true;
        this.guessChain = 0;
      }

      this.guesses[this.currentGuess] = guess;
      event.target.value = "";
      this.currentGuess++;
    },
    resetGame: function() {
      this.gameWon = false;
      this.gameOver = false;
      this.guesses = [];
      this.currentGuess = 1;
      this.word = this.newWord();
    }
  }
}
</script>

<style scoped>
h1 {
  color: #fff;
}

h3 {
  color: #999;
  margin: 40px 0 0;
}

div.center {
  margin:  0 auto;
  display: inline-block;
}

input {
  margin-top: 30px;
}

span.guessSmall {
  color: darkslateblue;
}

span.guessMedium {
  color: darkkhaki;
}

span.guessBig {
  color: darkseagreen;
}
</style>
