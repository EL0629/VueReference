<template>
  <q-page padding>
    <!-- using counter event -->
    <button style="position: absolute; right: 10px"
    @click="counter++">{{counter}}</button>
    
    
    <h5>I Love Vue.js</h5>

    <!-- storing data using one way binding method -->
    <h5>{{ message }}</h5>

    <!-- two way binding method -->
    <input v-model="message"/>

    <!-- using event and methods -->
    <button @click="clearMessage">Clear</button>

    <!-- using keyup event -->

    <input v-model="message"  @keyup="handleKeyup"/>
    <br>

    <!-- shortcut using keyup event -->

    <input v-model="keyup"  
    @keyup.esc="clearMessage"
    @keyup.enter="alertMessage"/>
    <br>

    <!-- using mouse enter event -->
    <input v-model="mouseEnter" @mouseenter="alertMessage"/>
    

    <!-- using v-show directive -->
    <h5 class="border-grey" v-show="message.length">{{ vshow }}</h5>

    <!-- using v-if directive -->
    <h5 class="border-grey" v-if="message.length">{{ vif }}</h5>

    <!-- using v-else directive -->
    <!-- show when v-if is false -->
    <h5 v-else>{{ velse }}</h5>

    <!-- using method funtion -->
    <p>Uppercase message: {{messageUppercase()}} </p>

    <!-- using computed funtion -->
    <p>Uppercase message: {{messageUppercasecomputed}} </p>

    <!-- using filter funtion -->
    <p>Lowercase message: {{message | messageLowercase}} </p>


    <!-- append counter in computed property -->
    <p>Uppercase message: {{messageUppercasecomputedappend}} </p>


    <!-- creating a own directive autofocus -->
    <input v-model="message"  @keyup="handleKeyup" v-autofocus/>

    <br>

    <!-- conditional style v-bind-->   
    <input v-model="message" v-bind:class="{'error' : message.length > 22}"/>

    <br>

    <!-- conditional other way of v-bind-->   
    <input v-model="message" :class="{'error' : message.length > 22}"/>

    <br>
    <!-- conditional other way of v-bind using computed property -->   
    <input v-model="message" :style="errorStyle"/>

    <div>{{message.length}}</div>
  </q-page>
</template>

<script>
export default {
  data(){
    return{
      message: "I Love Vue.js so hard",
      keyup: "Keyup Event",
      mouseEnter: "Mouse Enter Event",
      vshow: "V-Show Directive",
      vif: "V-If Directive",
      velse: "V-Else Directive",
      counter: 0
   }
  },
  computed: {
     messageUppercasecomputed(){
      console.log('messageUppercase was fired')
      return this.message.toUpperCase()
    },

    messageUppercasecomputedappend(){
      console.log('messageUppercase was fired')
      return this.message.toUpperCase() + this.counter
    },
    errorStyle(){
      if(this.message.length > 22){
        // return 'color: red; background: pink;' simple form 
        return{
          'color' : 'red',
          'background' : 'pink'
        }
      }
    }
  },
  methods: {
    clearMessage(){
      this.message = ''
    },
    handleKeyup(e){
      console.log(e)
      if(e.keyCode == 27){
        this.clearMessage()
      }
      else if(e.keyCode == 13){
        this.alertMessage()
      }
    },
    alertMessage(){
      alert(this.message)
    },
    messageUppercase(){
      console.log('messageUppercase was fired')
      return this.message.toUpperCase()
    }
  },
  //filters used by formating dates
  filters: {
    messageLowercase(value){
      return value.toLowerCase()
    }
  },
  directives: {
    autofocus: {
      inserted(el) {
        el.focus()
      }
    }
  }
};
</script>

<style>
  .border-grey{
    border: 1px solid grey;
  }

  .error{
    color:red;
    background: pink;
  }
</style>
