<template>
  <div id="app">
    <router-view :key="$route.fullPath" />
  </div>
</template>

<script>
export default {
  name: 'App',
  watch: {
    '$store.state.subject_id' (newSubjectId) {
      if (newSubjectId) {
        this.$store.dispatch('initializeHeartbeat') // ✅ Start heartbeat when subject_id is assigned
      }
    }
  },
  beforeDestroy () {
    this.$store.dispatch('terminateHeartbeat') // ✅ Stop heartbeat when app is closed
  }
}
</script>

<style>
/* Add global styles if needed */
input[type="radio"]:focus {
  outline: none !important;
  box-shadow: none !important;
  border-color: transparent !important;
  border-width: 0 !important;
}

/* Target Chrome/Edge/Safari native blue ring */
input[type="radio"]:focus::-webkit-focus-ring {
  outline: none !important;
  box-shadow: none !important;
  border: none !important;
}

</style>
