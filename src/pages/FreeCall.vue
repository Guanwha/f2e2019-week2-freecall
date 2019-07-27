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
          <!-- temp area -->
          <div class="area-temp">
            <div draggable="true"
                 @drop="drop($event, tempSlotID0)"
                 @dragover.prevent
                 @dragstart="dragStart($event, tempSlotID0, 0)"
                 @dragend="dragEnd($event)">
              <Card v-bind:pCardID='tempSlotCard(0)' v-bind:pSlotType='slotTypes.temp'/>
            </div>
            <div draggable="true"
                 @drop="drop($event, tempSlotID1)"
                 @dragover.prevent
                 @dragstart="dragStart($event, tempSlotID1, 0)"
                 @dragend="dragEnd($event)">
              <Card v-bind:pCardID='tempSlotCard(1)' v-bind:pSlotType='slotTypes.temp'/>
            </div>
            <div draggable="true"
                 @drop="drop($event, tempSlotID2)"
                 @dragover.prevent
                 @dragstart="dragStart($event, tempSlotID2, 0)"
                 @dragend="dragEnd($event)">
              <Card v-bind:pCardID='tempSlotCard(2)' v-bind:pSlotType='slotTypes.temp'/>
            </div>
            <div draggable="true"
                 @drop="drop($event, tempSlotID3)"
                 @dragover.prevent
                 @dragstart="dragStart($event, tempSlotID3, 0)"
                 @dragend="dragEnd($event)">
              <Card v-bind:pCardID='tempSlotCard(3)' v-bind:pSlotType='slotTypes.temp'/>
            </div>
          </div>
          <!-- finished area -->
          <div class="area-finished">
            <div draggable="true"
                 @drop="drop($event, finishedSlotID0)"
                 @dragover.prevent
                 @dragstart="dragStart($event, finishedSlotID0, finishSlotTopCardIdx(0))"
                 @dragend="dragEnd($event)">
              <Card v-bind:pCardID='finishSlotTopCard(0)' v-bind:pSlotType='slotTypes.finished'/>
            </div>
            <div draggable="true"
                 @drop="drop($event, finishedSlotID1)"
                 @dragover.prevent
                 @dragstart="dragStart($event, finishedSlotID1, finishSlotTopCardIdx(1))"
                 @dragend="dragEnd($event)">
              <Card v-bind:pCardID='finishSlotTopCard(1)' v-bind:pSlotType='slotTypes.finished'/>
            </div>
            <div draggable="true"
                 @drop="drop($event, finishedSlotID2)"
                 @dragover.prevent
                 @dragstart="dragStart($event, finishedSlotID2, finishSlotTopCardIdx(2))"
                 @dragend="dragEnd($event)">
              <Card v-bind:pCardID='finishSlotTopCard(2)' v-bind:pSlotType='slotTypes.finished'/>
            </div>
            <div draggable="true"
                 @drop="drop($event, finishedSlotID3)"
                 @dragover.prevent
                 @dragstart="dragStart($event, finishedSlotID3, finishSlotTopCardIdx(3))"
                 @dragend="dragEnd($event)">
              <Card v-bind:pCardID='finishSlotTopCard(3)' v-bind:pSlotType='slotTypes.finished'/>
            </div>
          </div>
        </div>
        <div class="playarea-lower">
          <!-- play area -->
          <div class="lower-left">
            <div class="area-play"
                 @drop="drop($event, playSlotID0)"
                 @dragover.prevent>
              <div v-for="(cardID, index) in cardsPlay[0]"
                   v-bind:key="index"
                   v-bind:style="{position: 'absolute', top: cardShiftY(index)}"
                   draggable="true"
                   @dragstart="dragStart($event, playSlotID0, index)"
                   @dragend="dragEnd($event)">
                <Card v-bind:pCardID="cardID"
                      v-bind:pSlotType="slotTypes.normal"/>
              </div>
            </div>
            <div class="area-play"
                 @drop="drop($event, playSlotID1)"
                 @dragover.prevent>
              <div v-for="(cardID, index) in cardsPlay[1]"
                   v-bind:key="index"
                   v-bind:style="{position: 'absolute', top: cardShiftY(index)}"
                   draggable="true"
                   @dragstart="dragStart($event, playSlotID1, index)"
                   @dragend="dragEnd($event)">
                <Card v-bind:pCardID="cardID"
                      v-bind:pSlotType="slotTypes.normal"/>
              </div>
            </div>
            <div class="area-play"
                 @drop="drop($event, playSlotID2)"
                 @dragover.prevent>
              <div v-for="(cardID, index) in cardsPlay[2]"
                   v-bind:key="index"
                   v-bind:style="{position: 'absolute', top: cardShiftY(index)}"
                   draggable="true"
                   @dragstart="dragStart($event, playSlotID2, index)"
                   @dragend="dragEnd($event)">
                <Card v-bind:pCardID="cardID"
                      v-bind:pSlotType="slotTypes.normal"/>
              </div>
            </div>
            <div class="area-play"
                 @drop="drop($event, playSlotID3)"
                 @dragover.prevent>
              <div v-for="(cardID, index) in cardsPlay[3]"
                   v-bind:key="index"
                   v-bind:style="{position: 'absolute', top: cardShiftY(index)}"
                   draggable="true"
                   @dragstart="dragStart($event, playSlotID3, index)"
                   @dragend="dragEnd($event)">
                <Card v-bind:pCardID="cardID"
                      v-bind:pSlotType="slotTypes.normal"/>
              </div>
            </div>
          </div>
          <div class="lower-right">
            <div class="area-play"
                 @drop="drop($event, playSlotID4)"
                 @dragover.prevent>
              <div v-for="(cardID, index) in cardsPlay[4]"
                   v-bind:key="index"
                   v-bind:style="{position: 'absolute', top: cardShiftY(index)}"
                   draggable="true"
                   @dragstart="dragStart($event, playSlotID4, index)"
                   @dragend="dragEnd($event)">
                <Card v-bind:pCardID="cardID"
                      v-bind:pSlotType="slotTypes.normal"/>
              </div>
            </div>
            <div class="area-play"
                 @drop="drop($event, playSlotID5)"
                 @dragover.prevent>
              <div v-for="(cardID, index) in cardsPlay[5]"
                   v-bind:key="index"
                   v-bind:style="{position: 'absolute', top: cardShiftY(index)}"
                   draggable="true"
                   @dragstart="dragStart($event, playSlotID5, index)"
                   @dragend="dragEnd($event)">
                <Card v-bind:pCardID="cardID"
                      v-bind:pSlotType="slotTypes.normal"/>
              </div>
            </div>
            <div class="area-play"
                 @drop="drop($event, playSlotID6)"
                 @dragover.prevent>
              <div v-for="(cardID, index) in cardsPlay[6]"
                   v-bind:key="index"
                   v-bind:style="{position: 'absolute', top: cardShiftY(index)}"
                   draggable="true"
                   @dragstart="dragStart($event, playSlotID6, index)"
                   @dragend="dragEnd($event)">
                <Card v-bind:pCardID="cardID"
                      v-bind:pSlotType="slotTypes.normal"/>
              </div>
            </div>
            <div class="area-play"
                 @drop="drop($event, playSlotID7)"
                 @dragover.prevent>
              <div v-for="(cardID, index) in cardsPlay[7]"
                   v-bind:key="index"
                   v-bind:style="{position: 'absolute', top: cardShiftY(index)}"
                   draggable="true"
                   @dragstart="dragStart($event, playSlotID7, index)"
                   @dragend="dragEnd($event)">
                <Card v-bind:pCardID="cardID"
                      v-bind:pSlotType="slotTypes.normal"/>
              </div>
            </div>
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
      playSlotID0: 0,
      playSlotID1: 1,
      playSlotID2: 2,
      playSlotID3: 3,
      playSlotID4: 4,
      playSlotID5: 5,
      playSlotID6: 6,
      playSlotID7: 7,
      finishedSlotID0: 8,
      finishedSlotID1: 9,
      finishedSlotID2: 10,
      finishedSlotID3: 11,
      tempSlotID0: 12,
      tempSlotID1: 13,
      tempSlotID2: 14,
      tempSlotID3: 15,
      cardsTemp: this.clearTempCards(),
      cardsFinished: this.clearFinishedCards(),
      cardsPlay: this.newGame(),
      cardsDragging: {
        fromSlotID: -1,
        cardIdx: -1,
      },
      slotTypes: cSlotTypes,

      playTime: 0,            // play time (unit: second)
      steps: 0,               // used steps number
    };
  },
  methods: {
    tempSlotCard(i) {
      return this.cardsTemp[i][0];
    },
    finishSlotTopCardIdx(i) {
      return this.cardsFinished[i].length - 1;
    },
    finishSlotTopCard(i) {
      const idx = this.cardsFinished[i].length - 1;
      return this.cardsFinished[i][idx];
    },
    cardShiftY(idx) {
      return (idx) ? `${37 * idx}px` : 0;
    },
    // drag & drop
    // -- slotID: source slot ID
    // -- cardIdx: card index in this slot
    dragStart(event, slotID, cardIdx) {
      const fromSlot = this.getSlot(slotID);
      // skip empty source slot
      if (!fromSlot || !fromSlot[cardIdx]) {
        event.preventDefault();
        return;
      }
      // remember this source slot and card index
      this.cardsDragging.fromSlotID = slotID;
      this.cardsDragging.cardIdx = cardIdx;
    },
    dragEnd(event) {
      event.dataTransfer.clearData();
    },
    // -- slotID: target slot ID
    drop(event, slotID) {
      if (slotID === this.cardsDragging.fromSlotID) return;     // skip source === target

      if (slotID <= this.playSlotID7) {
        // target slot is in play area
        const startIdx = this.cardsDragging.cardIdx;
        const fromSlotID = this.cardsDragging.fromSlotID;
        const fromSlot = this.getSlot(fromSlotID);
        const toSlot = this.getSlot(slotID);
        // -- move from source to target
        if (fromSlotID <= this.playSlotID7) {
          // from play slot to play slot
          for (let i = startIdx; i < fromSlot.length; i += 1) {
            toSlot.push(fromSlot[i]);
            fromSlot.splice(i, 1);
            i -= 1;
            // console.log(`${JSON.stringify(fromSlot)} -- ${JSON.stringify(toSlot)}`);
          }
        }
        else if (fromSlotID <= this.finishedSlotID3) {
          // from finished slot to play slot
          toSlot.push(fromSlot[fromSlot.length - 1]);
          fromSlot.pop();
        }
        else if (fromSlotID <= this.tempSlotID3) {
          // from temp slot to play slot
          toSlot.push(fromSlot[0]);
          fromSlot.pop();
        }
      }
      else if (slotID <= this.finishedSlotID3) {
        // target slot is in finished area
        const startIdx = this.cardsDragging.cardIdx;
        const fromSlot = this.getSlot(this.cardsDragging.fromSlotID);
        if (startIdx < fromSlot.length - 1) return;       // skip if source has over 2 cards
        // -- from any slot to finished slot
        this.cardsFinished[slotID - this.finishedSlotID0].push(fromSlot[fromSlot.length - 1]);
        fromSlot.pop();
      }
      else if (slotID <= this.tempSlotID3) {
        // target slot is in temp area
        const startIdx = this.cardsDragging.cardIdx;
        const fromSlot = this.getSlot(this.cardsDragging.fromSlotID);
        if (startIdx < fromSlot.length - 1) return;        // skip if dragging over 2 cards
        // -- from any slot to temp slot
        const tempSlotID = slotID - this.tempSlotID0;
        if (this.cardsTemp[tempSlotID][0]) return;         // skip if target has a card
        this.cardsTemp[tempSlotID][0] = fromSlot[fromSlot.length - 1];
        fromSlot.pop();
      }
    },
    // calcuation functions
    getSlot(slotID) {
      if (slotID < 0) return null;
      if (slotID <= this.playSlotID7) {
        return this.cardsPlay[slotID];
      }
      else if (slotID <= this.finishedSlotID3) {
        return this.cardsFinished[slotID - this.finishedSlotID0];
      }
      else if (slotID <= this.tempSlotID3) {
        return this.cardsTemp[slotID - this.tempSlotID0];
      }
      return null;
    },
    // generate new game
    clearTempCards() {
      return [[], [], [], []];
    },
    clearFinishedCards() {
      return [[], [], [], []];
    },
    newGame() {
      // initialize
      let i;
      const cardsPlay = [];
      for (i = 0; i < 8; i += 1) {
        cardsPlay[i] = [];
      }

      // random to generate new game
      const cards = [];
      let count = 52;
      for (i = 0; i < count; i += 1) {
        cards.push(i + 1);
      }
      let slotIdx;
      let cardIdx;
      let randIdx;
      let nCards;
      for (slotIdx = 0; slotIdx < 8; slotIdx += 1) {
        nCards = (slotIdx < 4) ? 7 : 6;
        for (cardIdx = 0; cardIdx < nCards; cardIdx += 1) {
          randIdx = Math.floor(Math.random() * count);
          // randIdx = count - 1;
          cardsPlay[slotIdx][cardIdx] = cards[randIdx];
          cards.splice(randIdx, 1);
          count -= 1;
        }
      }
      // console.log(cardsPlay);

      return cardsPlay;
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
    height: $card-height;
    flex-shrink: 0;
    margin: 30px 85px 0 85px;
    display: flex;
  }
  &-lower {
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
  width: $card-width;
  height: 100%;
  background: purple;
  position: relative;
}
</style>

