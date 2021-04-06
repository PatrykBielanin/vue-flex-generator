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

        <p class="footer">visit <span style="color: orange;"><a href="https://github.com/PatrykBielanin/vue-flex-generator" target="_blank">GitHub</a></span></p>

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
    @import '../../styles/Flex.scss';
</style>
