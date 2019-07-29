
<template>
  <div class="container">  
    <div class="translucent"></div>  
    <div class="content">
      <div class="outer-dialog">
        <div class="inner-dialog">
          <div class="title"><img src="../assets/word-congratulations.svg"></div>
          <div class="buttons">
            <button @click.prevent="$emit('restart-game')">Restart</button>
            <button @click.prevent="$emit('new-game')">New Game</button>
          </div>
        </div>
      </div>  
    </div>
  </div>  
</template>

<script>
export default {
  name: 'DialogFinished',
};
</script>

<style lang="scss" scoped>
@import '../styles/_variables.scss';

.container {   
  position: absolute; /* make any positioned child elements relative to this */  
  width: 100%;
  height: 100%;
  left: 0;
  top: 0;
  z-index: 2;
}  
.translucent {
  width: 100%;
  height: 100%;
  position: absolute;
  background-color: $color-black;  
  opacity: 0.5;  
  -moz-opacity: 0.5;  
  filter:alpha(opacity=50);  
}  
.content {   
  width:100%;
  height: 100%;
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
}
.outer-dialog {
  width: 678px;
  height: 419px;
  border: 4px solid $color-black;
  border-radius: 10px;
  background: $color-white;
  display: flex;
  justify-content: center;
  align-items: center;
}
.inner-dialog {
  width: 663px;
  height: 405px;
  border: 4px solid $color-second;
  border-radius: 5px;
  background: $color-main;
  background-image: url("../assets/bg-congratulations.png");
  padding: 25px;
  display: flex;
  flex-direction: column;
  align-items: center;
  .title {
    margin-bottom: 30.21px;
  }
  .buttons {
    width: 424.75px;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
  }
  button {
    width: 191.75px;
    height: 39.65px;
    border: 3px solid $color-black;
    border-radius: 31px;
    background: $color-main-light;
    margin-top: 22px;
    color: $color-white;
    font-size: 0.75rem;
    font-family: 'Press Start 2P', cursive;
    outline-width: 0;
    &:hover {
      background: $color-second;
    }
  }
}

</style>
