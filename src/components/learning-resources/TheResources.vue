<template>
  <base-card>
    <base-button
      v-on:click="setSelectedTab('stored-resources')"
      v-bind:mode="storedResButtonMode">Stored Resources</base-button>
    <base-button
      v-on:click="setSelectedTab('add-resource')"
      v-bind:mode="addResButtonMode">Add Resource</base-button>
  </base-card>
  <keep-alive>
    <component v-bind:is="selectedTab"></component>
  </keep-alive>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';
export default {
  components: { StoredResources, AddResource },
  data: function() {
    return {
      selectedTab: 'stored-resources',
      storedResources: [
        {
          id: 'official-guide',
          title: 'Official Guide',
          description: 'The official Vue.js documentation',
          link: 'https://vuejs.org'
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Learn how to use Google...',
          link: 'https://google.com'
        }
      ]
    };
  },
  provide: function() {
    return {
      resources: this.storedResources,
      addResource: this.addResource
    };
  },
  computed: {
    storedResButtonMode() {
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    }
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addResource(title, description, url) {
      const newResource = {
        id: new Date().toISOString(),
        title: title,
        description: description,
        link: url
      };

      this.storedResources.unshift(newResource);
      this.selectedTab = 'stored-resources';
    }
  }
};
</script>

<style></style>
