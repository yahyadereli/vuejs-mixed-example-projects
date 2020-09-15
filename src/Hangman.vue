<template>
  <div class="MainPage">
    <div class="Top"></div>
    <div class="Middle">
      <div class="SideBars"></div>
      <div class="LeftGame">
        <div class="hangMan">
          <div v-if="winner == 0"></div>
          <div class="imager">
            <img
              src="https://image.shutterstock.com/image-vector/you-lose-red-rubber-stamp-260nw-244769227.jpg"
              v-show="winner == 0"
              width="100%"
              height="100%"
            />
            <div v-if="counter == 7">
              <img
                src="https://image.freepik.com/free-vector/you-win-lettering-pop-art-text-banner_185004-60.jpg"
                v-show="counter == 7"
                width="100%"
                height="100%"
              />
            </div>
          </div>
        </div>
        <div class="hideLetter">
          <div
            class="hideButton"
            v-for="(letter, letterIndex) in findLetter"
            :key="letterIndex"
            v-cloak
          >
            {{ letter }}
          </div>
        </div>
      </div>
      <div class="RightGame">
        <div class="RightGameLetter">
          <div
            class="RGT"
            v-for="(row, lettersIndex) in letters"
            :key="lettersIndex"
          >
            <button
              class="Letter"
              v-for="(letter, colIndex) in row"
              :key="colIndex"
              @click="lettersCheck(letter)"
              :disabled="winner == 0 || counter == 7 || findWord == ''"
            >
              {{ letter }}
            </button>
          </div>
        </div>
        <div class="RightGameControl">
          <div class="AnswerLetter">
            <button class="RestartButton" @click="start(x)">Start</button>
            <div v-if="counter != 7">
              <div v-if="winner != 0">Choice = {{ winner }}</div>
              <div v-if="winner != 0">Find = {{ counter }}</div>
              <div v-if="counter == 7 || winner == 0">{{ findWord }}</div>
            </div>
          </div>
        </div>
      </div>
      <div class="SideBars"></div>
    </div>
    <div class="Lower"></div>
    <div></div>
  </div>
</template>

<script>
export default {
  data: () => {
    return {
      images: [],
      words: [
        "SHAVING",
        "WASHING",
        "DRAWING",
        "OVERSAW",
        "SERVING",
        "UNSAVED",
        "UNWHITE",
        "VINEGAR",
        "VINTAGE",
        "WEIGHTS",
        "WRIGHTS",
        "ENOUGHS",
        "GUNSHOT",
        "HARVEST",
        "HUNGERS",
        "STOWING",
        "TWINGES",
        "VERTIGO",
        "WEARING",
        "ADVISOR",
        "GROUNDS",
        "HOSTING",
        "SERVANT",
        "SITDOWN",
        "TAVERNS",
        "THUNDER",
        "VERSION"
      ],
      letters: [
        "D",
        "E",
        "V",
        "R",
        "S",
        "A",
        "G",
        "T",
        "I",
        "N",
        "O",
        "U",
        "W",
        "H"
      ],
      findLetter: ["_", "_", "_", "_", "_", "_", "_"],
      findWord: "",
      winner: 6,
      counter: 0,
      selectedLetters: [],
      deletedLetter: "",
      deneme: ""
    };
  },
  methods: {
    start(x) {
      this.letters = [
        "D",
        "E",
        "V",
        "R",
        "S",
        "A",
        "G",
        "T",
        "I",
        "N",
        "O",
        "U",
        "W",
        "H"
      ];
      this.counter = 0;
      this.winner = 6;
      this.selectedLetters = [];
      this.findLetter = ["_", "_", "_", "_", "_", "_", "_"];
      var i = Math.floor(Math.random() * this.words.length);
      this.findWord = this.words[i];
    },
    lettersCheck(letter) {
      var counter = "";
      this.deletedLetter = "";
      for (var i = 0; i < this.findWord.length; i++) {
        if (letter == this.findWord[i]) {
          Vue.set(this.findLetter, i, letter);
          counter = this.findWord[i];
          this.counter++;
        }
        if (letter == this.letters[i[i]]) {
          this.letters.splice(i);
        }
      }
      if (letter != counter) {
        this.winner--;
      }
      if (letter == counter || letter != counter) {
        this.selectedLetters.push(letter);
        this.deletedLetter = letter;
        for (var i = 0; i < this.letters.length; i++) {
          if (this.deletedLetter == this.letters[i]) this.letters[i] = "";
        }
      }
    }
  }
};
</script>

<style>
.MainPage {
  display: flex;
  flex-direction: column;
  height: 100vh;
  width: 100%;
  background-color: rgb(184, 184, 184);
}
.Top {
  width: 100%;
  height: 10%;
  background-color: white;
}
.Middle {
  display: flex;
  flex-direction: row;
  width: 100%;
  height: 80%;
}
.Lower {
  width: 100%;
  height: 10%;
  background-color: white;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}
.SideBars {
  width: 10%;
  height: 100%;
}
.LeftGame {
  width: 40%;
  height: 100%;
  background-color: whitesmoke;
  border-right: 1px solid black;
  display: flex;
  flex-direction: column;
}
.hangMan {
  width: 100%;
  height: 80%;
  justify-content: center;
  align-items: center;
}
.hideLetter {
  width: 100%;
  height: 20%;
  background-color: rgb(248, 217, 248);
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}
.hideButton {
  height: 50%;
  width: 10%;
  font-size: 200%;
}
.RightGame {
  display: flex;
  flex-direction: row;
  width: 40%;
  height: 100%;
  background-color: whitesmoke;
}
.RightGameLetter {
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 100%;
  background-color: white;
  border: 0.5px dashed black;
}
.RGT {
  display: flex;
  flex-direction: row;
  width: 100%;
  height: 33%;
}
.RightGameControl {
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 50%;
  justify-content: center;
  align-items: center;
}
.RestartButton {
  background-color: green;
  width: 100%;
}
.Letter {
  width: 30%;
  height: 80%;
  margin-left: 4%;
  margin-top: 2%;
}
.imager {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 120%;
}
</style>
