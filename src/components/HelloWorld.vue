<template>
  <v-container fluid>
    <v-row align="center">
        <v-col
        class="d-flex"
        cols="12"
        sm="6"
        center
      >
        <v-select
          :items="items"
          label="Select minutes"
          v-model="select"
          solo
        ></v-select>
      </v-col>
    </v-row>
    <div>
      <v-text-field
        :rules="rules"
        style="width: 50%"
        v-if="showInputBox"
        v-model="select"
      ></v-text-field>
    </div>
    <v-btn
      elevation="2"
      right
      @click="startTimer"
    >Press</v-btn>
  <div v-if="showTimer">
    <div> {{this.minutes}} : <p v-if="this.seconds < 10">0{{this.seconds}}</p>
    <p v-else>{{this.seconds}}</p></div>
  </div>
  </v-container>
</template>
<script>
export default {
  data: () => ({
    select: '',
    items: [20, 30, 40, 50, 'choose number'],
    rules: [
      value => !!value || 'Required.',
      value => (value && !(isNaN(value))) || 'Enter digit',
    ],
    seconds: 0,
    minutes: 0,
    showInput: false,
    showTimer: false
  }),
  computed:{
    showInputBox(){
      if(this.select === 'choose number'){
        // eslint-disable-next-line vue/no-side-effects-in-computed-properties
        this.showInput = true
      }
      return this.showInput
    },

  },
  methods:{
    startTimer(){
      this.showTimer = true
      this.minutes = this.select-1
      this.seconds = 59

      if(this.minute !== 0 && this.seconds > 0){
        setInterval(this.funcToTimer,1000)

      }
    },
    funcToTimer(){
      if(this.minutes > 0 && this.seconds === 0){
        this.minutes --
        this.seconds = 59
      }
     else if(this.seconds > 0) {
        this.seconds--
      }
     else {
        this.minutes = 0
        this.seconds = 0
      }
    }
  }
}
</script>
