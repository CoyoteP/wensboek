<template>
  <!-- <div class="search_bar">
    zoeken maar
    <input type="text" v-model="search" placeholder="zoek een wens"/>
  </div>
  {{ search }}
  <div class="home">
    <div v-if="projects.length">
      <p>check1</p>
      {{ search }}
      <div v-if="search !== 'search'">
        <p>check</p>
        <div v-for="project in projects" :key="project.id">
          <p>{{project.wens}}</p>
          <div v-if="searchPhrase in project.wens">
            <SingleProject :project="project" @delete="handleDelete" @complete="handleComplete" />
          </div>
        </div>
      </div>
      <div v-else>
        <div v-for="project in projects" :key="project.id">
          <p>{{project.wens}}</p>
          <SingleProject :project="project" @delete="handleDelete" @complete="handleComplete" />
        </div>
      </div>
    </div>
  </div> -->
  <div class="home">
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <SingleProject :project="project" @delete="handleDelete" @complete="handleComplete" />
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from '../components/SingleProject.vue'

export default {
  name: 'Home',
  components: { SingleProject },
  data() {
    return {
      projects: [],
      searchPhrase: "yes",
      search: ""
    };
  },
  mounted() {
    fetch('http://localhost:3000/wishes')
      .then(res => res.json())
      .then(data => this.projects = data)
      .catch(err => console.log(err))
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter(project => {
        return project.id !== id
      })
    },
    handleComplete(id) {
      let p = this.projects.find(project => {
        return project.id === id
      })
      p.complete = !p.complete
    }
  }
}
</script>
