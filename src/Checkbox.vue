<template>
    <label >
        <!-- <input type="checkbox" @change="onChange"> -->
         <input type="checkbox" v-model="model">
        {{ label }}
    </label>
</template>
<script setup>
defineProps({
    label: String
});
const model = defineModel()
const emits = defineEmits(['check','uncheck']);
const onChange = (event) => {
    if(event.currentTarget.checked){
        emits('check');
    }else{
        emits('uncheck');
    }
}
</script>