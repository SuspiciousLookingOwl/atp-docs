<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <router-link class="navbar-brand" to="/">Advanced TP</router-link>
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav mr-auto">
        <li
          v-for="link in links"
          :key="link.title"
          class="nav-item"
          :class="$route.name === link.to.name ? 'active' : ''"
        >
          <router-link :to="link.to" class="nav-link">
            {{ link.title }}
          </router-link>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component
export default class AppHeader extends Vue {
  public links = [
    {
      title: "Commands",
      to: {
        name: "commands"
      }
    }
  ];
}
</script>
