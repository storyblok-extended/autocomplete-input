<template>
  <div class="container">
    <h2>{{ title }}</h2>
    <autocomplete
      placeholder="Search for icon"
      input-class="uk-input"
      :source="icons"
      @selected="chooseIcon"
    >
    </autocomplete>
  </div>
</template>

<script>
import Autocomplete from "vuejs-auto-complete";

export default {
  mixins: [window.Storyblok.plugin],
  components: { Autocomplete },
  data: function() {
    return {
      title: "Autocomplete plugin",
      icons: []
    };
  },
  methods: {
    chooseIcon(event) {
      this.$emit("changed-model", event.selectedObject);
    },
    initWith() {
      return {
        // needs to be equal to your storyblok plugin name
        plugin: "autocomplete-input"
      };
    },
    async pluginCreated() {
      // eslint-disable-next-line
      const {
        data: { datasource_entries }
      } = await this.api.get(
        `cdn/datasource_entries?datasource=${this.options.datasource_name}`
      );
      this.icons = datasource_entries;
    }
  },
};
</script>

<style>
.container {
  display: flex;
  flex-direction: column;
  height: 200px;
}
</style>
