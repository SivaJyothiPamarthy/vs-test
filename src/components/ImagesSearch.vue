<template>
  <div class="input-container">
    <input type="text" placeholder="Search" 
    :value="modelValue" 
    @input="$emit('update:modelValue', $event.target.value)"/>
  </div>
</template>

<script>
  export default {
    props: ['modelValue']
  };
</script>


<style scoped>
.input-container {
	border-radius: 5px;
	background: #677482;
	padding: 10px;
  width: 500px;
  margin: 20px 2px 20px 2px;
}

.input-container input {
	border: none;
	background: transparent;
	padding: 6px;
	font-size: 18px;
  width: 475px;
  color: #fff;
}

::placeholder { 
  color: #a6b0ba;
  opacity: 1; 
}

</style>