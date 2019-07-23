<template>
  <div class="frame-main">
    <!-- main play area -->
    <div class="main">
      <div class="main-header"/>
      <div class="main-playarea">
        <div class="playarea-upper">
          <div class="area-temp">
            <div class="card"/>
            <div class="card"/>
            <div class="card"/>
            <div class="card"/>
          </div>
          <div class="area-finished">
            <div class="card"/>
            <div class="card"/>
            <div class="card"/>
            <div class="card"/>
          </div>
        </div>
        <div class="playarea-lower"/>
      </div>
      <div class="main-footer"/>
    </div>
    <!-- dialog -->
  </div>
</template>

<script>
export default {
  name: 'FreeCall',
  data() {
    return {
      cards_temp: [],
      cards_finished: {
        1: [],
        2: [],
        3: [],
        4: [],
      },
      cards_play: {
        1: [],
        2: [],
        3: [],
        4: [],
        5: [],
        6: [],
        7: [],
        8: [],
      },
    };
  },
};
</script>

<style scoped lang="scss">
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
    height: 67px;
    background: red;
    flex-shrink: 0;
    display: flex;
    justify-content: space-between;
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
    background: blue;
    flex-shrink: 0;
  }
}
.playarea {
  &-upper {
    height: 145px;
    // background: yellow;
    flex-shrink: 0;
    margin: 30px 85px 0 85px;
    display: flex;
  }
  &-lower {
    // background: lightgreen;
    flex-grow: 1;
  }
}
.area {
  &-temp {
    width: 50%;
    height: 100%;
    // background: orange;
    margin-right: 43px;
    display: flex;
    justify-content: space-between;
  }
  &-finished {
    width: 50%;
    height: 100%;
    // background: orangered;
    margin-left: 43px;
    display: flex;
    justify-content: space-between;
  }
}
.card {
  width: 110px;
  height: 145px;
  border: 2px solid #665e58;
  border-radius: 10px;
}
</style>

