<template>
  <div>
    <h1>Pelada</h1>
    <h3>{{ game.day }}</h3>

    <h4>Lista de Confirmados</h4>
    <ul>
      <li v-for="player of game.players">{{ player.nickName }}</li>
    </ul>

    <h4>Lista de Espera</h4>
    <ul>
      <li v-for="player of game.waitingList">{{ player.nickName }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  data () {
    return{
      game: {}
    }
  },
  created () {
    this.$http.get('http://localhost:8080/pelada/list')
      .then(result => result.json())
      .then(function(game){
        this.game = game;
        this.game.day = new Date(game.day).toLocaleString();
        console.log(game);
      });
  }
}
</script>

<style lang="scss">

</style>
