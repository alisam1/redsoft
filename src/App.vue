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
            .paints__card(v-for="(i, index) in paints" :key="index" :class="{'paints__card-sale': i.sale}")
              img(:src="i.imgSrc" alt="logo")
              h3.paints__card-name {{i.title}}
              .paints__card-block
                .paints__card-price
                  p.paints__card-old-price {{i.oldPrice}}
                  p.paints__card-new-price {{i.newPrice}}
                button.paints__card-button(@click="buttonClick" v-if="i.button") {{button}}
                p.paints__card-sale-description(v-if="i.sale") {{i.saleDescription}}

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
import axios from 'axios'
import VueAxios from 'vue-axios'

export default {
  name: 'app',
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
        button: true,
        inStock: true,
        sale: false
      },
      {
        imgSrc: '/src/assets/paint_2.png',
        title: '«Тайная вечеря» Леонардо да Винчи',
        oldPrice: '',
        newPrice: '3 000 000 $',
        button: true,
        inStock: true,
        sale: false
      },
      {
        imgSrc: '/src/assets/paint_3.png',
        title: '«Сотворение Адама» Микеланджело',
        oldPrice: '6 000 000 $',
        newPrice: '5 000 000',
        button: true,
        inStock: true,
        sale: false
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
    ],
    info: null,
    button: 'Купить',
    sale: false
    }
  },
  methods: {
    async buttonClick() {
      const promise = axios.get('https://jsonplaceholder.typicode.com/posts/1')
        .then(response => (this.info = response.data))

        this.button = 'Loading...'

      await promise

        this.button = 'В корзине'
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
  &__card{
    width: 280px;
    border: 1px solid #E1E1E1;
    padding-bottom: 24px;
      &-sale{
        background: #FFFFFF;
        opacity: 0.5;
        .paints__card-price{
          display: none;
        }
        button{
          display: none;
        }

      }
      &-name{
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
      &-block{
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        padding-left: 24px;
        padding-right: 24px;
      }
      &-old-price{
        margin: 0;
        padding: 0;
        font-style: normal;
        font-weight: 300;
        font-size: 14px;
        line-height: 150%;
        text-decoration-line: line-through;
        color: #A0A0A0;
      }
      &-new-price{
        margin: 0;
        padding: 0;
        font-style: normal;
        font-weight: bold;
        font-size: 16px;
        line-height: 150%;
        color: #343030;
      }
      &-button{
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
        &:hover{
          background: #776763;
          cursor: pointer;
        }
      }
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
