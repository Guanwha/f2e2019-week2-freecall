<template>
  <div class="frame-main">
    <!-- main play area -->
    <div class="main">
      <div class="main-header">
        <div class='left'>
          <img src="../assets/logo-bk.svg">
        </div>
        <div class='middle'>
          <button v-bind:class="['menu', { disabled: false}]"
                  v-on:click.prevent="findHint"/>
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
                 @dragend="dragEnd($event)"
                 @click.prevent="autoMove(tempSlotID0, 0)">
              <Card v-bind:pCardID='tempSlotCard(0)' v-bind:pSlotType='slotTypes.temp'/>
            </div>
            <div draggable="true"
                 @drop="drop($event, tempSlotID1)"
                 @dragover.prevent
                 @dragstart="dragStart($event, tempSlotID1, 0)"
                 @dragend="dragEnd($event)"
                 @click.prevent="autoMove(tempSlotID1, 0)">
              <Card v-bind:pCardID='tempSlotCard(1)' v-bind:pSlotType='slotTypes.temp'/>
            </div>
            <div draggable="true"
                 @drop="drop($event, tempSlotID2)"
                 @dragover.prevent
                 @dragstart="dragStart($event, tempSlotID2, 0)"
                 @dragend="dragEnd($event)"
                 @click.prevent="autoMove(tempSlotID2, 0)">
              <Card v-bind:pCardID='tempSlotCard(2)' v-bind:pSlotType='slotTypes.temp'/>
            </div>
            <div draggable="true"
                 @drop="drop($event, tempSlotID3)"
                 @dragover.prevent
                 @dragstart="dragStart($event, tempSlotID3, 0)"
                 @dragend="dragEnd($event)"
                 @click.prevent="autoMove(tempSlotID3, 0)">
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
                   @dragend="dragEnd($event)"
                   @click.prevent="autoMove(playSlotID0, index)">
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
                   @dragend="dragEnd($event)"
                   @click.prevent="autoMove(playSlotID1, index)">
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
                   @dragend="dragEnd($event)"
                   @click.prevent="autoMove(playSlotID2, index)">
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
                   @dragend="dragEnd($event)"
                   @click.prevent="autoMove(playSlotID3, index)">
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
                   @dragend="dragEnd($event)"
                   @click.prevent="autoMove(playSlotID4, index)">
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
                   @dragend="dragEnd($event)"
                   @click.prevent="autoMove(playSlotID5, index)">
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
                   @dragend="dragEnd($event)"
                   @click.prevent="autoMove(playSlotID6, index)">
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
                   @dragend="dragEnd($event)"
                   @click.prevent="autoMove(playSlotID7, index)">
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
    <DialogNewGame v-if="status === gameStatus.start" @new-game="newGame"/>
  </div>
</template>

<script>
import Card from '../components/Card';
import DialogNewGame from '../components/DialogNewGame';
import { cSlotTypes, cGameStatus } from '../common/constants';

