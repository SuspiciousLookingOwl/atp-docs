<template>
  <div>
    <h4 class="text-center">Commands & Permission</h4>
    <label class="mr-1">Search:</label>
    <input v-model="keyword" type="text" label="Search" />
    <table class="table table-striped my-4">
      <thead>
        <tr>
          <th scope="col">Command</th>
          <th scope="col">Aliases</th>
          <th scope="col">Permission</th>
          <th scope="col">Description</th>
          <th scope="col">Syntax</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="command in filteredCommand" :key="command.name">
          <td v-html="highlight(command.name, keyword)" />
          <td>{{ command.aliases.join(",") }}</td>
          <td>
            <code v-html="highlight(command.permission, keyword)" />
          </td>
          <td v-html="highlight(command.description, keyword)" />
          <td>
            <code v-html="highlight(command.syntax, keyword)" />
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import commands from "@/assets/commands.json";

@Component
export default class AppHeader extends Vue {
  public commands = commands;
  public keyword = "";

  get filteredCommand() {
    const reg = this.getRegex(this.keyword);
    console.log(reg);
    return this.commands.filter(c => {
      return (
        c.name.match(reg) || c.permission.match(reg) || c.description.match(reg)
      );
    });
  }

  highlight(word: string, find: string): string {
    if (typeof word !== "string" || !find) return word;
    return word.replace(this.getRegex(find), "<mark>$1</mark>");
  }

  getRegex(keyword: string) {
    const keywords = keyword.split(/[\s]+/).filter(s => !!s);
    return new RegExp(`(${keywords.join("|")})`, "gi");
  }
}
</script>

<style>
mark {
  padding: 0 !important;
  margin: 0 !important;
}
</style>
