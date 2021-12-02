<template>
  <div class="card">
    <!-- Left part -->
    <div class="info">
      <div>
        <img :src="companyLogo" alt="" class="companyLogo">
      </div>
      <div class="infoDetail">
        <div class="companyName">
          <p>{{data.company}}</p>
          <div>
            <span v-show="data.new" class="newTag">NEW!</span>
            <span v-show="data.featured" class="featuredTag">FEATURED</span>
          </div>
        </div>
        <h1 class="jobTitle">{{ data.position}}</h1>
        <p class="details">{{ data.postedAt }} - {{ data.contract }} - {{ data.location }}</p>
      </div>
    </div>
    <!-- Right part -->
    <div class="tags">
      <span @click="roleSelection(data.role)">{{ data.role }}</span>
      <span @click="levelSelection(data.level)">{{ data.level }}</span>
      <span v-for="tag in data.languages" :key="tag" @click="tagSelection(tag)">{{ tag }}</span>
      <span v-for="tool in data.tools" :key="tool" @click="toolSelection(tool)">{{ tool }}</span>
    </div>
  </div>
</template>

<script>

export default {
  data(){
    return {
      // img: this.data.logo
    }
  },
  props: {
    data: Object
  },
  methods: {
    tagSelection(value) {
      this.$emit("filterTag", value)
    },
    toolSelection(value) {
      this.$emit("filterTool", value)
    },
    roleSelection(value) {
      this.$emit("filterRole", value)
    },
    levelSelection(value) {
      this.$emit("filterLevel", value)
    },
  },
  computed: {
    companyLogo() {
      return require(`@/assets/${this.data.logo}`)
    }
  }
}

</script>

<style lang="sass">
.card
  display: flex
  justify-content: space-between
  align-items: center
  width: 100%
  background-color: white
  border-radius: 5px
  padding: 30px 30px
  box-shadow: 0px 0px 7px 0px rgba(0, 0, 0, .4)
  margin-bottom: 2%
  .info
    display: flex
    align-items: center
    .companyName 
      display: flex
      align-items: center
      p
        color: hsl(180, 29%, 50%)
        font-weight: 700
        padding-right: 7%
      span
        font-size: 11px
        border-radius: 10px 
        padding: 6px 8px 3px
        color: white
        margin-right: 5%
        font-weight: 700
        width: 30px
        height: 20px
      .newTag
        background-color: hsl(180, 29%, 50%)
      .featuredTag
        background-color: hsl(180, 14%, 20%)
    .companyLogo
      border-radius: 50%
    .infoDetail
      display: flex
      flex-direction: column
      justify-content: center
      margin-left: 10%
      width: 300px
      p
        margin: 0
      .jobTitle
        font-size: 15px
        margin: 5% 0
        font-weight: 700
      .jobTitle:hover
        color: hsl(180, 29%, 50%)
        cursor: pointer
      .details
        color: grey
  .tags
    display: flex
    justify-content: end
    width: 50%
    span
      color: hsl(180, 29%, 50%)
      background-color: hsl(180, 31%, 95%)
      font-weight: 700
      font-size: 13px
      padding: 10px 7px
      margin: 0 10px
      cursor: pointer
    span:hover
      color: hsl(180, 31%, 95%)
      background-color: hsl(180, 29%, 50%)

</style>