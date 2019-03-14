<template>
  <div class="content">
    <button class="add-to-cart" @click="addToCart()">Add to Cart</button>
    <div class="top-row">
      <div :class="[saleBorderClass, 'top', 'part']">
        <div class="robot-name">
          {{ selectedRobot.head.title }}
          <span v-if="selectedRobot.head.onSale" class="sale">Sale!</span>
        </div>
        <img :src="selectedRobot.head.src" title="head">
        <button @click="selectPreviouseHead()" class="prev-selector">&#9668;</button>
        <button @click="selectNextHead()" class="next-selector">&#9658;</button>
      </div>
    </div>
    <div class="middle-row">
      <div class="left part">
        <img :src="selectedRobot.leftArm.src" title="left arm">
        <button @click="selectPreviouseLeftArm()" class="prev-selector">&#9650;</button>
        <button @click="selectNextLeftArm()" class="next-selector">&#9660;</button>
      </div>
      <div class="center part">
        <img :src="selectedRobot.torsos.src" title="left arm">
        <button @click="selectPreviouseTorsos()" class="prev-selector">&#9668;</button>
        <button @click="selectNextTorsos()" class="next-selector">&#9658;</button>
      </div>
      <div class="right part">
        <img :src="selectedRobot.rightArm.src" title="left arm">
        <button @click="selectPreviouseRightArm()" class="prev-selector">&#9650;</button>
        <button @click="selectNextRightArm()" class="next-selector">&#9660;</button>
      </div>
    </div>
    <div class="bottom-row">
      <div class="bottom part">
        <img :src="selectedRobot.bases.src" title="left arm">
        <button @click="selectPreviouseBases()" class="prev-selector">&#9668;</button>
        <button @click="selectNextBases()" class="next-selector">&#9658;</button>
      </div>
    </div>
    <div>
      <h1>
        <table>
          <thead>
            <tr>
              <th>Robot</th>
              <th class="cost">Cost</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(robot, index) in cart" :key="index">
              <td>{{robot.head.title}}</td>
              <td class="cost">{{robot.cost}}</td>
            </tr>
          </tbody>
        </table>
      </h1>
    </div>
  </div>
</template>

<script>
// import { Component, Prop, Vue } from 'vue-property-decorator';
import availableParts from '../../data/parts';
import createdHookMixin from './created-hook-mixin';

function getPreviouseValidIndex(index, length) {
  const deprecatedIndex = index - 1;
  return deprecatedIndex < 0 ? length - 1 : deprecatedIndex;
}

function getNextValidIndex(index, length) {
  const incrementedIndex = index + 1;
  return incrementedIndex > length - 1 ? 0 : incrementedIndex;
}

