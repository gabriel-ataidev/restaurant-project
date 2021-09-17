<template>
  <div class="item--quantity">
    <button
      class="buttons"
      @click="onDecreaseButtonClick"
      :disabled="item.quantity == 0"
    >
      -
    </button>
    <span class="number">{{ item.quantity }}</span>
    <button class="buttons" @click="onincreaseButtonClick()">+</button>
    <Modal :show="showModal">
      <div class="modal--content">
        <h2>Deseja remover este item do carrinho?</h2>
        <div class="buttons">
          <button class="secondary-button" @click="onRemoveButtonClick">
            Sim, remover.
          </button>
          <button class="primary-button" @click="onCancelButtonClick">
            Voltar ao carrinho.
          </button>
        </div>
      </div>
    </Modal>
  </div>
</template>

<script>
import { mapActions } from "vuex";
import Modal from "./Modal.vue";

export default {
  components: {
    Modal,
  },
  props: {
    item: {},
    useStore: {
      type: Boolean,
      default: true,
    },
  },
  data() {
    return {
      showModal: false,
    };
  },
  methods: {
    ...mapActions(["increaseQuantity", "decreaseQuantity"]),
    onDecreaseButtonClick() {
      if (this.useStore) {
        this.decreaseQuantity(this.item.id);
        if (!this.item.quantity) this.showModal = true;
        return;
      }
      --this.item.quantity;
    },
    onincreaseButtonClick() {
      if (this.useStore) {
        this.increaseQuantity(this.item.id);
        return;
      }
      ++this.item.quantity;
    },
    onCancelButtonClick() {
      this.increaseQuantity(this.item.id);
      this.showModal = false;
    },
    onRemoveButtonClick() {
      this.showModal = false;
      this.$nextTick(() => {
        this.$store.dispatch("removeFromCart", this.item.id);
      });
    },
  },
};
</script>

<style scoped lang="less">
.item--quantity {
  display: flex;
  align-items: center;
  padding-right: 20px;
  .number {
    color: @yellow;
    padding: 10px;
    text-align: center;
  }
  .buttons {
    cursor: pointer;
    font-size: 20px;
    padding: 0;
    background: none;
    border: 0;
    outline: none;
    :focus {
      outline: 0;
    }
  }
  .modal--content {
    text-align: center;
    .buttons {
      text-align: center;
      button {
        cursor: pointer;
      }
      button + button {
        margin-left: 30px;
      }
    }
  }
}
</style>
