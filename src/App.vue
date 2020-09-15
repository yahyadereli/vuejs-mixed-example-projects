<template>
  <div>
  <PhoneListGrid/>

    <!-- 
  <Hangman/>
  <SosGame/>
  <TicTacToe />
 -->
  </div>
</template>

<script>
import TicTacToe from "./TicTacToe.vue";
import SosGame from "./SosGame.vue";
import PhoneListGrid from "./PhoneListGrid.vue";
import Hangman from "./Hangman.vue";

export default {
  components: {
    TicTacToe,
    SosGame,
    PhoneListGrid,
    Hangman
  }
};
</script>

<style src="./styles/main.css" />
