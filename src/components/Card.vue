<template>
  <div v-bind:class="[showEmpty ? 'frame-card' : 'frame-card-hover']">
    <img v-if='showCard' v-bind:src=imgPath>
    <div v-if='showEmptyTemp' class='temp'/>
    <div v-if='showEmptyFinished' class='finished'>
      <div class='center'>A</div>
    </div>
  </div>
</template>

<script>
import { cSlotTypes, cCards } from '../common/constants';

export default {
  name: 'Card',
  props: {
    pCardID: Number,
    pSlotType: Number,
  },
  data() {
    return {
      curCardID: this.pCardID,
      curSlotType: this.pSlotType,
      slotTypes: cSlotTypes,
    };
  },
  computed: {
    imgPath() {
      return `./static/${cCards(this.pCardID)}`;
    },
    showCard() {
      return ((this.pSlotType === this.slotTypes.normal) || (this.pCardID > 0));
    },
    showEmptyTemp() {
      return ((this.pSlotType === this.slotTypes.temp)
          && (!this.pCardID || this.pCardID <= 0));
    },
    showEmptyFinished() {
      return ((this.pSlotType === this.slotTypes.finished)
          && (!this.pCardID || this.pCardID <= 0));
    },
    showEmpty() {
      return this.showEmptyTemp || this.showEmptyFinished;
    },
  },
};
</script>

<style lang="scss" scoped>
@import '../styles/_variables.scss';

.frame-card {
  width: $card-width;
  height: $card-height;
  &-hover:hover {
    border-radius: 11px;
    box-shadow: 0 0 0 3px orange;
  }
}
.temp {
  width: $card-width;
  height: $card-height;
  border: 2px solid $color-card-line;
  border-radius: 10px;
}
.finished {
  width: $card-width;
  height: $card-height;
  border: 2px solid $color-card-line;
  border-radius: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  .center {
    font-size: 72px;
    color: $color-card-line;
    transform: translateX(5px);
  }
}
</style>
