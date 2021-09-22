<template>
  <div class="order">
    <form>
      <div class="input-field">
        <label for=""> {{ formData.name.label }} </label>
        <input
          type="text"
          :placeholder="formData.name.placeholder"
          v-model="formData.name.value"
          @blur="formData.name.isValid()"
          :class="{ error: !formData.name.valid }"
        />
        <p class="error-message" v-if="!formData.name.valid">
          {{ formData.name.errorMessage }}
        </p>
      </div>
      <div class="input-field">
        <label for=""> {{ formData.cellphone.label }} </label>
        <input
          type="text"
          :placeholder="formData.cellphone.placeholder"
          v-model="formData.cellphone.value"
          @blur="formData.cellphone.isValid()"
          :class="{ error: !formData.cellphone.valid }"
        />
        <p class="error-message" v-if="!formData.cellphone.valid">
          {{ formData.cellphone.errorMessage }}
        </p>
      </div>
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
          placeholder: "Digite seu nome",
          errorMessage: "O nome é obrigatório",
          label: "Nome*",
          valid: true,
          isValid: () => {
            this.formData.name.valid = this.formData.name.value.length;
          },
        },
        cellphone: {
          value: "",
          placeholder: "Digite seu celular",
          errorMessage: "O celular é obrigatório",
          label: "Celular*",
          valid: true,
          isValid: () => {
            this.formData.cellphone.valid = (this.formData.cellphone.value.length === 9);
          },
        },
      },
    };
  },
  methods: {
    triggerValidations() {
      this.formData.name.isValid();
      this.formData.cellphone.isValid();
    },
    orderItems() {
      this.triggerValidations();
    },
  },
};
</script>

<style lang="less" scoped>
.order {
  background: #fff;
  border-radius: 10px;
  padding: 30px 50px;
  margin: 30px auto;
  form {
    display: flex;
    flex-direction: column;
    .input-field{
      display: flex;
      flex-direction: column;
      & + .input-field {
        margin-top: 20px;
      }
    }
    label {
      font-weight: 500;
      font-size: 16px;
      margin-bottom: 5px;
    }
    .error-message {
      font-size: 12px;
      color: @error-color;
    }
  }
  button{
    margin: 30px auto;
  }
}
</style>
