<template lang="pug">
  #app
    header.header
      .container
        .header__content
          .header__menu
            ul.header__list
              li.header__item
                img(src='./assets/logo.svg' alt="logo")
              li.header__item(v-for="(i, index) in nav" :key="index")
                a(href= "{i.path}") {{ i.name }}
          .header__search
              input(
                type='search'
                name='search'
                placeholder= "Поиск по названию картины"
              )
              input(
                type='submit'
                value='Найти'
              )
    main
      section.paints
        .container
          h1.paints__title Картины эпохи Возрождения
          .paints__block
              PaintsCard(
                v-for="item in paints" 
                :item="item" 
                :key="item.id" 
                :class="{'card__sale': item.sale}" 
                @update-cart="updateCart()")

    footer.footer
      .container
        .footer__content
          .footer__menu
            ul.footer__list
              li.footer__item
                    img(src='./assets/logo_footer.svg' alt="logo")
              li.footer__item(v-for="(i, index) in nav" :key="index")
                    a(href= "{i.path}") {{ i.name }}
          .footer__contacts
            p.footer__phone
              a(href= "phone:84955555555") +7 (495) 555-55-55
            p.footer__address г. Москва, ул. Расплетина, 24
</template>

<script>

import PaintsCard from './components/paintsCard'

export default {
  name: 'app',
  components: {
    PaintsCard
  },
  data () {
    return {
      nav:[
        { name: 'Каталог', path: '/' },
        { name: 'Доставка', path: '/' },
        { name: 'Оплата', path: '/' },
        { name: 'Контакты', path: '/' },
        { name: 'О галерее', path: '/' }
      ],
      paints: [
        {
          imgSrc: '/src/assets/paint_1.png',
          title: '«Рождение Венеры» Сандро Боттичелли',
          oldPrice: '2 000 000 $',
          newPrice: '1 000 000 $',
          button: 'Купить',
          basket: false,
          inStock: true,
          sale: false
        },
        {
          imgSrc: '/src/assets/paint_2.png',
          title: '«Тайная вечеря» Леонардо да Винчи',
          oldPrice: '',
          newPrice: '3 000 000 $',
          button: 'Купить',
          basket: false,
          inStock: true,
          sale: false
        },
        {
          imgSrc: '/src/assets/paint_3.png',
          title: '«Сотворение Адама» Микеланджело',
          oldPrice: '6 000 000 $',
          newPrice: '5 000 000',
          button: 'Купить',
          basket: false,
          inStock: true,
          sale: false,
        },
        {
          imgSrc: '/src/assets/paint_4.png',
          title: '«Урок анатомии» Рембрандт',
          oldPrice: '',
          newPrice: '',
          inStock: false,
          sale: true,
          saleDescription: 'Продана на аукционе'
        }
      ]
    }
  },
  methods: {
    updateCart(item) {
        this.getStateBasket()
        console.log(123)
      },
      getStateBasket(){
        localStorage.basket = this.basket
        console.log(1234)
      }
  },
  mounted() {
    if (localStorage.basket) {
      this.basket = localStorage.basket;
      console.log(789)
    }
  },
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Merriweather:wght@400;700&display=swap');

body {
  font-family: 'Merriweather', serif;
  margin: 0;
  padding: 0;
}

.container{
  width: 1216px;
  margin: 0 auto;
}

.header{
  border-bottom: 1px solid #E1E1E1;
  padding-top: 5px;
  padding-bottom: 5px;
  &__content{
    display: flex;
    flex-direction: row;
    justify-content: space-between;
  }
  &__list{
    list-style-type: none;
    padding: 0;
    display: flex;
    flex-direction: row;
    align-items: center;
  }
  &__item{
    margin-right: 48px;
      a{
        font-style: normal;
        font-weight: normal;
        font-size: 14px;
        line-height: 150%;
        color: #343030;
        text-decoration: none;
      }
  }
  &__search{
    display: flex;
    flex-direction: row;
    align-items: center;
    input[type="search"]{
      width: 294px;
      border: 1px solid #E1E1E1;
      padding-top: 13px;
      padding-bottom: 14px;
      padding-left: 16px;
      box-sizing: border-box;
      font-family: 'Merriweather', serif;
      font-style: normal;
      font-weight: normal;
      font-size: 14px;
      line-height: 150%;
      color: #9F9F9F;
      outline: none;
      &:focus{
        border: 1px solid #B5B5B5;
        color: #343030;
      }
    }
    input[type="submit"]{
      width: 122px;
      padding-top: 13px;
      padding-bottom: 14px;
      box-sizing: border-box;
      font-family: 'Merriweather', serif;
      font-style: normal;
      font-weight: bold;
      font-size: 14px;
      line-height: 150%;
      color: #FFFFFF;
      border: none;
      background: #403432;
      border: 1px solid #403432;;
      cursor: pointer;
    }
  }
}

.card__sale{
  background: #FFFFFF;
  opacity: 0.5;
  .paints__card-price{
    display: none;
  }
  button{
    display: none;
  }
}

.paints{
  padding-top: 45px;
  padding-bottom: 320px;
  &__title{
    margin: 0;
    padding: 0;
    padding-bottom: 39px;
    font-style: normal;
    font-weight: bold;
    font-size: 24px;
    line-height: 150%;
    color: #343030;
  }
  &__block{
    display: flex;
    flex-direction: row;
    justify-content: space-between;
  }
}

.footer{
  background: #ECEAEA;
  padding-top: 24px;
  padding-bottom: 24px;
    &__content{
      display: flex;
      flex-direction: row;
      justify-content: space-between;
      align-items: center;
    }
    &__list{
      list-style-type: none;
      padding: 0;
      display: flex;
      flex-direction: row;
      align-items: center;
    }
    &__item{
      margin-right: 48px;
        a{
          font-style: normal;
          font-weight: normal;
          font-size: 14px;
          line-height: 150%;
          color: #343030;
          text-decoration: none;
        }
    }
    &__contacts{
      display: flex;
      flex-direction: row;
      align-items: center;
    }
    &__phone{
      margin: 0;
      padding: 0;
      margin-right: 51px;
      position: relative;
      a{
        font-style: normal;
        font-weight: normal;
        font-size: 14px;
        line-height: 150%;
        color: #555555;
        text-decoration: none;
      }
       &::before{
          content: "";
          position: absolute;
          width: 14px;
          height: 14px;
          background-image: url("./assets/phone_icon.svg");
          left: -20px;
          top: 5px;
        }
    }
    &__address{
        margin: 0;
        padding: 0;
        font-style: normal;
        font-weight: normal;
        font-size: 14px;
        line-height: 150%;
        color: #555555;
        position: relative;
        &::before{
          content: "";
          position: absolute;
          width: 10px;
          height: 14px;
          background-image: url("./assets/address_icon.svg");
          left: -20px;
          top: 5px;
        }
    }
}


</style>