export default {
  name: 'RobotBuildComponent',
  data() {
    return {
      availableParts,
      cart: [],
      selectedHeadIndex: 0,
      selectedLeftArmIndex: 0,
      selectedTorsosIndex: 0,
      selectedRightArmIndex: 0,
      selectedBasesIndex: 0,
    };
  },
  mixins: [createdHookMixin],
  computed: {
    saleBorderClass() {
      return this.selectedRobot.head.onSale ? 'sale-border' : '';
    },
    selectedRobot() {
      return {
        head: availableParts.heads[this.selectedHeadIndex],
        leftArm: availableParts.arms[this.selectedLeftArmIndex],
        torsos: availableParts.torsos[this.selectedTorsosIndex],
        rightArm: availableParts.arms[this.selectedRightArmIndex],
        bases: availableParts.bases[this.selectedBasesIndex],
      };
    },
  },
  methods: {
    addToCart() {
      const robot = this.selectedRobot;
      const cost = robot.head.cost
        + robot.leftArm.cost
        + robot.torsos.cost
        + robot.rightArm.cost
        + robot.bases.cost;
      this.cart.push(Object.assign({}, robot, { cost }));
    },
    // Change head
    selectNextHead() {
      this.selectedHeadIndex = getNextValidIndex(
        this.selectedHeadIndex,
        availableParts.heads.length,
      );
    },
    selectPreviouseHead() {
      this.selectedHeadIndex = getPreviouseValidIndex(
        this.selectedHeadIndex,
        availableParts.heads.length,
      );
    },
    // Change Left Arm
    selectNextLeftArm() {
      this.selectedLeftArmIndex = getNextValidIndex(
        this.selectedLeftArmIndex,
        availableParts.arms.length,
      );
    },
    selectPreviouseLeftArm() {
      this.selectedLeftArmIndex = getPreviouseValidIndex(
        this.selectedLeftArmIndex,
        availableParts.arms.length,
      );
    },
    // Change Torsos
    selectNextTorsos() {
      this.selectedTorsosIndex = getNextValidIndex(
        this.selectedTorsosIndex,
        availableParts.torsos.length,
      );
    },
    selectPreviouseTorsos() {
      this.selectedTorsosIndex = getPreviouseValidIndex(
        this.selectedTorsosIndex,
        availableParts.torsos.length,
      );
    },
    // Change Right Arm
    selectNextRightArm() {
      this.selectedRightArmIndex = getNextValidIndex(
        this.selectedRightArmIndex,
        availableParts.torsos.length,
      );
    },
    selectPreviouseRightArm() {
      this.selectedRightArmIndex = getPreviouseValidIndex(
        this.selectedRightArmIndex,
        availableParts.torsos.length,
      );
    },
    // Change Bases
    selectNextBases() {
      this.selectedBasesIndex = getNextValidIndex(
        this.selectedBasesIndex,
        availableParts.torsos.length,
      );
    },
    selectPreviouseBases() {
      this.selectedBasesIndex = getPreviouseValidIndex(
        this.selectedBasesIndex,
        availableParts.torsos.length,
      );
    },
  },
};
</script>

<style lang="scss">
.test-class {
  background: green;
}
.part {
  position: relative;
  width: 165px;
  height: 165px;
  border: 3px solid #aaa;
}
.part img {
  width: 165px;
}
.top-row {
  display: flex;
  justify-content: space-around;
}
.middle-row {
  display: flex;
  justify-content: center;
}
.bottom-row {
  display: flex;
  justify-content: space-around;
  border-top: none;
}
.head {
  border-bottom: none;
}
.left {
  border-right: none;
}
.right {
  border-left: none;
}
.left img {
  transform: rotate(-90deg);
}
.right img {
  transform: rotate(90deg);
}
.bottom {
  border-top: none;
}
.prev-selector {
  position: absolute;
  z-index: 1;
  top: -3px;
  left: -28px;
  width: 25px;
  height: 171px;
}
.next-selector {
  position: absolute;
  z-index: 1;
  top: -3px;
  right: -28px;
  width: 25px;
  height: 171px;
}
.center .prev-selector,
.center .next-selector {
  opacity: 0.8;
}
.left .prev-selector {
  top: -28px;
  left: -3px;
  width: 144px;
  height: 25px;
}
.left .next-selector {
  top: auto;
  bottom: -28px;
  left: -3px;
  width: 144px;
  height: 25px;
}
.right .prev-selector {
  top: -28px;
  left: 24px;
  width: 144px;
  height: 25px;
}
.right .next-selector {
  top: auto;
  bottom: -28px;
  left: 24px;
  width: 144px;
  height: 25px;
}
.right .next-selector {
  right: -3px;
}
.robot-name {
  position: absolute;
  top: -25px;
  text-align: center;
  width: 100%;
}
.sale {
  color: red;
}

.content {
  position: relative;
}

.add-to-cart {
  position: absolute;
  right: 30px;
  width: 220px;
  padding: 3px;
  font-size: 13px;
}

td,
th {
  text-align: left;
  padding: 5px;
  padding-right: 20px;
  font-size: 12px;
}
.cost {
  text-align: right;
}
.sale-border {
  border: 3px solid red;
}
.avarage-border {
  border: 3px solid #aaa;
}
</style>
