<template>
  <div>
    <app-new></app-new>
    <app-Vacabulary></app-Vacabulary>
    <app-list></app-list>
  </div>
</template>

<script>
import NewWordForm from "./NewWordForm.vue";
import Vacabulary from "./Vacabulary.vue";
import OwnList from "./OwnList.vue";
export default {
  components: {
    appNew: NewWordForm,
    appVacabulary: Vacabulary,
    appList: OwnList
  }
};
</script>

<style></style>
