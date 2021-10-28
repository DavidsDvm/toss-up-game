<template>
  <h1>{{winner}}</h1>
  <img alt="Vue logo" ref="logoChange" src="./assets/head_coin.png" width="300" height="300">
  <br>
  <br>
  <input ref="gamblingCoins" type="number" value="10" min="10" :max="coins">
  <select ref="coinElection">
    <option value="cara">cara</option>
    <option value="sello">sello</option>
  </select>
  <button @click="coinFlip">Girar moneda</button>
  <br>
  <br>
  <br>
  <div>Tus monedas actuales son: {{coins}}</div>
  <br>
  <br>
  <button @click="gameFinish">Terminar de jugar</button>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      winner : "Bienvenido, dale al boton",
      coins: 5000,
      juegos: 0,
      ganados: 0,
      perdidos: 0
    }
  },
  methods: {
    coinFlip() {
      const randomNum = Math.floor(Math.random() * 2);
      var self = this
      this.juegos = Number(this.juegos) + 1

      if (this.$refs.gamblingCoins.value > this.coins){
        alert('estas apostando mas de las monedas que tienes')
      }
      else {
        if (randomNum == 1) {
          this.$refs.logoChange.src = require("./assets/heads-coinflip.gif")
          this.winner = "Girando..."
  
          setTimeout(function(){
            self.winner = "Gana cara"
            self.$refs.logoChange.src = require("./assets/head_coin.png")
          }, 3100)

          if (this.$refs.coinElection.value == "cara"){
            this.coins = parseInt(Number(this.coins) + Number(this.$refs.gamblingCoins.value))
            alert('Ganaste!')
            this.ganados = Number(this.ganados) + 1
          } else {
            this.coins = parseInt(Number(this.coins) - Number(this.$refs.gamblingCoins.value));
            alert('Perdiste!')
            this.perdidos = Number(this.perdidos) + 1
          }
        } else {
          this.$refs.logoChange.src = require("./assets/tails-coinflip.gif")
          this.winner = "Girando..."
  
          setTimeout(function(){
            self.winner = "Gana sello"
            self.$refs.logoChange.src = require("./assets/tail_coin.png")
          }, 3100)

          if (this.$refs.coinElection.value == "sello"){
            this.coins = parseInt(Number(this.coins) + Number(this.$refs.gamblingCoins.value));
            alert('Ganaste!')
            this.ganados = Number(this.ganados) + 1
          } else {
            this.coins = parseInt(Number(this.coins) - Number(this.$refs.gamblingCoins.value));
            alert('Perdiste!')
            this.perdidos = Number(this.perdidos) + 1
          }
        }
      }
    },
    gameFinish (){
      alert('Has terminado de jugar, gracias por jugar con nosotros')
      alert('Has jugado un total de: ' + this.juegos + 'partidas')
      alert('Has ganado un total de: ' + this.ganados + ' partidas')
      alert('Y perdiste un total de: ' + this.perdidos + ' partidas')
      alert('Juego elaborado por DavidsDvm, sigueme en github <3 ')
      window.open("https://github.com/DavidsDvm", "_self")
    }
  },
  watch: {
    coins(){
      if ((Number(this.coins)) == 0) {
        var self = this

        setTimeout(function(){
            alert('no te queda dinero')
            alert('Te daremos 5000 mas porque nos caes bien (;')
            self.coins = 5000
          }, 1000)
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
