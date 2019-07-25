<template>
  <div class="frame-main">
    <!-- main play area -->
    <div class="main">
      <div class="main-header">
        <div class='left'>
          <img src="../assets/logo-bk.svg">
        </div>
        <div class='middle'>
          <img src="../assets/btn-more.svg">
          <p>Time:{{playMinSec}}</p>
          <img src="../assets/btn-return.svg">
        </div>
        <div class='right'>
          <img src="../assets/bone.svg">
          <p>Move: {{steps}}</p>
        </div>
      </div>
      <div class="main-playarea">
        <div class="playarea-upper">
          <div class="area-temp">
            <Card v-bind:pCardID='tempSlotCard(0)' v-bind:pSlotType='slotTypes.temp'/>
            <Card v-bind:pCardID='tempSlotCard(1)' v-bind:pSlotType='slotTypes.temp'/>
            <Card v-bind:pCardID='tempSlotCard(2)' v-bind:pSlotType='slotTypes.temp'/>
            <Card v-bind:pCardID='tempSlotCard(3)' v-bind:pSlotType='slotTypes.temp'/>
          </div>
          <div class="area-finished">
            <Card v-bind:pCardID='finishSlotTopCard(1)' v-bind:pSlotType='slotTypes.finished'/>
            <Card v-bind:pCardID='finishSlotTopCard(2)' v-bind:pSlotType='slotTypes.finished'/>
            <Card v-bind:pCardID='finishSlotTopCard(3)' v-bind:pSlotType='slotTypes.finished'/>
            <Card v-bind:pCardID='finishSlotTopCard(4)' v-bind:pSlotType='slotTypes.finished'/>
          </div>
        </div>
        <div class="playarea-lower">
          <div class="lower-left">
            <div class="area-play"/>
            <div class="area-play"/>
            <div class="area-play"/>
            <div class="area-play"/>
          </div>
          <div class="lower-right">
            <div class="area-play"/>
            <div class="area-play"/>
            <div class="area-play"/>
            <div class="area-play"/>
          </div>
        </div>
      </div>
      <div class="main-footer">
        <img class="left" src="../assets/bg-left.png">
        <div class="middle">
          <p>QUICKLY</p>
          <img src="../assets/bg-JQK.svg">
        </div>
        <img class="right" src="../assets/bg-right.png">
      </div>
    </div>
    <!-- dialog -->
  </div>
</template>

<script>
import Card from '../components/Card';
import { cSlotTypes } from '../common/constants';

export default {
  name: 'FreeCall',
  components: {
    Card,
  },
  data() {
    return {
      cardsTemp: [],
      cardsFinished: {
        1: [],
        2: [],
        3: [],
        4: [],
      },
      cardsPlay: {
        1: [],
        2: [],
        3: [],
        4: [],
        5: [],
        6: [],
        7: [],
        8: [],
      },
      slotTypes: cSlotTypes,

      playTime: 0,            // play time (unit: second)
      steps: 0,               // used steps number
    };
  },
  methods: {
    tempSlotCard(i) {
      return this.cardsTemp[i];
    },
    finishSlotTopCard(i) {
      const idx = this.cardsFinished[i].length - 1;
      return this.cardsFinished[i][idx];
    },
  },
  computed: {
    playMinSec() {
      const min = this.playTime % 60;
      const sec = this.playTime - (min * 60);
      if (min < 10) {
        return (sec < 10) ? `0${min}:0${sec}` : `0${min}:${sec}`;
      }
      return (sec < 10) ? `${min}:0${sec}` : `${min}:${sec}`;
    },
  },
};
</script>

<style scoped lang="scss">
@import '../styles/_variables.scss';

.frame-main {
  height: 100%;
  width: 1280px;
  margin: 0 auto;
}
.main {
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;

  &-header {
    margin-top: 35px;
    width: 100%;
    height: $height-header;
    flex-shrink: 0;
    display: flex;
    justify-content: space-between;
    .left {
      flex: 1;
      display: flex;
      justify-content: flex-start;
    }
    .middle {
      flex: 1;
      display: flex;
      justify-content: center;
      align-items: center;
      img {
        width: 50px;
        height: 50px;
      }
      p {
        font-size: $font-size-header;
        line-height: $font-size-header;
        color: $color-white;
      }
    }
    .right {
      flex: 1;
      display: flex;
      justify-content: flex-end;
      align-items: center;
      img {
        width: 37.22px;
        height: 41.63px;
      }
      p {
        font-size: $font-size-header;
        line-height: $height-header;
        color: $color-white;
        padding: 0 85px 0 8px;
      }
    }
  }
  &-playarea {
    width: 100%;
    min-height: 574px;
    // background: green;
    flex-grow: 1;
    display: flex;
    flex-direction: column;
  }
  &-footer {
    width: 100%;
    height: 124px;
    flex-shrink: 0;
    display: flex;
    justify-content: space-around;
    align-items: flex-end;
    .left {
      transform: translateY(1px);
    }
    .middle {
      transform: translateY(23px);
    }
    .right {
      transform: translateY(1px);
    }
    p {
      color: $color-white;
    }
  }
}
.playarea {
  &-upper {
    height: 145px;
    flex-shrink: 0;
    margin: 30px 85px 0 85px;
    display: flex;
  }
  &-lower {
    background: lightgreen;
    flex-grow: 1;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    padding: 19px 0 0 0;
  }
}
.area {
  &-temp {
    width: 50%;
    height: 100%;
    margin-right: 43px;
    display: flex;
    justify-content: space-between;
  }
  &-finished {
    width: 50%;
    height: 100%;
    margin-left: 43px;
    display: flex;
    justify-content: space-between;
  }
}
.lower-left {
  width: 50%;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  padding: 0 43px 0 85px;
}
.lower-right {
  width: 50%;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  padding: 0 85px 0 43px;
}
.area-play {
  width: 110px;
  height: 100%;
  background: purple;
}
</style>

