<template>
    <div class="hello" id="editor">
       <!-- <textarea v-model="input"></textarea> -->
        <textarea :value="input" @input="updateWithDebounce"></textarea>
        <div v-html="compiledMarkdown"></div>
    </div>
</template>

<script lang="ts">
    import Vue from 'vue';
    import { Marked } from 'marked-ts';
    // import _ from 'lodash';
    // import { debounce } from 'typescript-debounce-decorator';
    import { debounce } from 'ts-debounce';

    export default Vue.extend({
        name: 'HelloWorld',
        props: {
            msg: String,
        },
        data() {
            return {
                input: '# hello',
            };
        },

        methods: {
           /* update(e) {
                this.input = e.target.value;
            },
            updateWithDebounce: _.debounce(update, 2000),
            update: _.debounce(function(e) {
                this.input = e.target.value;
            }, 2000),

           updateWithDebounce(e: any) {

               debounce(() => {this.input = e.target.value; console.log(e); }, 100);
           },*/

            updateWithDebounce: debounce(function(e: any) {
                this.input = e.target.value;
            }, 2000),


           update(e: any) {
                this.input = e.target.value;
            },

        },
        computed: {
            compiledMarkdown(): string {
                return Marked.parse(this.input);
            },
        },
    });
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
    h3
        margin 40px 0 0

    ul
        list-style-type none
        padding 0

    li
        display inline-block
        margin 0 10px

    a
        color #42b983

    #editor
        margin 0
        height 100%
        font-family 'Helvetica Neue', Arial, sans-serif
        color #333

    textarea, #editor div
        display inline-block
        width 49%
        height 100%
        vertical-align top
        box-sizing border-box
        padding 0 20px

    textarea
        border none
        border-right 1px solid #ccc
        resize none
        outline none
        background-color #f6f6f6
        font-size 14px
        font-family 'Monaco', courier, monospace
        padding 20px

    code
        color #f66
</style>
