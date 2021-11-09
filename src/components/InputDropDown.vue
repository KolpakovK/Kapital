<template>
    <div v-bind:id="id" class="input-field">
        <!-- Поле ввода -->
        <input autocomplete="off" v-bind:id="id+'Input'" v-model="valueInput" v-on:change="changeData" v-bind:name="id" v-bind:list="id+'List'" type="text" required>
        <!-- Подпись -->
        <label v-bind:for="id+'Input'">{{title}}</label>
        <!-- Стрелка -->
        <img class="list-arrow" src="@/assets/arrow-bottom.svg"/>
        <!-- Список -->
        <div v-bind:id="id +'List'" class="list">
            <span v-for="item in list" :key="item" v-on:click="listSelect">{{item}}</span>
        </div>
        <!-- <datalist v-bind:id="id + 'List'">
            <option v-for="item in list" :key="item" v-bind:value="item"/>
        </datalist>   -->
    </div>
</template>

<script>

    export default{
        name: 'InputDropDown',
        props:{
            id: String,
            title: String,
            list: Object
        },
        data(){
            return{
                valueInput:'',
                listInput:'',
            }
        },
        methods:{
            listSelect:function(event){
                this.valueInput = event.target.innerText;
                this.changeData();
            },
            changeData:function(){
                if (this.id == "Category"){
                    this.$parent.categoryChange(this.valueInput);
                    this.$parent.finalJSON.category = this.valueInput;
                }
                else if(this.id == "Brand"){
                    this.$parent.brandChange(this.valueInput);
                    this.$parent.finalJSON.brand = this.valueInput;
                }
                else if(this.id == "Model"){
                    this.$parent.brandChange(this.valueInput);
                    this.$parent.finalJSON.model = this.valueInput;
                }
                else if(this.id == "State"){
                    this.$parent.brandChange(this.valueInput);
                    this.$parent.finalJSON.state = this.valueInput;
                }

                console.log(this.$parent.finalJSON);
            }
        }
    }
</script>