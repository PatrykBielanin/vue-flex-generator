<template>
    <div class="container">
        <div class="header">
            <h1>Flex Generator</h1>
            <p>Built by <span style="color: #EE2737FF;"><a href="https://pbielanin.pl" target="_blank">pbielanin</a></span></p>
        </div>

        <div class="wrapper">
            <div class="flexOptions">
                <button class="btn" @click="createDiv()">Add div</button>
                <button class="btn" @click="deleteDiv()">Delete div</button>

                <div class="height">
                    <label for="height">Height of div (px)</label><br>
                    <input type="number" v-model="height"/>
                </div>

                <div class="width">
                    <label for="width">Width of div (px)</label><br>
                    <input type="number" v-model="width"/>
                </div>

                <div class="margin">
                    <label for="margin">Margin of div (px)</label><br>
                    <input type="number" v-model="margin"/>
                </div>

                <div class="flexDirection">
                    <label for="flexDirection">flex-direction</label><br>
                    <select name="flexDirection" v-model="flexDirection">
                        <option value="row">row</option>
                        <option value="column">column</option>
                        <option value="row-reverse">row-reverse</option>
                        <option value="column-reverse">column-reverse</option>
                    </select>
                </div>

                <div class="flexWrap">
                    <label for="flexWrap">flex-wrap</label><br>
                    <select name="flexWrap" v-model="flexWrap">
                        <option value="nowrap">nowrap</option>
                        <option value="wrap">wrap</option>
                        <option value="wrap-reverse">wrap-reverse</option>
                    </select>
                </div>

                <div class="flexJustifyContent">
                    <label for="flexJustifyContent">justify-content</label><br>
                    <select name="flexJustifyContent" v-model="flexJustifyContent">
                        <option value="flex-start">flex-start</option>
                        <option value="flex-end">flex-end</option>
                        <option value="center">center</option>
                        <option value="space-between">space-between</option>
                        <option value="space-around">space-around</option>
                        <option value="space-evenly">space-evenly</option>
                    </select>
                </div>

                <div class="flexAlignItems">
                    <label for="flexAlignItems">align-items</label><br>
                    <select name="flexAlignItems" v-model="flexAlignItems">
                        <option value="flex-start">flex-start</option>
                        <option value="flex-end">flex-end</option>
                        <option value="center">center</option>
                        <option value="baseline">baseline</option>
                        <option value="stretch">stretch</option>
                    </select>
                </div>

                <div class="flexAlignContent">
                    <label for="flexAlignContent">align-content</label><br>
                    <select name="flexAlignContent" v-model="flexAlignContent">
                        <option value="flex-start">flex-start</option>
                        <option value="flex-end">flex-end</option>
                        <option value="center">center</option>
                        <option value="space-between">space-between</option>
                        <option value="space-around">space-around</option>
                        <option value="stretch">stretch</option>
                    </select>
                </div>

                <button class="btn openModal" @click="toggleModal()">Generate flexbox code</button>
            </div>

            <div
                class="flexContainer"
                :style="{
                    flexDirection: flexDirection,
                    flexWrap: flexWrap,
                    justifyContent: flexJustifyContent,
                    alignItems: flexAlignItems,
                    alignContent: flexAlignContent}"
            >
                <FlexItem v-for="(flex, index) in divs"
                    :height="height"
                    :width="width"
                    :margin="margin"
                    :backgroundColor="backgroundColor"
                    :key="index"
                />
            </div>
        </div>

        <div v-if="modalStatus" class="modal">
            <button @click="toggleCloseModal()">Close modal</button>
            <section class="html">
                <pre>
                    &lt;!-- index.html -->

                    &lt;!DOCTYPE html>
                    &lt;html>
                        &lt;head>
                            &lt;title>FlexBox Template&lt;/title>
                            &lt;link rel='stylesheet' href='./style.css' type='text/css' />
                        &lt;/head>
                        &lt;body>
                            &lt;section class='flexContainer'><template v-for="i in divs">
                                    &lt;div>&lt;/div></template>
                            &lt;/section>
                        &lt;/body>
                    &lt;/html>
                </pre>
            </section>

            <section class="css">
                <pre>
                    /* style.css */

                    .flexContainer {
                        display: flex;
                        height: 80vh;
                        width: 80%;
                        background-color: #2f1d58;
                        overflow: auto;

                        flex-direction: {{flexDirection}};
                        flex-wrap: {{flexWrap}};
                        justify-content: {{flexJustifyContent}};
                        align-items: {{flexAlignItems}};
                        align-content: {{flexAlignContent}};
                    }

                    .flexContainer div {
                        width: {{width}}px;
                        height: {{height}}px;
                        margin: {{margin}}px;
                        background-color: {{backgroundColor}};
                    }
                </pre>
            </section>
        </div>
    </div>
