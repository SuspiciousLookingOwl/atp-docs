<template>
  <div id="app">
    <app-header />
    <keep-alive>
      <router-view class="container mt-4" />
    </keep-alive>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import AppHeader from "@/components/AppHeader.vue";

@Component({
  components: { AppHeader }
})
export default class Home extends Vue {}
</script>
