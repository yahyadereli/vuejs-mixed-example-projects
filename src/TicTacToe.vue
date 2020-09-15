<template>
  <div>
    <div class="mainTable">
      <div class="tic-tac-toe-row" v-for="(row, rowindex) in rows" :key="rowindex">
        <div
          class="tic-tac-toe-column"
          :class="{ 'tic-tac-toe-column-full': col }"
          v-for="(col, colindex) in row"
          :key="colindex"
          @click="playGame(rowindex, colindex)"
        >{{ col }}</div>
      </div>
      <div class="tic-tac-toe-row">
        <span v-if="winner">Winner: {{ winner }}</span>
        <span v-if="!winner && mouseTick<25">Player: {{ xox }}</span>
        <span v-if="!winner && mouseTick>25">The game is a draw</span>
        <div>
          <button class="restart-button" @click="restart()">RESTART</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data: () => {
    return {
      rows: [["", "", ""], ["", "", ""], ["", "", ""]],
      xox: "X",
      winner: "",
      mouseTick: 0
    };
  },
  methods: {
    playGame(r, c) {
      if (this.rows[r][c] == "" && !this.winner) {
        this.$set(this.rows[r], c, this.xox);
        this.xox = this.xox == "X" ? "O" : "X";
        this.checkWinner();
        this.mouseClick();
      }
    },
    checkWinner() {
      const rows = this.rows;
      for (let i = 0; i < 3; i++) {
        if (
          rows[0][i] != "" &&
          rows[0][i] == rows[1][i] &&
          rows[1][i] == rows[2][i]
        ) {
          this.winner = rows[0][i];
        }
      }
      for (let i = 0; i < 3; i++) {
        if (
          rows[i][0] != "" &&
          rows[i][0] == rows[i][1] &&
          rows[i][1] == rows[i][2]
        ) {
          this.winner = rows[i][0];
        }
      }
      if (
        rows[0][0] != "" &&
        rows[0][0] == rows[1][1] &&
        rows[1][1] == rows[2][2]
      ) {
        this.winner = rows[0][0];
      }
      if (
        rows[2][0] != "" &&
        rows[2][0] == rows[1][1] &&
        rows[1][1] == rows[0][2]
      ) {
        this.winner = rows[2][0];
      }
    },
    restart() {
      if (this.winner == "X" || "O" || "") {
        (this.rows = [["", "", ""], ["", "", ""], ["", "", ""]]),
          (this.xox = "X"),
          (this.winner = ""),
          (this.mouseTick = 0);
      }
    },
    mouseClick() {
      for (let y = 0; y < 3; y++) {
        if (!this.rows[y] == "X" || "O") {
          this.mouseTick++;
        }
      }
    }
  }
};
</script>

<style>
.tic-tac-toe-row {
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: center;
  align-items: center;
  -webkit-user-select: none;
}
.tic-tac-toe-column {
  border: 1px dashed #666;
  width: 80px;
  height: 80px;
  font-size: 75px;
  text-align: center;
}

.tic-tac-toe-column-full {
  background-color: #eee;
  cursor: not-allowed;
}
.restart-button {
  background-color: darkslategrey;
}
</style>
