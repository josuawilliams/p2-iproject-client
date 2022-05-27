<script>
import { mapActions, mapWritableState } from 'pinia';
import { RouterLink } from 'vue-router'
import { useDataNews } from '../stores/dataNews';
export default{
    data(){
        return{
            urlForDetail : ""
        }
    },
    props :['news'],
    components :{
        RouterLink
    },
    methods :{
        clickURL(params){
            this.urlForDetail = params
            this.dataURL = this.urlForDetail
            this.$router.push("/categories/detail") 
        },
        changeDate(input){
            const options = {weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
            const date = new Date(input).toLocaleDateString('id-ID', options);
            return date
        }
    },
    computed:{
        ...mapWritableState(useDataNews ,['dataURL'])
    },
}   
</script>

<template>
                <div v-for="data in news.data" id="card" class="col-md-2 mb-4 p-1 " >
                    <a @click.prevent="clickURL(data.link)" href>
                    <div  class="card h-100">
                        <img :src=data.thumbnail alt="">
                        <div  class="card-body">
                            <h2 class="card-title">{{data.title}}</h2>
                            <p>{{changeDate(data.pubDate)}}</p>
                            <h6>{{data.description}}</h6>
                        </div>
                    </div>
                    </a>
                </div>
                
</template>

<style>
#card{
    box-shadow: 5px 5px 20px black;
    border-radius: 10px;
    margin-left: 20px;
}
#card :hover{
    transform: scale(1.1);
    transition: transform .5s;
    border-radius: 10px;
}
a{
    text-decoration: none;
    color: black;
}
</style>