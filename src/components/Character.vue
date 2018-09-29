<template>
  <div class="col-md-4 my-2 " @click="switchCharacer">
    <div class="character-card">
      <div class="card-body">
        <h4 class="card-title">{{ character.name }}</h4>
        <p class="card-text">Height: <br> {{ character.height }}</p>
        <p class="card-text">Hair Color: <br> {{ character.hair_color }}</p>
        <p class="card-text">Eye Color: <br> {{ character.eye_color }}</p>
        <p class="card-text">Date of Birth: <br> {{ character.date_of_birth }}</p>
      </div>
    </div>
  </div>
</template>


<script>
  export default {
    props: ['id'],
    data() {
      return {
        character: {}
      }
    },
    methods: {
      fetchCharacter(id) {
        fetch(`https://lotrapi.app/api/v1/characters/${id}`, {
          method: 'get'
        }).then(response => response.json())
          .then(json => this.character = json)
      },

      switchCharacer() {
        let random_id = Math.floor(Math.random() * 10) + 1
        this.fetchCharacter(random_id)
      }
    },
    created() {
      this.fetchCharacter(this.id);
    }
  }
</script>
