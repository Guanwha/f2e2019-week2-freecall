
<template>
  <div class="container">  
    <div class="translucent"></div>  
    <div class="content">
      <div class="outer-dialog">
        <div class="inner-dialog">
          <div><img src="../assets/word-new-game.png"></div>
          <button @click.prevent="$emit('new-game')">Start a New Game</button>
        </div>
      </div>  
    </div>
  </div>  
</template>

<script>
export default {
  name: 'DialogNewGame',
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
  height: 269px;
  border: 4px solid $color-black;
  border-radius: 10px;
  background: $color-white;
  display: flex;
  justify-content: center;
  align-items: center;
}
.inner-dialog {
  width: 663px;
  height: 255px;
  border: 4px solid $color-second;
  border-radius: 5px;
  background: $color-main;
  padding: 25px;
  display: flex;
  flex-direction: column;
  align-items: center;
  button {
    width: 432px;
    height: 62px;
    border: 3px solid $color-black;
    border-radius: 31px;
    background: $color-main-light;
    margin-top: 52.21px;
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
