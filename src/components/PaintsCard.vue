<template lang="pug">
  .card
    img(:src="item.imgSrc" alt="logo")
    h3.card__name {{item.title}}
    .card__block
      .card__price
        p.card__old-price {{item.oldPrice}}
        p.card__new-price {{item.newPrice}}
      button.card__button(@click="buttonClick(item)" :class="{'card__button-basket': item.basket, 'card__button-loading': item.loading}") {{item.button}}
      p(:class="{'card__sale-description': item.sale, 'card__none-description': !item.sale}") {{item.saleDescription}}
</template>

<script>

import axios from 'axios'
import VueAxios from 'vue-axios'

export default {
  name: "PaintsCard",
  props:['item'],
  data () {
    return {}
  },
  methods: {
      async buttonClick(item) {
        this.$emit('update-cart', item)
        localStorage.basket = this.basket
        const promise = axios.get('https://jsonplaceholder.typicode.com/posts/1')
          .then(response => (this.info = response.data))
              item.loading = true
          await promise
              item.button = 'В корзине'
              item.basket = true,
              item.loading = false
    },
  },
}
</script>

<style lang="scss">

@import url('https://fonts.googleapis.com/css2?family=Merriweather:wght@400;700&display=swap');

.card{
    width: 280px;
    border: 1px solid #E1E1E1;
    padding-bottom: 24px;
      &__sale{
        background: #FFFFFF;
        opacity: 0.5;
        &-description{
          display: block;
        }
        .paints__card-price{
          display: none;
        }
        button{
          display: none;
        }

      }
      &__none-description{
        display: none;
      }
      &__name{
        margin: 0;
        padding: 0;
        padding-left: 24px;
        padding-right: 24px;
        padding-top: 17px;
        padding-bottom: 22px;
        box-sizing: border-box;
        font-style: normal;
        font-weight: normal;
        font-size: 18px;
        line-height: 150%;
        color: #343030;
      }
      &__block{
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        padding-left: 24px;
        padding-right: 24px;
      }
      &__old-price{
        margin: 0;
        padding: 0;
        font-style: normal;
        font-weight: 300;
        font-size: 14px;
        line-height: 150%;
        text-decoration-line: line-through;
        color: #A0A0A0;
      }
      &__new-price{
        margin: 0;
        padding: 0;
        font-style: normal;
        font-weight: bold;
        font-size: 16px;
        line-height: 150%;
        color: #343030;
      }
      &__button{
        width: 114px;
        height: 48px;
        font-family: 'Merriweather', serif;
        font-style: normal;
        font-weight: bold;
        font-size: 14px;
        line-height: 150%;
        color: #F4F6F9;
        background: #382E2B;
        border: none;
        cursor: pointer;
        margin-left: 20px;
        &-loading{
          position: relative;
          &::after{
            content:"";
            position: absolute;
            border: 2px solid #f3f3f3;
            border-radius: 50%;
            border-top: 2px solid #000;
            width: 20px;
            height: 20px;
            -webkit-animation: spin 2s linear infinite; /* Safari */
            animation: spin 2s linear infinite;
            left: 47px;
          }
        }
        &-basket{
          background: #5B3A32;
          position: relative;
          padding-left: 25px;
          &::before{
            content: "";
            position: absolute;
            width: 14px;
            height: 14px;
            background-image: url("../assets/basket_icon.svg");
            left: 10px;
            top: 17px;
          }
        }
        &:hover{
          background: #776763;
          cursor: pointer;
        }
      }
  }

  /* Safari */
  @-webkit-keyframes spin {
    0% { -webkit-transform: rotate(0deg); }
    100% { -webkit-transform: rotate(360deg); }
  }

  @keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
  }


</style>