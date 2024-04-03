<script> 
export default {
      // truyền data từ component cha xuống component con
      props: {
            modelValue: {type: String, default: ""},
      },
      
      // emits: cách để component phát hiện ra event và thông báo
      // cho component cha. 
      emits: ["submit", "update: modelValue"],
      // các method trong component 
      methods: {
            updateModelValue(e){
                  this.$emit("update:modelValue", e.target.value);
            },

            submit(){
                  this.$emit("submit");
            },
      },
};

</script>

<template>
<div class="input-group">
      <input type="text"
            class="form-control"
            placeholder="Nhập thông tin cần tìm"
            :value="modelValue"
            @input="updateModelValue"
            @keyup.enter="submit">

      <div class="input-group-append">
      <button class="btn btn-ouline-secondary"
            type="button"
            @click="submit">
            <i class="fas fa-search"></i>Tìm kiếm
      </button>
</div>
</div>

</template>