export default {
  name: 'FreeCall',
  components: {
    Card,
    DialogNewGame,
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
      cardsPlay: [[], [], [], [], [], [], [], []],
      // cardsPlay: [
      //   [3, 28],
      //   [39, 1, 37, 10, 35, 8, 33, 6, 31, 4, 29, 2],
      //   [13, 3, 11, 36, 9, 34, 7, 32, 5, 30],
      //   [46],
      //   [],
      //   [17],
      //   [44],
      //   [45],
      // ],
      // cardsPlay: [
      //   [7, 6, 5, 4, 3, 2, 1],
      //   [19, 18, 17, 16, 15, 14],
      //   [33, 32, 31, 30, 29, 28, 27],
      //   [45, 44, 43, 42, 41, 40],
      //   [13, 12, 11, 10, 9, 8],
      //   [26, 25, 24, 23, 22, 21, 20],
      //   [39, 38, 37, 36, 35, 34],
      //   [52, 51, 50, 49, 48, 47, 46],
      // ],
      cardsDragging: {
        srcSlotID: -1,
        cardIdx: -1,
      },
      slotTypes: cSlotTypes,

      // game help
      history: [],            // record each step ({ srcSlotID, cardIDs, tarSlotID })
      hint: {},               // hint ({ srcSlotID, cardIDs, tarSlotID })

      // game flow
      gameStatus: cGameStatus,
      status: cGameStatus.start,  // game status

      // game data
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
          this.steps += 1;
          // -- auto-detect
          this.autoDetect();
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
          this.steps += 1;
          // -- auto-detect
          this.autoDetect();
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
          this.steps += 1;
          // -- auto-detect
          this.autoDetect();
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
        this.steps += 1;
        // -- auto-detect
        this.autoDetect();
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
        this.steps += 1;
        // -- auto-detect
        this.autoDetect();
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

      // start to accumulate the play time
      this.status = this.gameStatus.playing;
      this.playTime = 0;
      this.accumulateTime();

      this.cardsPlay = cardsPlay;
    },
    // accumulate the play time
    accumulateTime() {
      setTimeout(() => {
        this.playTime += 1;
        this.accumulateTime();
      }, 1000);
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
    checkLinkRule(smallerCardInfo, largerCardInfo) {
      // check color
      if (largerCardInfo.isRed === smallerCardInfo.isRed) {
        return false;
      }
      // check number
      else if (largerCardInfo.num !== smallerCardInfo.num + 1) {
        return false;
      }
      return true;
    },
    canAnyToFinished(srcSlot, startIdx, tarSlot) {
      // skip if moved cards has over 2 cards
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
    recordHistoryFromHint() {
      this.history.push(this.hint);
    },
    undo() {
      if (this.history.length === 0) return;
      const action = this.history[this.history.length - 1];
      this.undoAction(action);
      this.history.pop();
    },
    undoAction(action) {
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
    },
    findHint() {
      if (this.findHintFromTempToFinished()     // check temp card can move to finished slot
       || this.findHintFromPlayToFinished()     // check play card can move move to finished slot
       || this.findHintFromPlayToPlay()         // check play card can move to another play slot
       || this.findHintFromTempToPlay()         // check temp card can move to play slot
       || this.findHintFromPlayToTemp()) {      // check play card can move to temp slot
        alert(`${this.hint.srcSlotID} --> ${this.hint.tarSlotID} with ${this.hint.cardIDs.length} cards (${this.hint.cardIDs})`);
        return true;
      }

      alert('hint not found');
      return false;
    },
    findHintFromTempToFinished() {
      let i;
      this.hint = { srcSlotID: -1, cardIDs: [], tarSlotID: -1 };
      for (i = 0; i < 4; i += 1) {
        if (this.findHintFromOneTempToFinished(i)) return true;
      }
      return false;
    },
    findHintFromOneTempToFinished(tempSlotID) {
      const i = tempSlotID;
      const tempSlot = this.cardsTemp[i];
      let j;
      if (tempSlot.length === 1) {
        // temp slot has a card
        for (j = 0; j < 4; j += 1) {
          if (this.cardsFinished[j].length === 0) {
            // finished slot is empty
            if ((tempSlot[0] - 1) % 13 === 0) {
              // found
              this.setHint(this[`tempSlotID${i}`], [tempSlot[0]], this[`finishedSlotID${j}`]);
              return true;
            }
          }
          else {
            // finished slot has any card
            const finishedSlot = this.getSlot(this[`finishedSlotID${j}`]);
            if (this.canAnyToFinished(tempSlot, 0, finishedSlot)) {
              // found
              this.setHint(this[`tempSlotID${i}`], [tempSlot[0]], this[`finishedSlotID${j}`]);
              return true;
            }
          }
        }
      }
      return false;
    },
    findHintFromPlayToFinished() {
      let i;
      this.hint = { srcSlotID: -1, cardIDs: [], tarSlotID: -1 };
      for (i = 0; i < 8; i += 1) {
        if (this.findHintFromOnePlayToFinished(i)) return true;
      }
      return false;
    },
    findHintFromOnePlayToFinished(playSlotID) {
      const i = playSlotID;
      const playSlot = this.cardsPlay[i];
      let j;
      if (playSlot.length > 0) {      // play slot has any card
        const tailCardID = playSlot[playSlot.length - 1];

        for (j = 0; j < 4; j += 1) {
          if (this.cardsFinished[j].length === 0) {
            // finished slot is empty
            if ((tailCardID - 1) % 13 === 0) {
              // found
              this.setHint(this[`playSlotID${i}`], [tailCardID], this[`finishedSlotID${j}`]);
              return true;
            }
          }
          else {
            // finished slot has any card
            const finishedSlot = this.getSlot(this[`finishedSlotID${j}`]);
            if (this.canAnyToFinished(playSlot, playSlot.length - 1, finishedSlot)) {
              // found
              this.setHint(this[`playSlotID${i}`], [tailCardID], this[`finishedSlotID${j}`]);
              return true;
            }
          }
        }
      }
      return false;
    },
    findHintFromPlayToPlay() {
      let i;
      this.hint = { srcSlotID: -1, cardIDs: [], tarSlotID: -1 };
      for (i = 0; i < 8; i += 1) {
        if (this.cardsPlay[i].length > 0) {
          // play slot has any card
          const startIdx = this.findPlaySlotSequentialHead(i);
          if (this.findHintFromOnePlayCardToPlay(i, startIdx)) return true;
        }
      }
      return false;
    },
    findHintFromOnePlayCardToPlay(playSlotID, startIdx) {
      const i = playSlotID;
      const srcPlaySlot = this.cardsPlay[i];
      let j;
      // loop from startIdx to the bottom
      let iCard;    // card index from startIdx to the bottom in the play slot
      for (iCard = startIdx; iCard < srcPlaySlot.length; iCard += 1) {
        // loop for target play-slot
        for (j = 0; j < 8; j += 1) {
          if (this.canDrag(i + this.playSlotID0, iCard) && this.canPlayToPlay(i, iCard, j)) {
            // found
            const cardIDs = [];
            for (let k = iCard; k < srcPlaySlot.length; k += 1) {
              cardIDs.push(srcPlaySlot[k]);
            }
            this.setHint(this[`playSlotID${i}`], cardIDs, this[`playSlotID${j}`]);
            return true;
          }
        }
      }
      return false;
    },
    findHintFromTempToPlay() {
      let i;
      this.hint = { srcSlotID: -1, cardIDs: [], tarSlotID: -1 };
      for (i = 0; i < 4; i += 1) {
        if (this.findHintFromOneTempToPlay(i)) return true;
      }
      return false;
    },
    findHintFromOneTempToPlay(tempSlotID) {
      const i = tempSlotID;
      const tempSlot = this.cardsTemp[i];
      let j;
      if (tempSlot.length === 1) {
        // temp slot has a card
        for (j = 0; j < 8; j += 1) {
          if (this.cardsPlay[j].length > 0) {
            // play slot has any card
            if (this.canTempToPlay(i, j)) {
              // found
              this.setHint(this[`tempSlotID${i}`], [tempSlot[0]], this[`playSlotID${j}`]);
              return true;
            }
          }
          else {
            // found
            this.setHint(this[`tempSlotID${i}`], [tempSlot[0]], this[`playSlotID${j}`]);
            return true;
          }
        }
      }
      return false;
    },
    findHintFromPlayToTemp() {
      let i;
      this.hint = { srcSlotID: -1, cardIDs: [], tarSlotID: -1 };
      for (i = 0; i < 8; i += 1) {
        if (this.findHintFromOnePlayToTemp(i)) return true;
      }
      return false;
    },
    findHintFromOnePlayToTemp(playSlotID) {
      const i = playSlotID;
      const playSlot = this.cardsPlay[i];
      let j;
      if (playSlot.length > 0) {      // play slot has any card
        const tailCardID = playSlot[playSlot.length - 1];

        for (j = 0; j < 4; j += 1) {
          if (this.cardsTemp[j].length === 0) {
            // found
            this.setHint(this[`playSlotID${i}`], [tailCardID], this[`tempSlotID${j}`]);
            return true;
          }
        }
      }
      return false;
    },
    setHint(srcSlotID, cardIDs, tarSlotID) {
      this.hint = { srcSlotID, cardIDs, tarSlotID };
    },
    // playSlotID must be valid
    findPlaySlotSequentialHead(playSlotID) {
      let i = -1;
      let beFirst = true;
      let preCardInfo = {};
      let cardInfo = {};
      const cardSlot = this.cardsPlay[playSlotID];
      const nTotalCards = cardSlot.length;
      // check from bottom to top
      for (i = nTotalCards - 1; i >= 0; i -= 1) {
        cardInfo = this.analysisCard(cardSlot[i]);
        // don't check at first
        if (beFirst) {
          beFirst = false;
        }
        else if (!this.checkLinkRule(preCardInfo, cardInfo)) {
          // discontinous card found
          break;
        }

        preCardInfo = cardInfo;
      }

      return i + 1;
    },
    autoMove(slotID, cardIdx) {
      if (slotID < 0) return;
      if (slotID <= this.playSlotID7) {
        // play slot
        if (this.autoMoveFromPlay((slotID - this.playSlotID0), cardIdx)) {
          console.log(this.hint);
          this.doAction(this.hint);
          this.recordHistoryFromHint();
          this.steps += 1;
          // -- auto-detect
          this.autoDetect();
        }
      }
      else if (slotID >= this.tempSlotID0 && slotID <= this.tempSlotID3) {
        // temp slot
        if (this.autoMoveFromTemp(slotID - this.tempSlotID0)) {
          console.log(this.hint);
          this.doAction(this.hint);
          this.recordHistoryFromHint();
          this.steps += 1;
          // -- auto-detect
          this.autoDetect();
        }
      }
    },
    autoMoveFromPlay(playSlotID, cardIdx) {
      const isBottomCard = ((this.cardsPlay[playSlotID].length - cardIdx) === 1);
      if (isBottomCard && this.findHintFromOnePlayToFinished(playSlotID)) return true;
      if (this.findHintFromOnePlayCardToPlay(playSlotID, cardIdx)) return true;
      if (isBottomCard && this.findHintFromOnePlayToTemp(playSlotID)) return true;
      return false;
    },
    autoMoveFromTemp(tempSlotID) {
      if (this.findHintFromOneTempToFinished(tempSlotID)) return true;
      if (this.findHintFromOneTempToPlay(tempSlotID)) return true;
      return false;
    },
    doAction(action) {
      // remove source slot cards
      let i;
      const srcSlot = this.getSlot(action.srcSlotID);
      for (i = 0; i < srcSlot.length; i += 1) {
        if (action.cardIDs[0] === srcSlot[i]) {
          break;
        }
      }
      srcSlot.splice(i, srcSlot.length - i);
      // recover target slot cards
      const tarSlot = this.getSlot(action.tarSlotID);
      for (i = 0; i < action.cardIDs.length; i += 1) {
        tarSlot.push(action.cardIDs[i]);
      }
    },
    autoDetect() {
      setTimeout(() => {
        if (this.findHintFromTempToFinished()
        || this.findHintFromPlayToFinished()) {
          console.log(this.hint);
          this.doAction(this.hint);
          this.recordHistoryFromHint();
          // -- auto-detect
          this.autoDetect();
        }
      }, 100);
    },
  },
  computed: {
    playMinSec() {
      const min = parseInt((this.playTime / 60), 10);
      const sec = parseInt((this.playTime % 60), 10);
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
  position: relative;
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
    z-index: 1;
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
  position: relative;
}
</style>

