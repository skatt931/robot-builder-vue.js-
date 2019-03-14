<template>
  <div>
    <RobotBuildComponent/>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import RobotBuildComponent from '@/components/build/RobotBuildComponent.vue'; // @ is an alias to /src

@Component({
  components: {
    RobotBuildComponent,
  },
})
export default class BuildRobotView extends Vue {}
</script>
