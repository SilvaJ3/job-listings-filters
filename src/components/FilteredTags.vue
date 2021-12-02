<template>
  <div class="filteredTags">
    <!-- TAGS -->
    <div class="tags">
      <!-- Languages -->
      <div class="tag" v-for="tag in tags" :key="tag">
        <p>{{ tag }}</p>
        <span class="closeBtn" @click="() => unSelect(tag)">
          <img :src="removeIcon" alt="">
        </span>
      </div>
      <!-- Tools -->
      <div class="tag" v-for="tool in tools" :key="tool">
        <p>{{ tool }}</p>
        <span class="closeBtn" @click="() => unSelectTool(tool)">
          <img :src="removeIcon" alt="">
        </span>
      </div>
      <!-- Role -->
      <div class="tag" v-show="role">
        <p>{{ role }}</p>
        <span class="closeBtn" @click="() => unSelectRole()">
          <img :src="removeIcon" alt="">
        </span>
      </div>
      <!-- Level -->
      <div class="tag" v-show="level">
        <p>{{ level }}</p>
        <span class="closeBtn" @click="() => unSelectLevel()">
          <img :src="removeIcon" alt="">
        </span>
      </div>
    </div>

    <!-- CLEAR -->
    <div class="clear">
      <span @click="() => this.$emit('clear')">Clear</span>
    </div>
  </div>
</template>

<script>
import removeIcon from "../assets/icon-remove.svg";

export default {
  data(){
    return {
      removeIcon: removeIcon
    }
  },
  props: {
    tags: Array,
    tools: Array,
    role: String,
    level: String,
  },
  methods: {
    unSelect(tag) {
      this.$emit("unSelected", tag)
    },
    unSelectTool(tool) {
      this.$emit("unSelectedTool", tool)
    },
    unSelectRole() {
      this.$emit("unSelectedRole")
    },
    unSelectLevel() {
      this.$emit("unSelectedLevel")
    },
  },
}
</script>

<style lang="sass">
.filteredTags
  width: 100%
  border-radius: 5px
  padding: 20px 30px
  box-shadow: 0px 0px 7px 0px rgba(0, 0, 0, .4)
  background-color: white
  color: hsl(180, 29%, 50%)
  transform: translateY(-110px)
  margin-bottom: -5%
  display: flex
  justify-content: space-between
  align-items: center
  .tags
    display: flex
    .tag
      display: flex
      align-items: center
      margin: 0 10px
      p
        color: hsl(180, 29%, 50%)
        background-color: hsl(180, 31%, 95%)
        font-weight: 700
        font-size: 13px
        padding: 10px 7px
        border-radius: 5px 0 0 5px
      .closeBtn
        cursor: pointer
        background-color: hsl(180, 29%, 50%)
        color: white
        padding: 10px 7px
        display: flex
        justify-content: center
        border-radius: 0 5px 5px 0
        img
          pointer-events: none
  .clear
    text-decoration: underline
    cursor: pointer
    color: hsl(180, 29%, 50%)
</style>