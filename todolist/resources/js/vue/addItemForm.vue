<template>
    <div class="addItem">
        <input type="text" @keyup.enter="addItem()" v-model="item.name" />
        <font-awesome-icon 
            icon="plus-square"
            @click="addItem()"
            :class="[ item.name ? 'active' : 'inactive', 'plus' ]" 
        />
    </div>
</template>

<script>
import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'
Vue.use(VueAxios, axios)
export default {
    data: function () {
        return {
            item: {
                name: ""
            }
        }
    },
    methods: {
        addItem() {
            if ( this.item.name == '') {
                return;
            }

            axios.post('item/store', {
                item: this.item
            }) 
            .then( response => {
                if ( response.status == 201 ) {
                    this.item.name = "";
                    this.$emit('reloadlist');
                }
            })
            .catch( error => {
                console.log( error );
            })
        }
    }
}
</script>

<style scoped>
    .addItem {
        display: flex;
        justify-content: center;
        align-items: center;
    }
    input {
        backdrop-filter: #f7f7f7;
        border: 0px;
        outline: none;
        padding: 5px;
        margin-right: 10px;
        width: 100%;
    }
    .plus {
        font-size: 20px;
    }
    .active {
        color: #00CE25;
    }
    .inactive {
        color: #999999;
    }
</style>