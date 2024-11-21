<template>
    <div v-bind="$attrs" class="all">
        <div class="content">
            <div class="cwrap">

<div class="items" v-if="item && item.id && item.title && item.url" >
<a :href="item.url" class="title">{{ item.title }}</a>
<!-- <p v-if="item.score">points</p> -->

</div>


<div class="description" v-if="item">
<span class="score"><img :src="icons('heart')" class="heart" alt="">{{ item.score !== undefined ? item.score +' points': 'No score'}}</span>
<span class="author"><img :src="icons('profile')" class="profile" alt=""> by {{ item.by  || 'Anonymous'}}</span>
<span class="time"><img :src="icons('clock')" class="clock" alt="">{{ timeago }}</span>
<a :href="item.url">{{ getdomain(item.url) }}</a>
</div>
</div>


<div class="iconsright">
    <div class="comment"><img :src="icons('comment')"  alt=""/></div>
    <div class="shares"><img :src="icons('shares')"  alt=""/></div>
    <div class="starred"><img :src="icons('starred')"  alt=""/></div>
</div>

        </div>
  


</div>

</template>

<script>
export default{
    name:'ListItem',
    props:{
          item:{
        type: Object,
        required:true,
    }
    },
    computed:{
        timeago(){
            const hours=Math.floor((Date.now()/1000-this.item.time)/3600);
            return hours < 24 ? `${hours} hours ago`:`${Math.floor(hours/24)} days ago`;
        }
    },
    methods:{
        getdomain(url){
            try{
                return  new URL(url).hostname.replace("www.","");
            } catch{
                return "Unknown url";
            }
        },
        icons(section){
            const icon={
                comment:'/comment-svgrepo-com.svg',
                shares:'/sharing-symbol-svgrepo-com.svg',
                starred:'/star-svgrepo-com.svg',
                heart:'/heart-svgrepo-com.svg',
                profile:'/person-male-svgrepo-com.svg',
                clock:'/clock-two-svgrepo-com.svg'
            }
            return icon[section];
        },
    }
};
</script>

<style>
*{padding: 0;
margin: 0;
}
    .description{
        display: block;
        flex-direction: row;
        color: rgb(70, 66, 66);
        gap: 12px;
        align-self: center;
        margin: 0;
        font-size: 11px;
        padding-top: 10px;
    }
    .description span,.description a{
        display:inline-flexbox;
        margin-right:55px ;
        padding: 0;
        
    }

    .all{
        display: grid;
       grid-template-columns: 1fr 200px;
       grid-template-areas: "content iconsright";
        box-shadow: 0 2px 4px rgb(45, 45, 53);
        padding: 10px;
        margin: 10px 0;
        gap: 20px;
        transition: 0.5ms ease;
        width: 100%;
        align-items: stretch;
        justify-content: flex-start;
        
    }
    .content{
        display: flex;
        flex-direction: column;
        flex: 1;
        padding: 0;
    }
    .items{
        display: flex;
        justify-content: flex-start;
        
    }
    .cwrap{
        display: flex;
        flex-direction: column;
        max-width: 100%;
        margin: 0;
        padding: 0;
        flex: 1;
    }

    .cwrap a{
        align-items: start;
    }
    .items a{
        font-size: 22px;
        text-decoration:none;
        color: black;
        font-weight: bold;
        display: block;
        margin-left: 0;
}

.score,.author,.time,.comments{
    display: inline-block;
    margin-right: 30px;
    
}
.iconsright{
    display:flex;
    flex-direction: row;
    justify-content:flex-end;
    align-items: center;
    gap:10px;
    padding-left: 20px;
    height: 100%;
    min-width: 70%;
}
.iconsright img{
    width: 25px;
    height: 25px;
}
</style>