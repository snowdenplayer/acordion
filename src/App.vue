<template>
  <div id="app">
    <h1 v-if="Object.keys(currentProduct).length">{{ `Name ${getProduct.name }
     Country ${getProduct.country } type ${getProduct.typ }` }}</h1>
    <div class="card-wrapper">
      <div class="card"
           v-for="item in products"
           :key="item.name"
           @click="showCountry(item)"
      >
        <div class="card__title">{{ item.name }}</div>
        <ul
            v-if="item.openCountry"
            class="card__list-county">
          <li
              class="card__item-country"
              v-for="country in item.countries"
              :key="country.name"
              @click="showTypes(item,country)"
          >
            {{ country.name }}
            <ul
                v-if="country.openTypes"
                class="card__list-type">
              <li
                  class="card__item-type"
                  v-for="typ in country.types.type"
                  :key="typ"
                  :data-value='`${typ}`'
                  :class="{'active': typ === currentProduct.typ}"
                  @click="setCurrentProduct(item.name,country.name,typ)"
              >
                {{ typ }}
              </li>
            </ul>
          </li>
        </ul>
      </div>

    </div>

  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return{
      currentProduct: {},
      products: [
        {
          name: 'Apple',
          openCountry: false,
          countries: [
            {
              name: 'Poland',
              openTypes: false,
              types: {
                type: [
                  'small',
                  'big',
                  'middle'
                ]
              }
            },
            {
              name: 'England',
              openTypes: false,
              types: {
                type: [
                  'red',
                  'blue',
                  'dark'
                ]
              }
            },
          ]
        },
        {
          name: 'Orange',
          openCountry: false,
          countries: [
            {
              name: 'Turkish',
              openTypes: false,
              types: {
                type: [
                  'small',
                  'big',
                  'middle'
                ]
              }
            },
            {
              name: 'England',
              openTypes: false,
              types: {
                type: [
                  'red',
                  'blue',
                  'dark'
                ]
              }
            },
          ]
        },
      ]
    }
  },
  methods:{
    showCountry(el){
      this.products.forEach(x => {
        if(x === el){
          x.openCountry = true
        }else{
          x.openCountry = false
        }
      })
    },
    showTypes(el,country){
      this.products.forEach(x => {
        if(x.name === el.name){
          console.log("Cuurent country", x , el)
          x.countries.forEach(item => {
            if(item === country){
              item.openTypes = true
            }else{
              item.openTypes = false
            }
          })
        }
      })
    },
    async setCurrentProduct(item, country, typ){
      await this.$nextTick()
      const newItem = {
        name: item,
        country,
        typ
      }
      this.currentProduct = newItem
    }
  },
  computed: {
    getProduct(){
      return this.currentProduct
    }
  }


}
</script>

<style lang="scss">
@import "../src/assets/style.css";
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.card-wrapper{
  max-width: 920px;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  margin: 0 auto;
  .active{
    background: red!important;
    font-weight: bolder;
  }
  .card{
    width: 30%;
    &__title{
      padding: 10px;
      background: gray;
      color: white;
      font-weight: bolder;
      position: relative;
      &::after{
        content: "";
        position: absolute;
        right: 10px;
        top: 50%;
        transform: translateY(-50%);
        width: 0;
        height: 0;
        border-style: solid;
        border-width: 8.7px 5px 0 5px;
        border-color: #ffffff transparent transparent transparent;
      }
    }
    &__list-county{
      list-style: none;
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    &__item-country{
      box-sizing: border-box;
      width: 100%;
      display: flex;
      justify-content: flex-start;
      flex-direction: column;
      align-items: flex-start;
      background: cadetblue;
      padding: 5px;
      color: white;
      position: relative;
      &::after{
        content: "";
        position: absolute;
        right: 10px;
        top: 12px;
        transform: translateY(-50%);
        width: 0;
        height: 0;
        border-style: solid;
        border-width: 8.7px 5px 0 5px;
        border-color: #ffffff transparent transparent transparent;
      }
    }
    &__list-type{
      list-style: none;
      display: flex;
      flex-direction: column;
      align-items: center;
      width: 100%;
    }
    &__item-type{
      box-sizing: border-box;
      width: 100%;
      display: flex;
      justify-content: flex-start;
      flex-direction: column;
      align-items: flex-start;
      background: silver;
      padding: 5px;
      color: white;
    }
  }
}
</style>
