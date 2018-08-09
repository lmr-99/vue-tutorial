<template>
    <div class="container">
        <form @submit.prevent="addSkill">
            <input type="text" placeholder="Enter a skill you have.." v-model="skill" v-validate="'min:5'" name="skill">
            <transition name="alert-in" enter-active-class="animated flipInX" leave-action-class="animated flipOutX">
                <p class="alert" v-if="errors.has('skill')">{{ errors.first('skill') }}</p>
            </transition>
        </form>
        <div class="holder">
            <p class="error" v-show="error">{{errorMsg}}</p>
            <ul>
                <transition-group name="list" enter-active-class="animated bounceInUp" leave-active-class="animated bounceOutDown">
                    <li v-for="(data, index) in skills" :key="index">{{data.skill}}
                        <i class="fa fa-minus-circle" v-on:click="remove(index)"></i>
                    </li>
                </transition-group>
            </ul>
            <p>These are the skills you possess</p>
        </div>
    </div>
    <!--<div class="skills">-->
    <!--<div class="holder">-->
    <!--<ul>-->
    <!--<li v-for="(data, index) in skills" :key="index">{{index}}. {{data.skill}}</li>-->
    <!--</ul>-->
    <!--<div v-bind:class="alertObject"></div>-->
    <!--<p v-if="skills.length > 5">You have more than 5 skills</p>-->
    <!--<p v-else>You have less than or equal to 5 skills</p>-->
    <!--</div>-->
    <!--<h1 v-once>{{name}}</h1>-->
    <!--<div v-bind:style="object2"></div>-->
    <!--{{ btnState ? 'The button is disabled' : 'The button is active'}}-->
    <!--<button v-on:click="changeName" v-bind:disabled="btnState">Change Name</button>-->
    <!--</div>-->
</template>

<script>
    export default {
        name: 'Skills',
        data() {
            return {
                error: false,
                errorMsg: '',
                skill: '',
                name: 'Coursetro',
                btnState: true,
                skills: [
                    {"skill": "Vue.js"},
                    {"skill": "Frontend Developer"}
                ],
                object2: {
                    "background-color": 'lightpink',
                    width: '100%',
                    height: '10px'
                },
                alertObject: {
                    alert: false,
                    another_class: true
                },
                alertObject2: {
                    bgColor: 'yellow',
                    bgWidth: '100%',
                    bgHeight: '30px'
                }
            }
        },
        methods: {
            addSkill() {
                this.$validator.validateAll().then((result) => {
                    if (result) {
                        this.skills.push({skill: this.skill})
                        this.skill = ''
                        this.error = false
                        this.errorMsg = ''
                    } else {
                        this.error = true
                        this.errorMsg = 'Invalid Input!'
                    }
                })
            },
            remove(id) {
                this.skills.splice(id, 1);
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    @import "https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css";
    @import "https://cdn.jsdelivr.net/npm/animate.css@3.5.1";
    /*.alert-in-enter-active {
        animation: bounce-in .5s;
    }
    .alert-in-leave-active {
        animation: bounce-in .5s reverse;
    }
    @keyframes bounce-in {
        0% {
            transform: scale(0);
        }
        50% {
            transform: scale(1.5);
        }
        100% {
            transform: scale(1);
        }
    }*/
    .holder {
        background: #fff;
    }

    ul {
        list-style-type: none;
        padding: 0;
        margin: 0;
    }

    ul li {
        padding: 20px;
        font-size: 1.3em;
        background-color: #E0EDF4;
        border-left: 5px solid #3EB3F6;
        margin-bottom: 2px;
        color: #3E5252;
    }

    p {
        text-align: center;
        padding: 30px 0;
        color: gray;
    }

    .container {
        box-shadow: 0 0 40px lightgray;
    }

    input {
        width: calc(100% - 40px);
        border: 0;
        padding: 20px;
        font-size: 1.3em;
        background-color: #323333;
        color: #687F7F
    }

    .alert {
        background: #fdf2ce;
        font-weight: bold;
        /*display: inline-block;*/
        padding: 5px;
        margin-top: 0;
        margin-bottom: 0;
    }

    .error {
        background: indianred;
        padding: 10px 0;
        height: 15px;
        font-weight: bold;
        color: #323333;
        margin-bottom: 0;
        margin-top: 0;
    }
</style>
