<template>
  <div>
    <div class="sos-game-table" v-for="(row ,rowIndex) in rows" :key="rowIndex">
      <div class="sos-game-row" v-for="(col,colIndex) in row" :key="colIndex">
        <div class="sos-game-col" v-for="(square,squareIndex) in col" :key="squareIndex">
          <div class="sos-game-square">
            {{ square }}
            <div
              class="sos-game-square-half"
              v-if="square==false"
              @click="deneme(rowIndex,colIndex,s)"
            >S</div>
            <div
              class="sos-game-square-half"
              v-if="square==false"
              @click="deneme(rowIndex,colIndex,o)"
            >O</div>
          </div>
        </div>
      </div>
    </div>
    <div class="sos-game-point-table">
      <strong> {{ sira }}</strong>
    </div>
    <div class="sos-game-point-table">
      <span class="sos-game-player-point-box">
        <strong>Player 1 :</strong>
        {{ player1point }}
      </span>
      <span class="sos-game-player-point-box">
        <strong>Player 2 :</strong>
        {{ player2point }}
      </span>
    </div>
    <div class="sos-game-point-table">
      <button class="sos-game-restart-button" @click="restart()">Restart</button>
    </div>
  </div>
</template>
<script>
export default {
  data: () => {
    return {
      rows: [
        [[""], [""], [""], [""], [""], [""], [""], [""], [""], [""]],
        [[""], [""], [""], [""], [""], [""], [""], [""], [""], [""]],
        [[""], [""], [""], [""], [""], [""], [""], [""], [""], [""]],
        [[""], [""], [""], [""], [""], [""], [""], [""], [""], [""]],
        [[""], [""], [""], [""], [""], [""], [""], [""], [""], [""]],
        [[""], [""], [""], [""], [""], [""], [""], [""], [""], [""]],
        [[""], [""], [""], [""], [""], [""], [""], [""], [""], [""]],
        [[""], [""], [""], [""], [""], [""], [""], [""], [""], [""]],
        [[""], [""], [""], [""], [""], [""], [""], [""], [""], [""]],
        [[""], [""], [""], [""], [""], [""], [""], [""], [""], [""]]
      ],
      s: "S",
      o: "O",
      player1point: 0,
      player2point: 0,
      sira: "PLAYER1"
    };
  },
  methods: {
    deneme(r, c, i) {
      let count = 0;
      if (this.rows[r][c] == "") {
        this.$set(this.rows[r], [c], i);
      }
      if (this.rows[r][c] == "O") {
        if (this.rows[r][c + 1] == "S" && this.rows[r][c - 1] == "S") count++;
        if (
          this.rows[r + 1] &&
          this.rows[r + 1][c] == "S" &&
          this.rows[r - 1] &&
          this.rows[r - 1][c] == "S"
        )
          count++;
        if (
          this.rows[r - 1] &&
          this.rows[r - 1][c + 1] == "S" &&
          this.rows[r + 1] &&
          this.rows[r + 1][c - 1] == "S"
        )
          count++;
        if (
          this.rows[r - 1] &&
          this.rows[r - 1][c - 1] == "S" &&
          this.rows[r + 1] &&
          this.rows[r + 1][c + 1] == "S"
        )
          count++;
      }
      if (this.rows[r][c] == "S") {
        if (
          this.rows[r + 1] &&
          this.rows[r + 1][c] == "O" &&
          this.rows[r + 2] &&
          this.rows[r + 2][c] == "S"
        )
          count++;
        if (
          this.rows[r - 1] &&
          this.rows[r - 1][c] == "O" &&
          this.rows[r - 2] &&
          this.rows[r - 2][c] == "S"
        )
          count++;
        if (this.rows[r][c + 1] == "O" && this.rows[r][c + 2] == "S") count++;
        if (this.rows[r][c - 1] == "O" && this.rows[r][c - 2] == "S") count++;
        if (
          this.rows[r + 1] &&
          this.rows[r + 1][c + 1] == "O" &&
          this.rows[r + 2] &&
          this.rows[r + 2][c + 2] == "S"
        )
          count++;
        if (
          this.rows[r - 1] &&
          this.rows[r - 1][c - 1] == "O" &&
          this.rows[r - 2] &&
          this.rows[r - 2][c - 2] == "S"
        )
          count++;
        if (
          this.rows[r - 1] &&
          this.rows[r - 1][c + 1] == "O" &&
          this.rows[r - 2] &&
          this.rows[r - 2][c + 2] == "S"
        )
          count++;
        if (
          this.rows[r + 1] &&
          this.rows[r + 1][c - 1] == "O" &&
          this.rows[r + 2] &&
          this.rows[r + 2][c - 2] == "S"
        )
          count++;
      }
      this.playerControl(r, c);
      if (count == 0) {
        this.sira = this.sira == "PLAYER 2" ? "PLAYER 1" : "PLAYER 2";
      }
      this.pointControl(r, c);
      if (count != 0 && this.sira == "PLAYER 1") {
        this.player1point += count;
      }
      if (count != 0 && this.sira == "PLAYER 2") {
        this.player2point += count;
      }
    },
    playerControl(r, c) {},
    pointControl(r, c) {},
    restart() {
      (this.rows = [
        [[""], [""], [""], [""], [""], [""], [""], [""], [""], [""]],
        [[""], [""], [""], [""], [""], [""], [""], [""], [""], [""]],
        [[""], [""], [""], [""], [""], [""], [""], [""], [""], [""]],
        [[""], [""], [""], [""], [""], [""], [""], [""], [""], [""]],
        [[""], [""], [""], [""], [""], [""], [""], [""], [""], [""]],
        [[""], [""], [""], [""], [""], [""], [""], [""], [""], [""]],
        [[""], [""], [""], [""], [""], [""], [""], [""], [""], [""]],
        [[""], [""], [""], [""], [""], [""], [""], [""], [""], [""]],
        [[""], [""], [""], [""], [""], [""], [""], [""], [""], [""]],
        [[""], [""], [""], [""], [""], [""], [""], [""], [""], [""]]
      ]),
        (this.s = "S"),
        (this.o = "O"),
        (this.player1point = 0),
        (this.player2point = 0),
        (this.sira = "PLAYER1");
    }
  }
};
</script>
<style>
.sos-game-square {
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  border: 1px solid red;
  width: 40px;
  height: 40px;
  font-size: 35px;
  justify-content: center;
}
.sos-game-table {
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: center;
  align-items: center;
}
.sos-game-square-half {
  border: 1px solid #666;
  background-color: rgb(241, 241, 241);
  width: 20px;
  height: 30px;
  text-align: center;
  justify-content: center;
  font-size: 20px;
  padding-top: 8px;
}
.sos-game-point-table {
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: center;
}
.sos-game-player-point-box{
  border: 1px solid #666;
  padding: 5px;
}
.sos-game-restart-button{
  background-color: green;
  border: 0;
  color: white;
  font-family: inherit;
  font-size: inherit;
  padding: 0.5em;
  margin: 3px;
}
</style>
