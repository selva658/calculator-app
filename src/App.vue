<template>
<div id="calculator">
  <h1>Calculator</h1>
  <div id="display">
    <input type="text" :value="userenter" />
  </div>
  
  <div id="buttons">
    <div class="button number" v-for="x in numbers" value="x" @click='getnum(x)' :key="x">
    
      {{ x }}
   
    </div>
    <div class="button" @click='add' >+</div>
    <div class="button" @click="subtrat">-</div>
    <div class="button" @click="multiple">*</div>
    <div class="button" @click='divide'>/</div>
    <div class="button" @click="modulo">%</div>
    <div class="button" @click="total" :disabled="!equalcheck" >=</div>
     <div class="button2" @click="clear"></div>
    <div class="button1" @click="clear">C</div>
     <div class="button1" @click="dot">.</div>
    <div class="button" @click="undo">↩</div>
     <div class="button2" @click="clear"></div>
  </div>
</div>
 

</template>

<script>

export default{
  data(){
    return {
    numbers: [...Array(10).keys()],
    userenter:'',
    output:0,
    dotindex:0,
    fordot:'',
    equalcheck:false
    }
  },
  methods:{
  getnum(x){
    this.userenter+=x
  },
  check(s){
    if(this.userenter[this.userenter.length-1]=='+' || this.userenter[this.userenter.length-1]=='-' || this.userenter[this.userenter.length-1]=='*' || this.userenter[this.userenter.length-1]=='/' || this.userenter[this.userenter.length-1]=='%' || this.userenter[this.userenter.length-1]=='√') {
     //
    //  this.equalcheck=false
    }
    else{
       this.userenter+=s
      // this.equalcheck=true
    }
  },
  add(){
    this.check('+')
  },
  subtrat(){
    this.check('-')
  },
  multiple(){
    this.check('*')
  },
  divide(){
    this.check('/')
  },
  modulo(){
    this.check('%')
  },
  clear(){
    this.userenter=''
  },
  dot(){
     this.userenter+='.'
  },
  undo(){
     this.userenter=this.userenter.substr(0, this.userenter.length - 1)
  },  
  total(){
    let operators=[]
    let fianl=[]
    let k=0
    this.fordot+=this.userenter[this.dotindex]

    //spliting all entered values based on '+,-,*,%,/'

    let all=(this.userenter.split(/[\\+\-/%\\*]/))
   
    //storing operators'+,-,*,%,/' in []
    for(let i=0;i<this.userenter.length;i++){
      if(this.userenter[i]=='+'){
         operators.push('+')
      }
      else if(this.userenter[i]=='-'){
        operators.push('-')
      }
      else if(this.userenter[i]=='*'){
        operators.push('*')
      }
      else if(this.userenter[i]=='/'){
        operators.push('/')
      }
      else if(this.userenter[i]=='%'){
        operators.push('%')
      }
    }
    
    //storing numbers next operators next to each like ['12','+','9','-','8']
    for(let j=0;j<all.length;j++){
      if(j%2==1){
        fianl.push(all[j])
        fianl.push(operators[k])
        k++
        
      }
      else{
        fianl.push(all[j])
        fianl.push(operators[k])
        k++
      }
    }
    this.output+=Number(fianl[0])



   //fianloutput
   for(let m=0;m<fianl.length;m++){
    
    if(fianl[m]==="+"){
      //
      this.output+=Number(fianl[m+1])
    }
    else if(fianl[m]==='-'){
      this.output-=Number(fianl[m+1])
    }
    else if(fianl[m]==='*'){
      this.output*=Number(fianl[m+1])
    }
     else if(fianl[m]==='/'){
      this.output/=Number(fianl[m+1])
    }
     else if(fianl[m]==='%'){
      this.output%=Number(fianl[m+1])
    }
   }
    this.userenter=this.output
    this.output=0
  }
  },
  computed:{
    col(){
      return this.equalcheck?'green':'red'
    }
  }
}
</script>

<style>
body{
  background-image: url(https://cdn1.vectorstock.com/i/1000x1000/17/50/abstract-background-calculator-vector-11601750.jpg);
  overflow-y: hidden;
  overflow-x: hidden;
}
#calculator {
  padding: 20px;
  width: 300px;
  border:1px solid rgb(117, 202, 191);
  margin: auto;
  border-radius: 10px;
  margin-top:7%;
  background-color: white;
  box-shadow: rgba(0, 0, 0, 0.25) 0px 54px 55px, rgba(0, 0, 0, 0.12) 0px -12px 30px, rgba(0, 0, 0, 0.12) 0px 4px 6px, rgba(0, 0, 0, 0.17) 0px 12px 13px, rgba(0, 0, 0, 0.09) 0px -3px 5px;
}

#display {
  width: 100%;
  margin-bottom: 20px;
}

#display input {
  width: 100%;
  height: 30px;
  text-align: right;
  border-radius:5px ;
  border:1px solid rgb(117, 202, 191)
}

input:focus{
        outline: none;
}

h1{
 margin-left: 25%;
}

#buttons {
  display: grid;
  gap: 10px;
  grid-template-columns: auto auto auto auto;
  order: -1;
}

#buttons .button, .button1 {
  padding: 10px;
  border: 1px solid rgb(117, 202, 191);
  border-radius: 5px;
  text-align: center;
  cursor: pointer;
  font-weight: bold; 
}

#buttons .button.number {
  font-weight: bold;
}

#buttons .button:hover {
  background-color: lightblue;
}

.button2{
  border:none
}

</style>

