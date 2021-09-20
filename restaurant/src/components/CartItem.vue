<template>
  <div class="item">
    <Quantity :item="item" class="item--quantity" />
    <div class="item--img-container">
      <img class="item--img" :src="imagePath" />
    </div>
    <div class="content">
      <h3 class="item--name">{{ item.name }}</h3>
      <a class="item--observation" @click="onShowObservationModal"
        >adicionar observação</a
      >
      <p class="item--observation-text">{{ item.observations }}</p>
    </div>
    <p class="item--price">{{ item.price | currency }}</p>
    <Modal
      :show="showObservationModal"
      @on-modal-close="onCloseObservationModal"
    >
      <div class="modal-content">
        <h1>Adicionar observaçao</h1>
        <textarea rows="7" v-model="item.observations"></textarea>
        <div class="buttons">
          <button class="secondary-button" @click="onCloseObservationModal">
            Cancelar.
          </button>
          <button class="primary-button" @click="saveObservation">
            Salvar.
          </button>
        </div>
      </div>
    </Modal>
  </div>
</template>

<script>
import { mapActions } from "vuex";
import Quantity from "./Quantity.vue";
import Modal from "./Modal.vue";

export default {
  name: "CartItem",
  components: {
    Quantity,
    Modal,
  },
  data() {
    return {
      showObservationModal: false,
    };
  },
  props: {
    item: {},
  },
  filters: {
    currency(value) {
      return `R$${value.toLocaleString("pt-br", {
        minimumFractionDigits: 2,
      })}`;
    },
  },
  computed: {
    imagePath() {
      return require(`../assets/images/${this.item.id}.png`);
    },
  },
  methods: {
    ...mapActions(["increaseQuantity", "decreaseQuantity"]),
    onShowObservationModal() {
      this.showObservationModal = true;
    },
    onCloseObservationModal() {
      this.showObservationModal = false;
    },
    saveObservation() {
      this.$store.dispatch('addObservation', this.item);
      this.showObservationModal = false;
    },
  },
  onShowObservationModal() {
    this.ShowObservationModal = true;
  },
};
</script>

<style lang="less" scoped>
.item {
  display: flex;
  margin: 15px 0;
  &--quantity {
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
  }
  &--img-container {
    background: purple;
    border-radius: 10px;
    background: @light-yellow;
    height: fit-content;
    padding: 4px;
    margin: 0;
    display: flex;
    align-items: center;
    img {
      width: 65px;
      height: 50px;
      margin: auto;
    }
  }
  .content {
    flex-grow: 1;
    padding: 0 10px;
  }
  &--name {
    margin: 0;
    font-size: 18px;
    font-weight: 600;
  }
  &--observation {
    font-weight: 500;
    font-size: 12px;
    color: @dark-grey;
    cursor: pointer;
  }
  &--observation-text {
    font-weight: 500;
    font-size: 12px;
    color: @dark-grey;
  }
  &--price {
    color: @yellow;
    font-weight: 600;
    line-height: 20px;
    font-size: 18px;
  }
  & + & {
    border-top: 1px solid @light-grey;
    padding-top: 15px;
  }
  .modal-content{
    text-align: center;
    textarea{
      width: 100%;
      margin-bottom: 20px;
      border-radius: 10px;
    }
    button + button {
      margin-left: 25px;
    }
  }

  @media @tablets {
    flex-wrap: wrap;
    &--img-container {
      order: 1;
    }
    .content {
      order: 2;
    }
    &--quantity {
      order: 3;
      padding-left: 15px;
      padding-right: 100px;
      margin-right: auto;
      justify-content: center;
    }
    &--price {
      order: 4;
      padding-left: 25px;
    }
    & + & {
      padding-top: 30px;
    }
    .modal-content{
      h1{
        font-size: 20px;
      }
    }
  }
}
</style>
