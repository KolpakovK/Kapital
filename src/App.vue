<template>
<!-- Навигация -->
  <div id="app">
    <Navigation/>
    <!-- Отступ -->
    <div class="space48"></div>
    <div class="container">
      <!-- Левая сторона приложения -->
      <div id="leftCol">
        <!-- Блок уведомления с градиентом -->
        <TextAlert v-bind='textAlertData'/>
        <div class="space48"></div>
        <!-- Название странцы -->
        <h2 class="text-white text-medium margin-bottom-24">{{namePage}}</h2>
        <!-- Описание страницы -->
        <p class="text-white text-light opacity7">{{descriptionPage}}</p>
        <div class="space48"></div>


        <!-- Форма -->
        <form id="calculator-form" class="field-grid">

          <!-- Категория -->
          <InputDropDown v-bind='formItems.category'/>

          <!-- Бренд -->
          <InputDropDown v-bind='formItems.brand'/>

          <!-- Модель -->
          <InputDropDown v-bind='formItems.model'/>

          <!-- Состояние -->
          <InputDropDown v-bind='formItems.state'/>

          <!-- Комлпектация -->
          <div class="input-checkbox">
            <!-- Название поля -->
            <p>Комплектация</p>
            <hr>
            <!-- Выбор чекбоксов в группе -->
            <form class="checkboxes">
              <!-- Цикл -->
              <div v-for="complect in formItems.complect" :key="complect" class="checkbox">
                <!-- Поле инпут -->
                <input type="checkbox" v-on:change="changeList('complect',complect)" v-bind:name="complect">
                <!-- Текст -->
                <label v-bind:for="complect">{{complect}}</label>
              </div>
            </form>
          </div>

          <!-- Поиск по -->
          <div class="input-checkbox">
            <!-- Название -->
            <p>Поиск по</p>
            <hr>
            <!-- Форма для инпутов -->
            <form class="checkboxes">
              <!-- Цикл -->
              <div v-for="search in formItems.search" :key="search" class="checkbox">
                <!-- Чек бокс -->
                <input type="checkbox" v-on:change="changeList('search',search)" v-bind:name="search">
                <!-- Подпись -->
                <label v-bind:for="search">{{search}}</label>
              </div>
            </form>
          </div>

        </form>
        <!-- Конец основной формы -->


        <div class="space48"></div>
        <!-- Кнопка отправки формы -->
        <!-- Кнопка находится за пределами так как в форме используется сетка и влом её настраивать)))) -->
        <a href="" id="sendForm" class="decoration-none text-medium text-white button button-blocked width-100">Рассчитать</a>
        

      </div>

      <div id="rightCol">
        <!-- Объявления -->
        <h1 class="text-white text-medium margin-bottom-24">ПРИМЕРЫ ОБЪЯВЛЕНИЙ</h1>
        <!-- условие -->
        <p v-if="!result" class="text-white text-light opacity7">Сделайте запрос и вы увидите примеры объявлений*</p>
        <div v-else id="result-container">
          <ResultCard v-for="resultItem in resultcards" :key="resultItem" v-bind="resultItem"/>

          <div class="space48"></div>
          <a href="" id="viewAllResults" class="decoration-none text-medium text-white button width-100">Смотреть всё</a>
          <div class="space96"></div>
          <h1 class="text-white text-medium margin-bottom-24">РЕЗУЛЬТАТ</h1>
          <h1 id="total">
            {{total + 'грн.'}}
          </h1>
        </div>
      </div>


    </div>
  </div>
</template>

<script>

  import axios from "axios";

  import Navigation from "@/components/Navigation.vue"
  import TextAlert from "@/components/TextAlert.vue"
  import InputDropDown from "@/components/InputDropDown.vue"
  import ResultCard from "@/components/ResultCard.vue"

  export default {
    name: 'App',
    components:{
      Navigation,
      TextAlert,
      InputDropDown,
      ResultCard,
    },
    data(){
      return{
        result:false,
        resultcards:{
          // 0:{
          //   url:"#",
          //   title:"Название",
          //   cost:"10.000"
          // },
          // 1:{
          //   url:"#",
          //   title:"Название",
          //   cost:"10.000"
          // },
          // 2:{
          //   url:"#",
          //   title:"Название",
          //   cost:"10.000"
          // },
        },
        total:"",
        textAlertData:{
          title: "ОНЛАЙН ОЦЕНКА ТЕХНИКИ",
          description: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Leo volutpat, vivamus enim nulla in magnis massa elementum. In proin turpis neque quis."
        },
        descriptionPage: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Leo volutpat, vivamus enim nulla in magnis massa elementum. In proin turpis neque quis. ",
        namePage:"Калькулятор",
        formItems: {
          category:{
            id: "Category",
            title: "Категория",
            list: []
          },
          brand: {
            id: "Brand",
            title: "Производитель",
            list: []
          },
          model: {
            id: "Model",
            title: "Модель",
            list: []
          },
          state:{
            id: "State",
            title: "Состояние",
            list: ["Плохое","Ниже среднего","Среднее","Выше среднего","Отличное"]
          },
          complect: [""],
          search: ["OLX","Besplatka","Bigl"]
        },
        finalJSON:{
          category:"",
          brand:"",
          model:"",
          state:"",
          complect:[],
          search:[]
        }
      }
    },
    methods:{

      // СМЕНА ПОЛЯ О КАТЕГОРИИ
      categoryChange:function(data){

        let JSON_CATEGORY_POST = {Category:data};
        axios.post("https://reqres.in/api/articles",JSON_CATEGORY_POST).then(response => {
          console.log(response.data);
          let FAKE_DATA ={
              id: "Brand",
              title: "Производитель",
              list: ["brand1","brand2","brand3","brand4"]
            }
          this.formItems.brand = FAKE_DATA;
        });
      },
      

      // СМЕНА ПОЛЯ О МОДЕЛИ УСТРОЙСТВА
      brandChange:function(data){

        let JSON_CATEGORY_POST = {Brand:data};
        axios.post("https://reqres.in/api/articles",JSON_CATEGORY_POST).then(response => {
          console.log(response.data);
          let FAKE_DATA = {
            model: {
              id: "Model",
              title: "Модель",
              list: ["model1","model2","model3","model4"]
            },
            complect: ["complect1","complect2","complect3","complect4"],
          }
          this.formItems.model = FAKE_DATA.model;
          this.formItems.complect = FAKE_DATA.complect;
        });
      },

      changeList:function(list,el){
        console.log(this.finalJSON[list]);
        
        if (this.finalJSON[list].includes(el)){
          this.finalJSON[list] = this.finalJSON[list].filter(function(value){
            return value != el;
          });
        }
        else{
          this.finalJSON[list].push(el);
        }

          console.log(this.finalJSON);
        }
      

    },

    // ПРИ СОЗДАНИИ СТРАНИЦЫ
    created(){
      axios.get("https://reqres.in/api/articles").then(response =>{
        console.log(response.data);
        let FAKE_DATA = {
            id: "Category",
            title: "Категория",
            list: ["test1","test2","test3","test4"]
          }
        
        this.formItems.category = FAKE_DATA;
      });
    }
  }

</script>

<style>
</style>
