<template>
<button type="submit"> Submit</button>
</template>

<script>


export default {
name: 'CustomButton',
}
</script>

<style lang="scss" scoped>
button{
  background-color: rgba(5, 128, 130);
  border: none;
  padding:10px;
  color: white;
  border-radius:6px;
}
button:disabled{
  background-color: rgba(5, 128, 130, 0.20);
  border: none;
  padding:10px;
  color: white;
  border-radius:6px;
}
</style>