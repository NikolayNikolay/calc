<template>
 <div class="wrapper">
   <main class="block">
    <div class="block__container">
      <div class="calculartor">
        <div
        class="calculartor__display">{{num}}</div>
        <div class="calculartor__keyboard keyboard">
          <div class="keyboard__calculation1">
            <div
            @click.stop="delet"
            class="circle">AC</div>
            <div 
            @click="absMath"
            class="circle circle_plus-minus">/</div>
            <div
            @click="getOperators('%')"
            class="circle">%</div>
            <div 
            @click="getOperators('/')"
            class="circle circle_division circle_green"><span></span></div>
          </div>
          <div class="keyboard__number">
            <div
            @click.stop="getKey($event)"
            class="circle">7</div>
            <div
            @click.stop="getKey($event)"
            class="circle">8</div>
            <div
            @click.stop="getKey($event)"
            class="circle">9</div>
            <div
            @click.stop="getKey($event)"
            class="circle">6</div>
            <div
            @click.stop="getKey($event)"
            class="circle">5</div>
            <div
            @click.stop="getKey($event)"
            class="circle">4</div>
            <div
            @click.stop="getKey($event)"
            class="circle">3</div>
            <div 
            @click.stop="getKey($event)"
            class="circle">2</div>
            <div
            @click.stop="getKey($event)"
            class="circle">1</div>
            <div
            @click.stop="getKey($event)"
            class="circle circle_null">0</div>
            <div
            @click.stop="getKey($event)" 
            class="circle">.</div>
          </div>
          <div class="keyboard__calculation2">            
            <div
            @click="getOperators('*')"
            class="circle circle_green">x</div>
            <div
            @click="getOperators('-')"
            class="circle circle_green">-</div>
            <div 
            @click="getOperators('+')"
            class="circle circle_green">+</div>
            <div
            @click="equals"
            class="circle circle_green">=</div>
          </div>
        </div>
      </div>
    </div>
  </main>
</div>
</template>

<script>
export default {
  name: 'CalculatorNew',
  data(){
    return{
      num:0,
      arr:[],
    }
  },
  methods:{
    getKey(event){
      console.log(typeof this.num === 'number');
      console.log(this.num.length);
      if (typeof this.num === 'number') {
        this.num = String(event.target.innerText)
      }else if (this.num.length < 9 ) {
        this.num += event.target.innerText;
      }
    },
    delet(){
      if (this.num.length - 1 === 0) {
        this.num = 0;
      }
      this.num = String(this.num.slice(0, -1));
    },
    getOperators(elem){
      if (this.num.length < 9 ) {
        this.num += String(elem);
      }
      
    },
    equals(){
      if (this.num.indexOf('%') !== -1) {
        console.log(this.num.indexOf('%'));
        let result = this.num.split('')
        result[this.num.indexOf('%')] = ' '
        let arr = result.join('').split(' ')
        let [a,b] = arr;
        this.num = String(+a / +b * 100);
      }else{
        let sum = eval(this.num);
        this.num = String(sum);
      }
    },
    absMath(){
      this.num = String(Math.abs(Number(this.num)))
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.wrapper{
  background: #5E6367;
  min-height: 100vh;
  overflow: hidden;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
}
.block {
  flex: 1 0 auto;
		// .block__container
		&__container {
      height: 100vh;
      max-width: 1400px;
      padding: 0px 15px;
      margin: 0 auto;
      display: flex;
      align-items: center;
      justify-content: center;
		}
}
.calculartor {
  width: 190px;
  height: 310px;
  border-radius: 25px;
  overflow: hidden;
  &__display{
    height: 75px;
    display: flex;
    align-items: center;
    justify-content: end;
    background: linear-gradient(134.31deg, rgba(255, 255, 255, 0.2) -9.79%, rgba(255, 255, 255, 0.072) 56.48%, rgba(255, 255, 255, 0) 58.82%), #151515;
    padding: 16px 16px;
    font-weight: 200;
    font-size: 36px;
    line-height: 43px;
    color: #fff;
  }
  &__keyboard {

		}
}
.keyboard {
  display: flex;
  flex-wrap: wrap;
  column-gap: 10px;
  row-gap: 10px;
  padding: 10px 10px;
  background: radial-gradient(138.51% 138.51% at -8.68% -37.02%, #575757 0%, #353535 100%) /* warning: gradient uses a rotation that is not supported by CSS and may not behave as expected */;
box-shadow: 0px 4px 4px -2px rgba(0, 0, 0, 0.25), inset 4px 4px 4px rgba(255, 255, 255, 0.03), inset 1px 1px 0px rgba(255, 255, 255, 0.08);
		// .keyboard__calculation1
		&__calculation1 {
      display: flex;
      column-gap: 10px;
      flex:1 0 100% ;
		}

		// .keyboard__number

		&__number {
      display: flex;
      flex-wrap: wrap;
      column-gap: 10px;
      row-gap: 10px;
      flex: 0 0 74%;
		}

		// .keyboard__calculation2

		&__calculation2 {
      display: flex;
      flex-direction: column;
      row-gap: 10px;
      flex: 0 0 34px;
		}
}
.circle{
  display: flex;
  align-items: center;
  justify-content: center;
  flex: 0 0 35px;
  height: 34px;
  background: #000;
  background: radial-gradient(100% 100% at 87.14% 100%, rgba(119, 119, 119, 0.46) 0%, rgba(56, 54, 54, 0.85) 100%) /* warning: gradient uses a rotation that is not supported by CSS and may not behave as expected */;
box-shadow: 0px 0px 0px 1px #212121, 5px 8px 4px -2px rgba(0, 0, 0, 0.16), -2px -2px 4px rgba(255, 255, 255, 0.05), inset 1px 3px 4px rgba(0, 0, 0, 0.25);
border-radius: 24px;
font-weight: 300;
font-size: 19px;
line-height: 23px;
color: #E0E0E0;
text-shadow: 0px -1px 1px rgba(0, 0, 0, 0.8);
cursor: pointer;
&:active{
  background: url('../img/Frame.png');
}
}
.circle_plus-minus{
&::after{
  content: '-';
}
&::before{
  content: '+';
  font-size: 15px;
}
}
.circle_division{
  flex-direction: column;
  row-gap: 3px;
  span{
    width: 15px;
    height: 2px;
    background: #E0E0E0;
  }
  &::before{
    content: '';
    width: 3px;
    height: 3px;
    background: #E0E0E0;
    border-radius: 50%;
  }
    &::after{
    content: '';
    width: 3px;
    height: 3px;
    background: #E0E0E0;
    border-radius: 50%;
  }
}
.circle_green{
  background: linear-gradient(0deg, #00FFD1, #00FFD1), radial-gradient(100% 100% at 87.14% 100%, rgba(119, 119, 119, 0.46) 0%, rgba(56, 54, 54, 0.85) 100%) /* warning: gradient uses a rotation that is not supported by CSS and may not behave as expected */;
background-blend-mode: multiply, normal;
box-shadow: 0px 0px 0px 1px #212121, 5px 8px 4px -2px rgba(0, 0, 0, 0.16), -2px -2px 4px rgba(255, 255, 255, 0.05), inset 1px 3px 4px rgba(0, 0, 0, 0.25);
}
.circle_null{
  flex: 0 0 80px;
  &:active{
  background: none;
}
}
</style>
