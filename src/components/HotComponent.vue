<template>
    <div class="filtering">
        <div class="left">
            <h1>Hot : </h1>
    
    <div>
        <div class="option">
            <label >
                in
                <select v-model="filterType" @change="update">
                    <option value="story">Stories</option>
                    <option value="comments">Comments</option>
                </select>
            </label>
            <label >by
                <select v-model="sort" @change="update">
                <option value="popularity">Popularity</option>
                <option value="date">Date</option>
                </select>
            </label>
            <label >
                for
                <select v-model="time" @change="update">
                    <option value="24h">Last 24 hours</option>
                    <option value="week">Last week</option>
                    <option value="month">Last Month</option>
                </select>
            </label>
        </div>
    </div>
        <div class="done">
            {{ result}} results ({{ response }} seconds)
        </div>
    </div>
        
       
</div>
</template>

<style>
.option label{
    margin-right: 2rem;
    padding: 10px;

}
.left{
    margin-left: 25px;
}
.filtering{
    display: flex;
    align-items: center;
    justify-content: space-between;
     padding: 0; 
     margin: 0; 
    padding: 0;
    width: 100%;
    margin: 0;
}
.left{
    display: flex;
    align-items: center;
    gap: 10px;
}
.done{
    margin:20px;
   position: relative;;
    font-size: medium;
    color: black;
    
}
</style>

<script>
export default{
    data(){
        return{
            filterType:'stories',
            sort:'popularity',
            time:'24h',
            result: 88,
            response:0.001,
        }
    },
    methods:{
        
    }
}
</script>
