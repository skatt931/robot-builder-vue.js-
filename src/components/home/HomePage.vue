<template>
  <div class="home">
    <div>
      <img src="../../assets/robot-home.png" alt="robot" class="robot">
    </div>
    <div class="get-started">
      <router-link to="/build">Get started</router-link> building your first robot!
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class HomePage extends Vue {
  @Prop() private msg!: string;
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  .home {
    text-align: center;
  }

  .robot {
    height: 300px;
  }

</style>
