<template>
  <div id="app">
    <div id='names' class='container' v-if='state'>
      <h1>Who pays the bill</h1>
      <div class='input_container'>
        <input type='text' v-model='inputName'/>
        <button @click='addNameToList'>ADD</button>
      </div>
      <div class='error_label' v-if='showError'>
        You must enter a name !!!
      </div>
      <div class='list_of_names'>
        <div v-for='(name, index) in names' :key='index' @click='removeName(index)'>
          {{name}}
        </div>
      </div>
      <div v-if='names.length > 1'>
        <div class='action_button' @click='showResults'>
          Check the loser
        </div>
      </div>
    </div>
    <div id='result' class='container' v-if='!state'>
      <div class='result_container'>
        <h1>The loser is:</h1>
        <div class='result_value'>{{result}}</div>
        <div class='action_button' @click='resetApp'>
          Start again
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      state: true,
      inputName: '',
      names: [],
      showError: false,
      result: '',
    }
  },
  methods: {
    addNameToList(){
      if(this.validate(this.inputName)){
        this.names.push(this.inputName)
        this.inputName = ''
        this.showError = false
      }else{
        this.showError = true
      }
    },
    validate(value){
      if(value !== ''){
        return true
      }else {
        return false
      }
    },
    showResults(){
      let rand = this.names[Math.floor(Math.random() * this.names.length)]
      this.result = rand

      this.state = false
    },
    resetApp(){
      this.state = true
      this.names = []
      this.result = ''
    },
    removeName(index){
      this.names.splice(index,1)
    },
  }
}
</script>

<style>
body {
    font-family: 'Roboto', sans-serif;
    padding:0;
    margin:0;
  }
  
a {
    text-decoration: none;
    color:#ffffff;
}
  
.container {
    min-height: 300px;
    width: 360px;
    position: absolute;
    left: 50%;
    top: 50%;
    -webkit-transform: translate(-50%, -50%);
    transform: translate(-50%, -50%);
}

h1 {
    color: #2196F3;
    font-size: 40px;
    text-align: center;
}

.input_container {
    display: flex;
}
input:focus{
    outline: none;
}
input {
        flex-grow: 1;
        border: 1px solid #dddddd;
    background: #f2f2f2;
    font-size: 20px;
    border-radius: 5px 0px 0px 5px;
    padding: 10px;
    box-sizing: border-box;
}

button {
        border-radius: 0px 5px 5px 0px;
    background: #2196F3;
    color: #ffffff;
    font-size: 16px;
    padding: 10px;
    box-sizing: border-box;
}

.list_of_names {
    padding: 10px 0px;
    cursor: pointer;
}

.list_of_names div {
    margin-right: 10px;
    margin-bottom: 10px;
    background: #2196F3;
    color: #ffffff;
    display: inline-block;
    padding: 5px 10px;
    border-radius: 15px;
 }

 .error_label {
    color: #F44336;
    font-weight: 600;
    text-align: center;
    margin-top: 10px;
}

.action_button {
    cursor: pointer;
   border: 1px solid #607D8B;
   color: #607D8B;
   font-size: 16px;
   width: 200px;
   text-align: center;
   padding: 10px;
   border-radius: 11px;
   margin: 0 auto;
}

.action_button:hover {
   background: #607D8B;
   color:#ffffff;
}

.result_value {
    font-size: 70px;
    color: #607D8B;
    font-weight: 600;
    text-align: center;
    margin-bottom: 20px;
}
</style>
