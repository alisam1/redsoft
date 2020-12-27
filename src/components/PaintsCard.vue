<template lang="pug">
  .card
    img(:src="item.imgSrc" alt="logo")
    h3.card__name {{item.title}}
    .card__block
      .card__price
        p.card__old-price {{item.oldPrice}}
        p.card__new-price {{item.newPrice}}
      button.card__button(@click="buttonClick(item)" :class="{'card__button-basket': item.basket}") {{item.button}}
      p.card__sale-description(:class="{'card__sale': item.sale}") {{item.saleDescription}}
</template>

<script>

import axios from 'axios'
import VueAxios from 'vue-axios'

export default {
  name: "PaintsCard",
  props:['item'],
  data () {},
  methods: {
      async buttonClick(item) {
        this.$emit('update-cart', item)
        const promise = axios.get('https://jsonplaceholder.typicode.com/posts/1')
          .then(response => (this.info = response.data))
          item.button = 'Loading...'
        await promise
            item.button = 'В корзине'
            item.basket = true
    }
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
        .paints__card-price{
          display: none;
        }
        button{
          display: none;
        }

      }
      &__name{
        margin: 0;
        padding: 0;
        padding-left: 24px;
        padding-right: 24px;
        padding-top: 20px;
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
        width: 118px;
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


</style>