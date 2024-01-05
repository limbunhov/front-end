<template>
    <div class="board_admin">
        <!-- <div class="profile_admin">
            <div class="pro_img">
                <i class="fa-solid fa-user"></i>
            </div>
            <div class="name">
                <a href="#">Admin</a>
            </div>
        </div> -->
        <div class="item_admin">
            <div class="add">
                <span @click="toglecreate"><i class="fa-solid fa-square-plus"></i></span>
                <h5>Add item</h5>
                <postproduct v-if="openproduct" :togleclose="toglecreate"/>
            </div>
            <div class="edit">
                <span @click="togleUpdate"><i class="fa-solid fa-pen-to-square"></i></span>
                <h5>Edit item</h5>
                <Updateproduct v-if="openUpdate" :togleclose="togleUpdate"/>
            </div>
            <div class="delete">
                <span @click="togleDelete"><i class="fa-solid fa-trash-can"></i></span>
                <h5>delete</h5>
                <deleteproduct  v-if="openDelete" :togleclose="togleDelete"/>
            </div>   
        </div>
        <div class="seeallproduct">
            <Seeallproduct/>
        </div>
    </div>
</template>
<script>
import postproduct from './crudpage/postproduct.vue';
import Updateproduct from './crudpage/Updateproduct.vue';
import deleteproduct from './crudpage/deleteproduct.vue';
import seeallproduct from './crudpage/seeallproduct.vue';
import Seeallproduct from './crudpage/seeallproduct.vue';
export default{
    components:{
    postproduct,
    Updateproduct,
    deleteproduct,
    seeallproduct,
    Seeallproduct
},
    data (){
        return {
            openproduct:false,
            openUpdate:false,
            openDelete:false,
        }
    },
    methods:{
        toglecreate(){
            this.openproduct =!this.openproduct;
        },
        togleUpdate(){
            this.openUpdate =!this.openUpdate
        },
        togleDelete(){
            this.openDelete =!this.openDelete
        }
    }
}
</script>