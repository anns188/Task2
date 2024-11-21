<template>
<header>
    <div class="logo">
        <div class="icon">
            <span>H</span>
        </div>
        <div class="text">Search <br>
        Hacker news</div>
    </div>
    <div class="search">
         <img :src="icons('search')"  alt="">
         
    </div>
   
    <input type="text" v-model="query" @input="searchresults" class="input" placeholder="Search stories by title,url or author">
    <span class="logoright">by <img class="pic" src="/algolia.png" alt=""></span>
</header>

<div v-if="results.length" class="results">
<ul>
    <li v-for="result in results.slice(0,3)" :key="result.id">
        <a :href="result.url">{{ result.title  }}</a>
        <p class="author">by {{ result.author }}</p>

    </li>
</ul>
</div>

</template>

<style scoped>
.logo{
    display: flex;
    align-items: center;
    top: 0;
    margin-right: 25px;
    
}
.search{
    display: flex;
    margin-left: 15px;
}
header{
    display: flex;
    align-items: center;
    justify-content:space-between;
    position: fixed; 
    width: 100%;
    top: 10px;
    left: 20px;
    right: 20px;
    height: 120px;
    /* border-bottom: 5px solid gray; */
   
}
.results{
    border: 2px solid black;
    margin-top:80px;
    border-radius: 10px;
    z-index: 1;
    background-color: rgb(230, 215, 187);
    height: 300px;
    width: auto;
}
.results ul{
    list-style: none;
}
.results li{
    margin-bottom: 5px;
}

.icon{
    display: flex;
    align-items: center;
    justify-content: center;
    width: 89px;
    height: 89px;
    border: 2px solid orange;
    background-color: orangered;
    margin-right: 10px;
    border-radius: 12px;
    
}
.icon span{
    color: antiquewhite;
    font-size: 45px;
    justify-content: center;
    font-weight:bolder;
    border: 6px solid rgb(241, 241, 241);
    padding-left: 10px;
    padding-right: 10px;
    margin-top: 8px;
    margin-bottom: 12px;
    border-radius: 15px;
}
.pic{
    height: 70px;
    width: 290px;
    margin-right: 20px;
    

}
.text{
    font-size: 30px;
    font-weight: bold;
    color: gray;
}
.input{
    flex: 1;
    outline: none;
    font-size: 22px;
    font-weight: bold;
    color: black;
    padding-left: 50px;
    width: 1000px;
    height: 60px;
    border-radius: 18px;
}
.logoright{
    display: flex;
    margin-left: 15px;
    font-size: 20px;
    color: gray;
}
</style>

<script>
import axios from 'axios';
export default{
    data(){
        return{
            query:"",
            results:[],
        };
    },
   
    methods:{
        async searchresults(){
            if(this.query.trim() !== ""){
                try{
                    const response=await axios.get(
                        `https://hn.algolia.com/api/v1/search?query=${this.query}`
                    );
                    this.results=response.data.hits;
                } catch(error){
                    console.log("error",error);
                }
            }
            else{
                this.results=[];
            }
        },
        icons(section){
            const icon={
                search:'/search-svgrepo-com.svg',
            }
        return icon[section];
        },
    },
}
</script>