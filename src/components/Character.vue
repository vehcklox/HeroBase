<template>
  <div class="col-md-4 my-2 ">
    <div class="character-card">
      <div class="float-right">

      </div>
      <div class="row align-items-center">
        <div class="col-1">
          <i v-if="page > 0 && page <= count"
             @click="page--"
             class="ml-3 fal fa-chevron-square-left fa-2x"
          ></i>
        </div>

        <div class="col-10">
          <div class="card-body" @click="switchCharacter" v-if="loaded">
            <h4 class="card-title">{{ character[this.page].name }}</h4>
            <p class="card-text">
              Height: <br> {{ character[this.page].height }}</p>
            <p class="card-text">
              Hair Color: <br> {{ character[this.page].hair_color }}</p>
            <p class="card-text">
              Eye Color: <br> {{ character[this.page].eye_color }}</p>
            <p class="card-text">
              Date of Birth: <br> {{ character[this.page].date_of_birth }}</p>
          </div>
        </div>

        <div class="col-1">
          <i v-if="page < count"
             @click="page++"
             class="mr-1 fal fa-chevron-square-right fa-2x"></i>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
  export default {
    props: ['id', 'card'],
    data() {
      return {
        loaded: false,
        character: {},
        count: -1,
        page: -1,
      }
    },
    methods: {
      fetchCharacter(id) {
        fetch(`https://lotrapi.app/api/v1/characters/${id}`, {
          method: 'get'
        }).then(response => response.json())
          .then(json => {
            this.count++;
            this.page++;
            this.$set(this.character, this.count, json);
            this.loaded = true;
          })
      },

      switchCharacter() {
        let random_id = Math.floor(Math.random() * 10) + 1;
        this.fetchCharacter(random_id)
      },
    },
    created() {
      this.fetchCharacter(this.id);
    }
  }
</script>
