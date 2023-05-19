<script>
  import TagInput from "./components/TagInput.vue"

  export default{
    components: {
      TagInput,
    },
    methods: {
      handleOnTagsChange(tags){
        console.log(tags)
      }
    }
  }

</script>

<template>
  <TagInput @onTagsChange="handleOnTagsChange"></TagInput>
</template>

<style scoped>

</style>
