<template>
    <div class="question-box-container">
        <b-jumbotron >
            <template slot='lead'>
                {{currentQuestion.question}}
            </template>
            <hr class="my-4"/>
            <b-list-group>
                <b-list-group-item 
                    v-for = "(answer, index) in answers" 
                    :key="index"
                    @click="selectAnswer(index)"
                >
                    {{answer}}
                </b-list-group-item>
            </b-list-group>
            <b-button variant="primary">Submit</b-button>
            <b-button @click="next" variant="success">Next</b-button>
        </b-jumbotron>
    </div>
</template>

<script>
export default {
    props:{
        currentQuestion : Object,
        next: Function,
        selectAnswer: Function
    },
    computed: {
        answers(){
            let answers = [...this.currentQuestion.incorrect_answers]
            answers.push(this.currentQuestion.correct_answer)
            return answers
        }
    }
}
</script>

<style scoped>
    .list-group {
        margin-bottom: 15px;
    }
    .list-group-item:hover{
        background: #EEE;
        cursor: pointer;
    }
    .btn{
        margin:0 5px;
    }
    
</style>