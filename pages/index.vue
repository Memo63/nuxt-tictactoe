<template>
  <div>
    <div
      :class="{'border border-green-500': player,'border border-blue-500': !player}"
      class="mx-auto rounded-md w-60 mt-20 p-5"
    >
      <div class="text-center text-blue-500 text-3xl mb-3">
        tictactoe game
      </div>
      <div
        v-if="start"
        class="grid grid-cols-3 grid-rows-3 grid-flow-row gap-4 text-2xl w-36 mx-auto"
      >
        <div
          v-for="(item, index) in field"
          :key="index"
          class="bg-blue-500 w-9 h-9"
          @click.once="item.text===''?updateField(index):''"
        >
          <div class="mx-auot my-auto ml-2">
            {{ item.text }}
          </div>
        </div>
      </div>
    </div>
    <div
      class="mx-auto rounded-md w-60 mt-5 p-5 text-center"
      :class="{'border border-blue-500': !player, 'border border-green-500': player}"
    >
      <div
        :class="{'visible':start, 'hidden':!start}"
      >
        <div v-if="player" class="text-green-500">
          Spieler 1 am Zug
        </div>
        <div v-if="!player" class="text-blue-500">
          Spieler 2 am Zug
        </div>
      </div>

      <button
        v-if="!start"
        class="w-32 mt-2 border rounded-md border-gray-700 p-2 hover:bg-gray-400"
        @click="start=true"
      >
        Spielen
      </button>
      <button
        v-if="start"
        class="w-32 mt-2 border rounded-md border-gray-700 p-2 hover:bg-gray-400"
        @click="resetField()"
      >
        Zurücksetzen
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      player: true,
      win: false,
      start: false,
      countRound: 0,
      field: [
        { id: 0, text: '', value: 0 },
        { id: 1, text: '', value: 0 },
        { id: 2, text: '', value: 0 },
        { id: 3, text: '', value: 0 },
        { id: 4, text: '', value: 0 },
        { id: 5, text: '', value: 0 },
        { id: 6, text: '', value: 0 },
        { id: 7, text: '', value: 0 },
        { id: 8, text: '', value: 0 }
      ]
    }
  },
  methods: {
    updateField (ind) {
      this.countRound++
      this.player ? this.field[ind].text = 'X' : this.field[ind].text = 'O'
      this.player ? this.field[ind].value = 1 : this.field[ind].value = 3
      // this.field[ind].text = ind
      this.checkField(ind)
      this.player = !this.player
      if (this.countRound === 9 && !this.win) {
        alert('Leider hat keiner gewonnen!')
      }
      if (this.win) { this.resetField() }
    },
    checkField (ind) {
      switch (ind) {
        case 0:
          this.checkWin(this.field[0].value, this.field[1].value, this.field[2].value)
          this.checkWin(this.field[0].value, this.field[3].value, this.field[6].value)
          this.checkWin(this.field[0].value, this.field[4].value, this.field[8].value)
          break
        case 1:
          this.checkWin(this.field[1].value, this.field[4].value, this.field[7].value)
          this.checkWin(this.field[1].value, this.field[0].value, this.field[2].value)
          break
        case 2:
          this.checkWin(this.field[2].value, this.field[5].value, this.field[8].value)
          this.checkWin(this.field[2].value, this.field[1].value, this.field[0].value)
          this.checkWin(this.field[2].value, this.field[4].value, this.field[6].value)
          break
        case 3:
          this.checkWin(this.field[3].value, this.field[4].value, this.field[5].value)
          this.checkWin(this.field[3].value, this.field[0].value, this.field[6].value)
          break
        case 4:
          this.checkWin(this.field[4].value, this.field[2].value, this.field[6].value)
          this.checkWin(this.field[4].value, this.field[0].value, this.field[8].value)
          this.checkWin(this.field[4].value, this.field[1].value, this.field[7].value)
          this.checkWin(this.field[4].value, this.field[3].value, this.field[5].value)
          break
        case 5:
          this.checkWin(this.field[5].value, this.field[2].value, this.field[8].value)
          this.checkWin(this.field[5].value, this.field[4].value, this.field[3].value)
          break
        case 6:
          this.checkWin(this.field[6].value, this.field[7].value, this.field[8].value)
          this.checkWin(this.field[6].value, this.field[3].value, this.field[0].value)
          this.checkWin(this.field[6].value, this.field[4].value, this.field[2].value)
          break
        case 7:
          this.checkWin(this.field[7].value, this.field[6].value, this.field[8].value)
          this.checkWin(this.field[7].value, this.field[4].value, this.field[1].value)
          break
        case 8:
          this.checkWin(this.field[8].value, this.field[7].value, this.field[6].value)
          this.checkWin(this.field[8].value, this.field[5].value, this.field[2].value)
          this.checkWin(this.field[8].value, this.field[4].value, this.field[0].value)
          break
      }
    },
    checkWin (ind1, ind2, ind3) {
      if (this.player) {
        if (ind1 + ind2 + ind3 === 3) {
          alert('Spieler 1 hat gewonnen"')
          this.win = true
        }
      } else
      if (ind1 + ind2 + ind3 === 9) {
        alert('Spieler 2 hat gewonnen"')
        this.win = true
      }
    },
    resetField () {
      for (let i = 0; i < 9; i++) {
        this.field[i].text = ''
        this.field[i].value = 0
      }
      this.win = false
      this.player = true
      this.start = false
      this.countRound = 0
    }
  }
}

</script>

<style>

</style>
