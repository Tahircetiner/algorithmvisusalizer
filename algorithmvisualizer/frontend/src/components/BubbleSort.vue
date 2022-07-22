<template>

  <div class="container">

    <v-btn v-on:click="bubbleSort();" elevation="5" large x-large style="margin-bottom: 20px;">Bubblesort</v-btn>
    <!--<h1>Unsorted graph</h1>-->
    <div class="container--fluid bargraph">
      <div class="bar" v-for="index in 10" ref="bar" :key="index" v-bind:style="{height:randomValue() +'px'}"></div>
    </div>
   <!--<h1>Sorted graph</h1>-->
    <!--<div class="container--fluid sortedBargraph">
    </div>-->
  </div>

</template>

<script>
export default {
  name: 'BarGraph',
  data(){
    return{
      sortedBar:[]
    }
  },
  methods:{
    bubbleSort: async function (){
      var bar = document.getElementsByClassName("bar");
      for(let i = 0; i < bar.length -1; i++){
        for(let k = 0; k < bar.length - 1; k++){
          bar.item(k).style.background = "antiquewhite";
          bar.item(k + 1).style.background = "antiquewhite";
          if(parseInt(bar.item(k).style.height) > parseInt(bar.item(k + 1).style.height)){
            bar.item(k).animate({
              transform: ["translate(124px)"],
            }, (300));
            bar.item(k + 1).animate({
              transform: ["translate(-124px)"],
            }, (300));
            await new Promise(resolve => setTimeout(resolve, 300));
            bar.item(k).style.transform = "translate(0px,0px)";
            bar.item(k + 1).style.transform = "translate(0px,0px)";
            var lastValue = bar.item(k).style.height;
            var nextValue = bar.item(k + 1).style.height;

            bar.item(k).style.height = nextValue;
            bar.item(k).textContent = parseInt(nextValue);

            bar.item(k + 1).style.height = lastValue;
            bar.item(k + 1).textContent = parseInt(lastValue);
          }
          await new Promise(resolve => setTimeout(resolve, 300));
          bar.item(k).style.background = "lightblue";
          bar.item(k + 1).style.background = "lightblue";
          await new Promise(resolve => setTimeout(resolve, 300));
        }

      }

    },
    randomValue: function (){
      return Math.floor( Math.random() * (100 -  20 + 1) + 20);
    },
    barElements: function (index){
      return parseInt(document.getElementsByClassName("bar").item(index).style.height);
    },
    selectionSort: async function (){

      var htmlbar = document.getElementsByClassName("bar");

      let indexSortedBar = 0;
      var deleteIndex = 0;
      var counter = 0;
      var currentMinimum = parseInt(htmlbar.item(counter).style.height);
      var sortedBargraph = document.getElementsByClassName("sortedBargraph").item(0);
      //var html;
      while(htmlbar.length){
        htmlbar = document.getElementsByClassName("bar");
        while(counter < htmlbar.length){
          if(currentMinimum > parseInt(htmlbar.item(counter).style.height)){
            currentMinimum = parseInt(htmlbar.item(counter).style.height);
            //html = htmlbar.item(counter);
            deleteIndex = counter;
            counter += 1;
          }
          else{
            counter += 1;
          }
        }
        this.sortedBar[indexSortedBar] = currentMinimum;
        var div = document.createElement("div");
        div.classList.add("sortedBar");
        div.textContent = currentMinimum;
        div.style.height = currentMinimum + "px";
        sortedBargraph.appendChild(div);
        indexSortedBar++;

        htmlbar.item(deleteIndex).style.background = "antiquewhite";
        await new Promise(resolve => setTimeout(resolve, 1000));

        htmlbar.item(deleteIndex).remove();
        await new Promise(resolve => setTimeout(resolve, 1000));
        counter = 0;
        deleteIndex = 0;
        if(htmlbar.length !== 0){
          currentMinimum = parseInt(htmlbar.item(counter).style.height);
        }
      }
      console.log(this.sortedBar);
    },

    sortElements: function (unsortedList, pivotElement){

    },
    quickSort: function (unsortedList){

      var pivot = this.divide(pivot, false);
      // pivot element bestimmen, sortieren,
    },

    determinePivotElement: function (value, isLeft){
      if(isLeft){
        value = value - 1;
      }else{
        value = value + 1;
      }
      return value;
    }
  },
  mounted() {
    this.$refs.bar.forEach(function (value){
      value.textContent = parseInt(value.style.height);
    })
  },
  props: {
  }
}
</script>

<style>
.bargraph{
  display: flex;
}
.bar{
  border: 1px solid black;
  background-color: lightblue;
  width: 50px;
  font-size: 20px;
  margin-right: 65px;
}
.sortedBargraph{
  display: flex;
}
.sortedBargraph .sortedBar{
  border: 1px solid black;
  background-color: lightblue;
  width: 50px;
  font-size: 20px;
  margin-right: 65px;
}
</style>
