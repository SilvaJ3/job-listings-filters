<template>
  <div id="app">
    <section>
      <div class="container">
        <FilteredTags 
        :tags="tags" 
        :tools="tools" 
        :role="role" 
        :level="level" 
        v-show="tags[0] || role || level || tools[0]" 
        @clear="clearTags" 
        @unSelected="undoTag" 
        @unSelectedTool="undoTool" 
        @unSelectedRole="undoRole"
        @unSelectedLevel="undoLevel"
        />
        <Card 
        v-for="job in filterJob" 
        :key="job.id" 
        :data="job" 
        @filterTag="selectedTag" 
        @filterTool="selectedTool" 
        @filterRole="selectedRole" 
        @filterLevel="selectedLevel"
        />
      </div>
    </section>
  </div>
</template>

<script>
import Card from "./components/Card.vue"
import FilteredTags from "./components/FilteredTags.vue"
import data from "../exo-ressources/data.json"


export default {
  name: 'App',
  components: {
    Card,
    FilteredTags
  },
  data() {
    return {
      offer: data,
      filteredJob: [],
      tags: [],
      tools: [],
      role: "",
      level: "",
    }
  },
  methods: {
    selectedTag(value){
      if (!this.tags.includes(value)) {
        this.tags.push(value);
      }
    },
    selectedTool(value){
      if (!this.tools.includes(value)) {
        this.tools.push(value);
      }
    },
    selectedRole(value){
      this.role = value;
    },
    selectedLevel(value){
      this.level = value;
    },
    filter(){
      this.filteredJob = [];
      this.offer.forEach(element => {
        if (this.tags.every(key => element.languages.includes(key)) && this.tools.every(key => element.tools.includes(key)) && (this.role === element.role || this.role === "" && (this.level === element.level || this.level === ""))) {
          if (!this.filteredJob.includes(element)) {
            this.filteredJob.push(element);
          }
        }
      })
      
    },
    // Suppression du niveau
    undoLevel(){
      this.level = ""
    },
    // Suppression du role
    undoRole(){
      this.role = ""
    },
    // Suppression d'un tag
    undoTag(tag){
      let index = this.tags.indexOf(tag);
      this.tags.splice(index, 1);
    },
    // Suppression d'un tool
    undoTool(tool){
      let index = this.tools.indexOf(tool);
      this.tools.splice(index, 1);
      console.log(this.tools);
    },
    // Clear all the selected tags
    clearTags(){
      this.tags = [];
      this.tools = [];
      this.filteredJob = [];
      this.role = ""
      this.level = ""
    }
  },
  computed: {
    filterJob: function () {
      if (this.tags[0] || this.role || this.level || this.tools[0]) {
        this.filter();
        return this.filteredJob
      } else {
        return this.offer
      }
    },
  }
}

</script>

<style lang="sass">
body
  font-family: 'Spartan', sans-serif
  padding: 0
  padding-top: 10%
  margin: 0
  box-sizing: border-box
  background-image: url("./assets/bg-header-desktop.svg")
  background-repeat: no-repeat
  background-size: contain
  background-color: hsl(180, 29%, 50%)

.container
  display: flex
  flex-direction: column
  justify-content: center
  align-items: center
  background-color: hsl(180, 52%, 96%)
  padding: 5% 15%
</style>
