<template>
  <span>
    <LetterContainer
      :letter="char.letter"
      :letterClass="char.cssClass"
      v-for="char in displayChars"
      :key="char"
    />
    <div class="clear">
    </div>
  </span>
</template>

<style scoped>
div {
  margin: 0 0.25em 0.25em 0;
}

div.clear {
  clear:  both;
  margin: 0;
}
</style>

<script>
import LetterContainer from './LetterContainer';

export default {
  name: 'GuessContainer',
  components: {
    LetterContainer,
  },
  props: {
    guess: {
      required: false,
      type: String,
    },
    actualWord: {
      required: true,
      type: String,
    }
  },
  computed: {
    displayChars: function () {
      if (this.guess) {
        return [...this.guess].map((char, pos) => {
          return {
            letter: char,
            cssClass: this.getCssClass(char, pos),
          }
        });
      }

      return [...'     '].map(function(char) {
        return {
          letter: char,
          cssClass: '',
        };
      })
    }
  },
  methods: {
    getCssClass: function(char, pos) {
      const actualWord = this.actualWord;

      if (actualWord.charAt(pos) === char) {
        return 'correct';
      }

      if (actualWord.includes(char)) {
        return 'contains';
      }

      return '';
    },
  },
}
</script>