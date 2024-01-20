<template>
    <HeaderPage />
<h1>Hello, Welcome On Add Restaurant Page</h1>    
<form class="add">
    <input type="text" placeholder="Enter Name" v-model="restaurant.name" name="name"/>
    <input type="text" placeholder="Enter Address" v-model="restaurant.address" name="address" />
    <input type="text" placeholder="Enter Contact" v-model="restaurant.contact" name="contact" />
    <button type="button" v-on:click="addRestaurant">Add New Restaurant</button>
</form>
</template>
<script>

import HeaderPage from './HeaderPage.vue';
import axios from 'axios';
export default{
    name:'AddRest',
    components:{
        HeaderPage
    },
    data()
    {
        return {
            restaurant:{
                name:'',
                address:'',
                contact:''
            }
        }
    },
    methods:{
        async addRestaurant()
        {
        const result = await axios.post("http://localhost:3000/restaurants",{
        name:this.restaurant.name,
        address:this.restaurant.address,
        contact:this.restaurant.contact,
        });
        if(result.status==201)
        {
            this.$router.push({name:'HomePage'});
        }
        }
    },
    mounted()
    {
        let user=localStorage.getItem('user-info');
        if(!user)
        {
        this.$router.push({name:'SignUp'})
        }
    }
};
</script>
