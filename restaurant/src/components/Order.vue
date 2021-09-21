<template>
  <div class="order">
    <form>
      <label for=""> {{ formData.name.label }} </label>
      <input
        type="text"
        placeholder="Digite seu nome"
        v-model="formData.name.value"
        @blur="formData.name.isValid()"
        :class="{'error' : !formData.name.valid}"
      />
      <p class="error-message" v-if="!formData.name.valid">
        {{ formData.name.errorMessage }}
      </p>
    </form>
    <button class="primary-button" @click="orderItems">Concluir pedido</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      formData: {
        name: {
          value: "",
          errorMessage: "O nome é obrigatório",
          label: "Nome*",
          valid: true,
          isValid: () => {
            this.formData.name.valid = this.formData.name.value.length;
          },
        },
      },
    };
  },
  methods: {
    triggerValidations() {
      this.formData.name.isValid();
    },
    orderItems() {
      this.triggerValidations();
    },
  },
};
</script>

<style lang="less" scoped>

</style>
