<template>
  <div class="adjust-content">
    <div class="header">
  <HeaderComponent></HeaderComponent>
</div>
  
    <nav class="sbar">
      <ul class="list">
        <li v-for="item in items"
        :key="item.section"
        @click="currentSection= item.section"
        :class="{active:currentSection === item.section}"
        >
        <span class="icn">
         <img :src="Icons(item.section)" alt="">
        </span>
        {{item.name }}</li>
      </ul>
    </nav>
    <div class="main">
      <HotComponent v-if="currentSection==='hot'" class="filter"></HotComponent>
       <NewsComponents class="news"></NewsComponents>
    </div>
    
   
  

  </div>


</template>

<style>
@media screen {
  *{
    /* margin:0;
    padding: 0; */
    box-sizing: border-box;
  }
  #app {
        display: grid
;
        grid-template-columns: 1fr 1fr;
        padding: 0;
        margin: 0;}
        
  .adjust-content{
    display: grid;
    width: 100%;
    grid-template-columns: 250px 1fr;
    grid-template-rows: 75px 1fr;
    grid-template-areas: "header header"
    "sidebar main";
    height: 100vh;
    position: relative;
    box-sizing: border-box;
  }
  
.sbar{
  top:50px;
grid-area: sidebar;
/* top: 49px; */
position: relative;
 width: 250px;
 border-top: 1px solid gray;
 background-color: rgb(216, 210, 210);
height: calc(100vh - 75px);
left: 0;
padding-top: 25px;
overflow-y: auto;
  bottom: 0;
  z-index: 6;
box-sizing: border-box;
}

.list{
 
  list-style: none;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
}
.main{
  
  /* margin-top: 55px; */
  grid-area: main;
  /* padding: 12px; */
  flex-grow: 1;
  gap: 0;
  width: 1300px;
  overflow-y: auto;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  overflow-y: auto;
  bottom: auto;
  justify-content: flex-start;
}
.filter{

  grid-area: filter;
  border-top: 1px solid grey;
  border-bottom: 1px solid gray;
  background-color: rgb(247, 241, 241);
  flex-grow: 1;
margin-top: 50px;
}
.hot{
  grid-area: hot;
}  
.news{
  
  padding: 10px 20px;
  flex: 1;
}
ul{
  list-style: none;
  margin: 0;
  padding: 0;

}
li{
  display: flex;
  align-items: center;
  cursor: pointer;
  width: 100%;
  font-size: medium;
  padding: 15px;
  color: rgb(0, 0, 0);
}
li.active,li:hover{
  background-color: rgb(94, 90, 90);
}
.icn{
  margin-right: 15px;
}
.header{
  grid-area: header;
  height: 75px;
  padding: 15px;
  position: fixed;
top: 0;
left: 0;
right: 0;
z-index: 10;
}
img{
  
  width: 25px;
  height: 25px;
}

}


</style>

<script>
import axios, { all } from 'axios';
import HeaderComponent from './components/HeaderComponent.vue';
import HotComponent from './components/HotComponent.vue';
import NewsComponents from './components/NewsComponents.vue';
export default {
  name:'Main',
  components:{
    HeaderComponent,HotComponent,NewsComponents
  },
  data(){
    return{
      currentSection:"hot",
      items:[
        {name:"All",section:"all"},
        {name:"Hot",section:"hot"},
        {name:"Show HN",section:"show hn"},
        {name:"Ask HN",section:"ask hn"},
        {name:"Polls",section:"polls"},
        {name:"Jobs",section:"jobs"},
        {name:"Shipow",section:"shipow"},
        {name:"Starred",section:"starred"},
      ],
    };
  },
  computed:{
    currentItem(){
      return this.items.find(item=>item.section === this.currentSection)||{};
    },
  },
  methods:{
    Icons(section){
      const icon={
           all:'/note-svgrepo-com.svg',
      hot:'/fire-svgrepo-com.svg',
      'show hn':'/megaphone-svgrepo-com.svg',
      'ask hn':'/bubble-svgrepo-com.svg',
      polls:'/light-bulb-svgrepo-com.svg',
      jobs:'/dollar-banknote-svgrepo-com.svg',
      shipow:'/person-male-svgrepo-com.svg',
      starred:'/star-svgrepo-com.svg',
      }
      console.log(icon[section]);
    return icon[section];
    },

  }
};
</script>