</template>

<script>
    import FlexItem from "./FlexItem";

    export default {
        name: "Flex",
        components:{
            FlexItem
        },
        data(){
            return{
                modalStatus: false,
                height: 100,
                width: 100,
                margin: 5,
                backgroundColor: "#fdfdfded",
                flexDirection: "row",
                flexWrap: "wrap",
                flexJustifyContent: "flex-start",
                flexAlignItems: "flex-start",
                flexAlignContent: "flex-start",
                divs: [1, 1, 1]
            }
        },
        methods:{
            createDiv(){
                this.divs.push(1);
            },

            deleteDiv(){
                this.divs.splice(-1,1);
            },

            toggleModal(){
                this.modalStatus = true;
            },

            toggleCloseModal(){
                this.modalStatus = false;
            }

        }
    }
</script>

<style lang="scss" scoped>

    .header{
        text-align: center;
        color: white;
        p{
            margin-top: -10px;

            a{
                color: inherit;
                text-decoration: none;
            }
        }
    }

    .wrapper{
        width: 100%;
        display: flex;
        flex-direction: row;
        flex-wrap: nowrap;
        margin: auto;
        .flexOptions{
            width: 30vw;
            height: 80vh;
            padding: 5px;
            margin-left: 10px;
            border-radius: 5px;
            background-color: #5f5f5f8e;

            display: flex;
            flex-direction: row;
            flex-wrap: wrap;

            div{
                width: 45%;
                margin: auto;
                color: white;

                input, select{
                    margin-top: 5px;
                    width: 100%;
                    border-radius: 10px;
                    text-align: center;
                    border: 1px solid rgba(255, 255, 255, 0);
                    background-color: rgba(255, 255, 255, 0.726);
                    transition: border .25s ease-in;
                    &:focus{
                        outline: none;
                        border: 1px solid #EE2737FF;
                    }
                }
            }
            .btn{
                margin: auto;
                width: 45%;
                height: 50px;
                border-radius: 10px;
                border: none;
                background-color: rgba(238, 39, 56, 0.712);
                color: white;
                cursor: pointer;

                &:first-child{
                    background-color: rgba(126, 252, 0, 0.527);
                }

                &:hover{
                    color: black;
                }
            }

            .openModal{
                background-color: #1b1b1b;
                &:hover{
                    color: rgba(238, 39, 56, 0.712);
                }
            }

        }

        .flexContainer{
            /* Design of flex-container */
            margin-left: 10px;
            margin-right: 10px;
            padding: 5px;
            width: 70vw;
            height: 80vh;
            background-color: #5f5f5f8e;
            border-radius: 5px;

            /* Divs flex */
            display: flex;
            overflow: auto;
        }
    }

    .modal{
        position: absolute;
        z-index: 10;
        background-color: rgba(0, 0, 0, 0.63);
        width: 100vw;
        height: 100vh;
        top: 0;
        display: flex;
        justify-content: center;
        align-content: center;
        flex-direction: column;

        button{
            width: 300px;
            height: 30px;
            margin: auto;
            background-color: rgba(238, 39, 56, 0.712);
            border: none;
            border-radius: 5px;
            color: white;
            cursor: pointer;
            &:hover{
                color: black;
            }
        }

        .html, .css{
            margin: auto;
            overflow: auto;
            background-color: rgba(0, 0, 0, 0.76);
            width: 50%;
            color: white;
            font-weight: 300;
        }
    }

    @media (max-width: 960px) {
        .wrapper{
            display: flex;
            justify-content: center;
            flex-direction: column;
            align-content: center;

            .flexOptions{
                width: 90vw;
                margin: auto;
            }

            .flexContainer{
                width: 90vw;
                margin: auto;
                margin-top: 30px;
            }
        }

        .modal{
            width: 100vw;
            height: 120%;
            background-color: rgba(0, 0, 0, 0.788);
            button{
                margin-top: 30px;
            }
            .html, .css{
                width: 95vw;
            }
        }
    }
</style>
