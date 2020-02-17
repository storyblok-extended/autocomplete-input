<template>
  <div class="container">
    <h2>{{title}}</h2>
    <p>autocomplete input plugin</p>
  </div>
</template>

<script>
export default {
  mixins: [window.Storyblok.plugin],
  data: function() {
    return {
      title: "Autocomplete plugin"
    };
  },
  methods: {
    initWith() {
      return {
        // needs to be equal to your storyblok plugin name
        plugin: "autocomplete-input"
      };
    },
    pluginCreated() {
      // eslint-disable-next-line
      console.log(
        "View source and customize: https://github.com/storyblok/storyblok-fieldtype"
      );
    }
  },
  mounted() {
    console.log(this);
  },
  watch: {
    model: {
      handler: function(value) {
        this.$emit("changed-model", value);
      },
      deep: true
    }
  }
};
</script>

<style>
.container {
  display: flex;
  flex-direction: column;
}
</style>
