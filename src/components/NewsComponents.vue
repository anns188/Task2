<template>
    <div class="news">
        <div class="list">
            <ListItem v-for="item in items" :key="item.id" :item="item"></ListItem>
        </div>
    </div>
</template>

<style>
.news{
    padding: 10px;
    margin: 0;
    width: 100%;
    background-color:rgb(245, 242, 237) ;
    gap: 0;
}

.list{
    display: flex;
    gap: 0;
    flex-direction: column;
}
</style>

<script>
import axios from 'axios';
import ListItem from'./ListItemComponent.vue';

export default{
    name:'NewsComponents',
    components:{ListItem},
    data(){
        return{
            items:[],
        };
    },
    async created() {
        try{
            const storiestop=await axios.get('https://hacker-news.firebaseio.com/v0/topstories.json?print=pretty') ;
            console.log('Top Stories:', storiestop.data);
            const storiesid=storiestop.data.slice(0,3);
        const stories=await Promise.all(storiesid.map(async(id)=>{
            const url=`https://hacker-news.firebaseio.com/v0/item/${id}.json?print=pretty`;
            const response=await axios.get(url);
            return response.data;
       }));
       this.items=stories.filter((story)=>story && story.id && story.url && story.title);
        console.log(this.items);   
    } catch(error){
            console.log("Error",error);
        }
    }
};



</script>