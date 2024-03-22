<script >
export default {
  props:{
    changeAmount: {
      type: Function,
      required: true
    },
    convert: {
      type: Function,
      required: true
    }
  },

}
</script>

<template>
  <input min="0" type="number" placeholder="Введите число" @input="changeAmount($event.target.value)">

</template>

<style scoped>
input{
  width: 500px;
  position: relative;
  top: -20px;
  border-radius: 3px;
  border: 0;
  padding: 10px 15px;
  background: #fafafa;
  color: #333;
  outline: none;
}


</style>