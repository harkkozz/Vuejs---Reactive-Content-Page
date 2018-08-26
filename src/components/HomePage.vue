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
      errorMessage: 'You have to input 4 characters'
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
$bgColor: #bdbdbd
$hotBtnColor: #ff6666
$coldBtnColor: #6666ff
$resp-width: 760px

.content-main
  position: fixed
  width: 100%
  height: 100%
  left: 0
  top: 0
  padding: 2%
  background: $bgColor
  z-index: 1

@media screen and (max-width: $resp-width) 
  .buttons 
    resize: both

@media screen and (max-width: $resp-width) 
  .content-main 
    font-size: 30px
    padding: 0

@media screen and (max-width: $resp-width)
  .error-msg
    font-size: 10px

.hot-button
  background-color: $hotBtnColor
  color: white
  font-size: 25px
  font-weight: bold
  padding-top: 65px
  width: 10%
  height: 170px
  border: 2px solid red
  outline: 0

@media screen and (max-width:760px) 
  .hot-button 
    font-size: 15px
    height: 100px

.cold-button 
  background-color: $coldBtnColor
  color: white
  font-size: 25px
  font-weight: bold
  padding-top: 65px
  width: 10%
  height: 170px
  border: 2px solid blue
  outline: 0

@media screen and (max-width:760px) 
  .cold-button 
    font-size: 15px
    height: 100px

.effect-enter-active, .effect-leave-active 
  transition: opacity 0.5s
.effect-enter, .effect-leave-to .effect-leave-active 
  opacity: 0

.errormsg-enter-active, .errormsg-leave-active
  transition: opacity 0.5s
.errormsg-enter, .errormsg-leave-to .errormsg-leave-active 
  opacity: 0

.welcome-text 
  font-size: 30px
  color: white

.name-text 
  font-size: 40px
  color: white

.error-msg
  font-size: 20px
  color: #990000
  text-decoration: underline

.temperature-text 
  font-size: 25px
  margin-top: 40px
  color: white

#input-name
  outline: none
  color: white
  background:  $bgColor
  border-style: none
  font-size: 40px

::placeholder
  font-size: 20px
  color: white
</style>
