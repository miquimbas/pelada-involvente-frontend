<template>
  <div>
    <section class="hero is-primary">
      <div class="hero-body">
          <div class="container">
            <p class="title is-1">Pelada</p>
            <p class="subtitle is-3">{{ game.day }}</p>
          </div>
        </div>
      </section>

      <div class="demo">
        <table class="table is-bordered">
            <thead>
              <tr>
                  <th>Lista de Confirmados</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="player of game.players"> 
                <td>
                    <input v-on:click="edita(player)" class="button is-white" v-model="player.nickName">
                    <a v-on:click="remove(player)" class="delete"></a>
                </td>
              </tr>
            </tbody>
          </table>
        </div>

        <div class="demo">
          <table class="table is-bordered is-responsive">
            <thead>
              <tr>
                  <th>Lista de Espera</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="player of game.waitingList"> 
                <td>{{ player.nickName }}</td>
              </tr>
            </tbody>
          </table>
      </div>

  </div>
</template>

<script>
export default {
  data () {
    return{
      game: {},
      edita: function(player) {
          console.log("edita o " + player.nickName);
      },
      remove: function(player) {
          console.log("remove o " + player.nickName);
      }
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
