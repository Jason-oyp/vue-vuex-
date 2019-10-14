<template>
    <div class="m-geo">
        <div class="position">
            <i class="el-icon-location" />
            {{$store.state.position.name}}
            <router-link class="changeCity" :to="{name: 'changeCity'}">切换城市</router-link>
            [
                <a href="#" v-for="(item, index) in nearCity" :key="index"> {{item.name}} </a>
            ]
        </div>
        <div class="m-user" v-if="!$store.state.userName">
            <router-link class="login" :to="{name: 'login'}">立即登录</router-link>
            <router-link class="register" :to="{name: 'register'}">注册</router-link>
        </div>
        <test :show="$store.state.change"/>
    </div>
</template>

<script>
import api from '@/api/index.js'
import test from './test'
export default {
    data() {
        return {
            nearCity: [],
        }
    },
    // computed:{
    //     change(){
    //         return this.$store.state.change;
    //     }
    // },
    watch: {
        "$store.state.position": function () {
              this.nearCity = this.$store.state.position.nearCity;
        }
    },
    mounted() {
        api.getCurPosition().then((res) => {
            this.$store.dispatch('setPosition', res.data.data);
            this.nearCity = res.data.data.nearCity;

        });
    },
    components:{
        test
    }
}
</script>


