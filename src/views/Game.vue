<template>
   <div class="game container-fluid">
      <div class="row">
          <div class="col-12">
              <h1 class="text-center">Vue Slap</h1>
              <input v-if="target.health == 100" v-model="target.name" type="text">
              <button v-if="target.health < 100" @click="restart" class="btn btn-success">Restart</button>
          </div>
          <div class="col-6">
              <img v-if="target.health > 50" src="https://upload.wikimedia.org/wikipedia/en/8/87/ShaggyRogers.png" alt="shaggy">
              <img class="card-img" v-else-if="target.health > 0" src="https://i.pinimg.com/originals/e7/ed/54/e7ed5472bafec55ab556e00f93f65ffc.jpg" alt="shaggy-scared">
              <img v-else src="https://archive-media-1.nyafuu.org/bant/image/1494/45/1494457435558.jpg" alt="shaggy-dead">
          </div>
          <div class="col-6">
              <h2 v-if="!target.name.includes('name')">Target name: {{target.name}}</h2>
              <h2>Target health: {{target.health}}</h2>
              <div class="d-flex" v-for="(damage, attack) in attacks" :key="attack">
                <button @click="attackTarget(damage)" :class="{'btn-outline-dark': attack == 'kick', 'disabled': !target.health}" class="btn btn-danger">{{attack}}</button>
              </div>
          </div>
      </div>
   </div>
</template>

<script>
export default {
   name: "game",
   props: [],
   data() {
      return {
          target: {
              name: 'Enter a name',
              health: 100
          },
          attacks: {
              slap: 1,
              punch: 5,
              kick: 10
          }
      }
   },
   computed: {
       isValidName() {
           return this.target.name != 'Enter a name' && this.target.name.length
       }
   },
   methods: {
       attackTarget(dmg) {
           if (!this.isValidName) return alert("Please enter a valid name!")
           let health = this.target.health - dmg
           if (health < 0) return
           this.target.health = health
       },
       restart() {
           this.target.health = 100
       }
   },
   components: {}
}
</script>
