<template>
  <div id="app">
    <h3>{{ title }}</h3>
    <div class="col-md-12">
      <div class="row">
        <Character
          v-for="(id, index) in initial_ids"
          :id="id"
          :key="index"
          :card="index"
        />
      </div>
    </div>
  </div>
</template>

<script>
  import Character from './components/Character';
  export default {
    name: 'app',
    data() {
      return {
        title: 'Generate Your Army',
        initial_ids: [1, 5, 8]
      };
    },
    components: {
      Character
    }
  };
</script>
