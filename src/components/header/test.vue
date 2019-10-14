<template>
    <div v-if="show">{{$store.state.position.name}}</div>
</template>
<script>
export default {
    props:['show'],
    beforeUpdate(){
        console.log(this.show);
    }
}
</script>