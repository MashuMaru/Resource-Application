<template>
    <ul>
      <LearningResource
        v-for="res in resources"
        v-bind:key="res.id"
        v-bind:id="res.id"
        v-bind:title="res.title"
        v-bind:description="res.description"
        v-bind:link="res.link"
      />
    </ul>
</template>

<script>
import LearningResource from './LearningResource.vue';

export default {
  components: { LearningResource },
  inject: ['resources']
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>
