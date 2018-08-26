<template>
  <div class="container">
    <div class="content-main" @mousemove="moveMouse" :style="{backgroundColor: color}">
        <div class="input" v-if="!wrapper" >
          <input type="text" name="" id="input-name" placeholder="Enter your name" autofocus v-model="name" v-on:keyup.enter.stop="onInput()">
          <transition name="errormsg">
            <p v-if="name.length > 1 && name.length < 4" class="error-msg">Warning: {{ errorMessage }}</p>
          </transition>
        </div>
        <transition name="effect" >
          <div class="wrapper" v-if="wrapper">
            <div class="welcome">
              <p class="welcome-text">Welcome <br> <span class="name-text"> {{ name }} </span></p>
            </div>
            <div class="buttons">
              <p class="temperature-text">Select your temperature</p>
              <button 
                class="hot-button"
                @click="onHotBtn">Hot</button>
              <button 
                class="cold-button"
                @click="onColdBtn">Cold</button>
            </div>
            <!-- <input type="text" v-model="color"> -->
          </div>
        </transition>
      </div>
    </div>
</template>

<script>
  export default {
  data() {
    return {
      name: '',
      wrapper: false,
      bgColors: {
        bgRed: false,
        bgBlue: false,
      },
      x: 0,
      color: '',
      errorMessage: 'You have to input at least 4 characters'
    }
  },
  methods: {
    //Checking name input values
    onInput() {
      if(this.name.length < 4){
        this.wrapper
      } 
      else {
        this.wrapper = !this.wrapper
      } 
    },
    colorRed () {
      //RGB red where R is static - 255 and 'g' 'b' are getting values from x coordinate
        let r = 255
        let g = Math.round(this.x/12)
        let b = Math.round(this.x/12)
        return 'rgb(' + r + ',' + g + ',' + b + ')'
    },
    colorBlue () {
      //RGB red where B is static - 255 and 'r' 'g' are getting values from x coordinate
        let r = Math.round(this.x/12)
        let g = Math.round(this.x/12)
        let b = 255
        return 'rgb(' + r + ',' + g + ',' + b + ')'
    },
    onHotBtn () {
      this.bgColors.bgRed = true;
      this.bgColors.bgBlue = false;
      this.color = this.colorRed()
    },
    onColdBtn () {
      this.bgColors.bgBlue = true;
      this.bgColors.bgRed = false;
      this.color = this.colorBlue()
    },
    ifBtnClicked() {
      if(this.bgColors.bgRed){
        this.color = this.colorRed()
      }
      if(this.bgColors.bgBlue){
        this.color = this.colorBlue()
      }
    },
    moveMouse (e) {
      //On mouse move start ifBtnClicked event to change color by getting coordinate X
      this.ifBtnClicked()
      this.x = e.clientX
    }
  }
}
</script>

<style lang="sass" scoped>
  @import '../assets/scss/homepage.sass'
</style>
