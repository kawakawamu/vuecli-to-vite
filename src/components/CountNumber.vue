<template>
  <div class="count__wrapper">
    <AddButton @pushClassComponent="countUp"></AddButton>
    <PlayGound :countProp="countProp"></PlayGound>
    <v-progress-circular
      v-if="initLoading"
      indeterminate
      color="purple"
    ></v-progress-circular>
  </div>
</template>
<script lang="ts">
import { Vue, Component, Watch } from "vue-property-decorator";
import AddButton from "./Atoms/AddButton.vue";
import PlayGound from "./Atoms/PlayGound.vue";

@Component({
  components: {
    AddButton,
    PlayGound,
  },
})
export default class CountNumer extends Vue {
  countProp: number = 0;
  initLoading: boolean = true;
  countUp(): void {
    this.countProp++;
  }
  @Watch("countProp")
  finishCount(CountNumer: number): void {
    if (CountNumer > 10) {
      alert("リセットします！");
      this.countProp = 0;
    }
  }
  mounted(): void {
    setTimeout(() => {
      this.initLoading = false;
    }, 2000);
  }
}
</script>

<style>
button {
  margin: 10px;
  padding: 10px;
}
.count__wrapper {
  margin: 30px 100px;
}
</style>
