<template>
  <div class="frame-main">
    <!-- main play area -->
    <div class="main">
      <div class="main-header">
        <div class='left'>
          <img src="../assets/logo-bk.svg">
        </div>
        <div class='middle'>
          <button v-bind:class="['menu', { disabled: false}]"/>
          <p>Time:{{playMinSec}}</p>
          <button v-bind:class="['undo', { disabled: noHistory}]"
                  v-bind:disabled="noHistory"
                  v-on:click.prevent="undo"/>
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
      // cardsPlay: [
      //   [],
      //   [39, 12, 37, 10, 35, 8, 33, 6, 31, 4, 29, 2, 27],
      //   [13, 38, 11, 36, 9, 34, 7, 32, 5, 30, 3, 28, 1],
      //   [40],
      //   [41],
      //   [43],
      //   [44],
      //   [45],
      // ],
      cardsDragging: {
        srcSlotID: -1,
        cardIdx: -1,
      },
      slotTypes: cSlotTypes,

      history: [],            // record each step ({ srcSlotID, cardIDs, tarSlotID })

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
    // -- srcSlotID: source slot ID
    // -- cardIdx: card index in this slot
    dragStart(event, srcSlotID, cardIdx) {
      const srcSlot = this.getSlot(srcSlotID);
      // skip
      if (!srcSlot || !srcSlot[cardIdx]                           // skip empty source slot
          || !this.canDrag(srcSlotID, cardIdx)) {                 // check dragging is fit the rule
        event.preventDefault();
        return;
      }
      // remember this source slot and card index
      this.cardsDragging.srcSlotID = srcSlotID;
      this.cardsDragging.cardIdx = cardIdx;
    },
    dragEnd(event) {
      event.dataTransfer.clearData();
    },
    // -- tarSlotID: target slot ID
    drop(event, tarSlotID) {
      if (tarSlotID === this.cardsDragging.srcSlotID) return;     // skip source === target

      if (tarSlotID <= this.playSlotID7) {
        // target slot is in play area
        const startIdx = this.cardsDragging.cardIdx;
        const srcSlotID = this.cardsDragging.srcSlotID;
        const srcSlot = this.getSlot(srcSlotID);
        const toSlot = this.getSlot(tarSlotID);
        // -- move from source to target
        if (srcSlotID <= this.playSlotID7) {
          // from play slot to play slot
          if (!this.canPlayToPlay((srcSlotID - this.playSlotID0),
                                  startIdx,
                                  tarSlotID - this.playSlotID0)) return;
          // -- push to history
          this.recordHistory(srcSlotID, startIdx, tarSlotID);
          // -- update cards
          for (let i = startIdx; i < srcSlot.length; i += 1) {
            toSlot.push(srcSlot[i]);
            srcSlot.splice(i, 1);
            i -= 1;
          }
        }
        else if (srcSlotID <= this.finishedSlotID3) {
          // from finished slot to play slot
          if (!this.canFinishedToPlay((srcSlotID - this.finishedSlotID0),
                                      startIdx,
                                      tarSlotID - this.playSlotID0)) return;
          // -- push to history
          this.recordHistory(srcSlotID, startIdx, tarSlotID);
          // -- update cards
          toSlot.push(srcSlot[srcSlot.length - 1]);
          srcSlot.pop();
        }
        else if (srcSlotID <= this.tempSlotID3) {
          // from temp slot to play slot
          if (!this.canTempToPlay((srcSlotID - this.tempSlotID0),
                                  tarSlotID - this.playSlotID0)) return;
          // -- push to history
          this.recordHistory(srcSlotID, startIdx, tarSlotID);
          // -- update cards
          toSlot.push(srcSlot[0]);
          srcSlot.pop();
        }
      }
      else if (tarSlotID <= this.finishedSlotID3) {
        // target slot is in finished area
        const startIdx = this.cardsDragging.cardIdx;
        const srcSlot = this.getSlot(this.cardsDragging.srcSlotID);
        const tarSlot = this.cardsFinished[tarSlotID - this.finishedSlotID0];
        if (!this.canAnyToFinished(srcSlot, startIdx, tarSlot)) return;
        // -- from any slot to finished slot
        // ---- push to history
        this.recordHistory(this.cardsDragging.srcSlotID, startIdx, tarSlotID);
        // ---- update cards
        this.cardsFinished[tarSlotID - this.finishedSlotID0].push(srcSlot[srcSlot.length - 1]);
        srcSlot.pop();
      }
      else if (tarSlotID <= this.tempSlotID3) {
        // target slot is in temp area
        const startIdx = this.cardsDragging.cardIdx;
        const srcSlot = this.getSlot(this.cardsDragging.srcSlotID);
        if (startIdx < srcSlot.length - 1) return;        // skip if dragging over 2 cards
        // -- from any slot to temp slot
        // ---- push to history
        this.recordHistory(this.cardsDragging.srcSlotID, startIdx, tarSlotID);
        // ---- update cards
        const tempSlotID = tarSlotID - this.tempSlotID0;
        if (this.cardsTemp[tempSlotID][0]) return;         // skip if target has a card
        this.cardsTemp[tempSlotID][0] = srcSlot[srcSlot.length - 1];
        srcSlot.pop();
      }
    },
    // get local id in play/finished/temp slot ID
    getLocalSlotID(slotID) {
      if (slotID < 0) return null;
      if (slotID <= this.playSlotID7) {
        return slotID - this.playSlotID0;
      }
      else if (slotID <= this.finishedSlotID3) {
        return slotID - this.finishedSlotID0;
      }
      else if (slotID <= this.tempSlotID3) {
        return slotID - this.tempSlotID0;
      }
      return null;
    },
    // get cards array according slot ID
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
    // check draggin cards number
    canDrag(srcSlotID, cardIdx) {
      // skip check if source slot isn't in play area
      if (srcSlotID > this.playSlotID7) return true;

      // check cards is sequential
      const playSlotID = this.getLocalSlotID(srcSlotID);
      if (!this.isSequentialCards(playSlotID, cardIdx)) return false;

      // check moved card number
      const nMovedCards = this.cardsPlay[playSlotID].length - cardIdx;
      let nEmptySlot = this.emptySlotNumber;
      nEmptySlot += 1;

      return (nMovedCards <= nEmptySlot);
    },
    isSequentialCards(playSlotID, cardIdx) {
      let i;
      let beFirst = true;
      let preCardInfo = {
        num: -1,        // card # (1~13)
        isRed: true,    // card color is red, or , is black
      };
      let cardInfo = {
        num: -1,        // card # (1~13)
        isRed: true,    // card color is red, or , is black
      };
      const cardSlot = this.cardsPlay[playSlotID];
      const nTotalCards = cardSlot.length;
      for (i = cardIdx; i < nTotalCards; i += 1) {
        cardInfo = this.analysisCard(cardSlot[i]);
        // don't check at first
        if (beFirst) {
          beFirst = false;
        }
        else if (!this.checkLinkRule(cardInfo, preCardInfo)) {
          return false;
        }

        preCardInfo = cardInfo;
      }
      return true;
    },
    analysisCard(cardID) {
      return {
        num: ((cardID - 1) % 13) + 1,
        isRed: (cardID <= 26),
      };
    },
    canPlayToPlay(srcPlaySlotID, cardIdx, tarPlaySlotID) {
      const sourceSlot = this.cardsPlay[srcPlaySlotID];
      const targetSlot = this.cardsPlay[tarPlaySlotID];
      if (targetSlot.length === 0) {
        // target slot is empty
        const nMovedCards = sourceSlot.length - cardIdx;
        const nEmptySlot = this.emptySlotNumber;
        return (nMovedCards <= nEmptySlot);
      }
      // target slot isn't empty
      const sourceCardInfo = this.analysisCard(sourceSlot[cardIdx]);
      const targetCardInfo = this.analysisCard(targetSlot[targetSlot.length - 1]);
      return this.checkLinkRule(sourceCardInfo, targetCardInfo);
    },
    canFinishedToPlay(srcFinishedSlotID, cardIdx, tarPlaySlotID) {
      const targetSlot = this.cardsPlay[tarPlaySlotID];
      if (targetSlot.length === 0) {
        // target slot is empty
        return true;
      }
      // target slot isn't empty
      const sourceSlot = this.cardsFinished[srcFinishedSlotID];
      const sourceCardInfo = this.analysisCard(sourceSlot[cardIdx]);
      const targetCardInfo = this.analysisCard(targetSlot[targetSlot.length - 1]);
      return this.checkLinkRule(sourceCardInfo, targetCardInfo);
    },
    canTempToPlay(srcTempSlotID, tarPlaySlotID) {
      const targetSlot = this.cardsPlay[tarPlaySlotID];
      if (targetSlot.length === 0) {
        // target slot is empty
        return true;
      }
      // target slot isn't empty
      const sourceSlot = this.cardsTemp[srcTempSlotID];
      const sourceCardInfo = this.analysisCard(sourceSlot[0]);
      const targetCardInfo = this.analysisCard(targetSlot[targetSlot.length - 1]);
      return this.checkLinkRule(sourceCardInfo, targetCardInfo);
    },
    // check source card can link to target card
    checkLinkRule(sourceCardInfo, targetCardInfo) {
      // check color
      if (targetCardInfo.isRed === sourceCardInfo.isRed) {
        return false;
      }
      // check number
      else if (targetCardInfo.num !== sourceCardInfo.num + 1) {
        return false;
      }
      return true;
    },
    canAnyToFinished(srcSlot, startIdx, tarSlot) {
      // skip if source has over 2 cards
      if (startIdx < srcSlot.length - 1) return false;

      // check link rule in finished slot
      if (tarSlot.length === 0) {
        // when finished slot is empty, source card must be 1
        if ((srcSlot[startIdx] - 1) % 13 !== 0) return false;
      }
      else {
        // when finished slot isn't empty, source card must be target card # + 1
        const srcCard = srcSlot[startIdx];
        const tarCard = tarSlot[tarSlot.length - 1];
        // -- check the card number
        if (srcCard !== tarCard + 1) return false;
        // -- check the card type
        if (((srcCard - 1) % 13 !== ((tarCard - 1) % 13) + 1)) return false;
      }
      return true;
    },
    recordHistory(srcSlotID, startIdx, tarSlotID) {
      let i;
      const cardIDs = [];
      const srcSlot = this.getSlot(srcSlotID);
      for (i = startIdx; i < srcSlot.length; i += 1) {
        cardIDs.push(srcSlot[i]);
      }
      const action = { srcSlotID, cardIDs, tarSlotID };
      this.history.push(action);
    },
    undo() {
      console.log('undo');
      if (this.history.length === 0) return;
      const action = this.history[this.history.length - 1];
      // remove target slot cards
      let i;
      const tarSlot = this.getSlot(action.tarSlotID);
      for (i = 0; i < tarSlot.length; i += 1) {
        if (action.cardIDs[0] === tarSlot[i]) {
          break;
        }
      }
      tarSlot.splice(i, tarSlot.length - i);
      // recover source slot cards
      const srcSlot = this.getSlot(action.srcSlotID);
      for (i = 0; i < action.cardIDs.length; i += 1) {
        srcSlot.push(action.cardIDs[i]);
      }
      this.history.pop();
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
    // calculate total empty number of temp/play slots
    emptySlotNumber() {
      let nEmptySlot = 0;
      let i;
      for (i = 0; i < 4; i += 1) {
        if (this.cardsTemp[i].length === 0) {
          nEmptySlot += 1;
        }
        if (this.cardsPlay[i].length === 0) {
          nEmptySlot += 1;
        }
      }
      for (i = 4; i < 8; i += 1) {
        if (this.cardsPlay[i].length === 0) {
          nEmptySlot += 1;
        }
      }

      return nEmptySlot;
    },
    noHistory() {
      return this.history.length === 0;
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
      .menu {
        width: 50px;
        height: 50px;
        background: url("../assets/btn-more.svg");
        border-width: 0;
        outline-width: 0;
        &:hover:not([disabled]) {
          filter: drop-shadow(0 0 10px red);
        }
      }
      .undo {
        width: 50px;
        height: 50px;
        background: url("../assets/btn-return.svg");
        border-width: 0;
        outline-width: 0;
        &:hover:not([disabled]) {
          filter: drop-shadow(0 0 10px red);
        }
      }
      .disabled {
        filter: grayscale(100%);
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

