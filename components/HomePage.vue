<template>
    <HeaderPage />
<h1>Hello {{name}}, Welcome On Home Page</h1>  
<table border="1px">
    <tr>
        <td>Id</td>
        <td>Name</td>
        <td>Address</td>
        <td>Contact</td>
        <td>Update</td>
        <td>Delete</td>
    </tr>
    <tr v-for="item in restaurants" :key="item.id">
        <td>{{item.id}}</td>
        <td>{{item.name}}</td>
        <td>{{item.address}}</td>
        <td>{{item.contact}}</td>
        <td><router-link :to="'/update/'+item.id">Update</router-link></td>
        <td><button v-on:click="deleteRestaurant(item.id)">Delete</button></td>
    </tr>
</table>
</template>
<script>
import axios from 'axios';
import HeaderPage from './HeaderPage.vue';
export default{
    name:'HomePage',
    data(){
        return {
            name:'',
            restaurants:[],
        }
    },
    components:{
        HeaderPage
    },
    methods:{
        async deleteRestaurant(id)
        {
        let result =await axios.delete("http://localhost:3000/restaurants/"+id);  
        if(result.status==200)
        {
        this.loadData()
        }
        },
        async loadData()
        {
        let user=localStorage.getItem('user-info');
        this.name=JSON.parse(user).name
        if(!user)
        {
        this.$router.push({name:'SignUp'})
        }
        let result =await axios.get("http://localhost:3000/restaurants");
        this.restaurants=result.data
        }

    },
    mounted()
    {
    this.loadData()    
    }
};
</script>
 
<style>
td{
    width: 160px;
    height: 40px;
}
</style>