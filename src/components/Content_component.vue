<template >
    <div class="col-sm-6 offset-3">

        <div v-if="msg.length > 0" class="alert alert-success" role="alert">
            <h4 class="alert-heading">Well done!</h4>
            <p>{{ msg }}</p>
            <hr>
            <button type="button" class="btn btn-primary" @click="reloadPage">take me an other exam</button>
        </div>
        <div class="jumbotron ">
            <h1 class="display-4">{{ question.category }} :</h1>
            <p class="lead">{{ question.question }}</p>
            <span>difficulty : {{ question.difficulty }}</span>
            <hr class="my-4">
            <ul class="list-group">
                <li class="list-group-item" v-for="(answer, i) in shuffledAnswers" :key="i" @click="saveIndex(i)"
                    :class="[cindex === i ? 'selected' : '']">{{ answer }}</li>
            </ul>
            <button class="btn btn-success btn-lg" href="#" role="button" @click="submitAnswer"
                :disabled="cindex === null">Submit</button>
        </div>
    </div>
</template>

<script>

import _ from 'lodash'
export default {
    data() {
        return {
            cindex: null,
            shuffledAnswers: [],
            componentKey: 0
        }
    },
    props: {
        question: Object,
        checkAnswer: Function,
        next: Function,
        msg: String,
    },
    methods: {
        saveIndex(index) {
            this.cindex = index
            console.log(this.cindex);
        },
        submitAnswer() {
            let is_correct = false;
            if (this.cindex === this.shuffledAnswers.indexOf(this.question.correct_answer)) {
                is_correct = true;
            }
            this.checkAnswer(is_correct)
            this.next()

        },
        shuffleAnswer() {
            let answers = [...this.question.incorrect_answers, this.question.correct_answer];
            this.shuffledAnswers = _.shuffle(answers)
        },
        reloadPage() {
            window.location.reload();
        }

    },

    watch: {
        question: {
            immediate: true,
            handler() {
                this.cindex = null;
                this.shuffleAnswer();
            }

        }
    }
}
</script>


<style scoped>
.btn {
    margin: 10px 3px;
}

.list-group-item:hover {
    background-color: #eee;
    cursor: pointer;
}

.selected {
    background-color: lightblue;
}

.connrect {
    background-color: lightgreen;
}

.wrong {
    background-color: lightcoral;
}
</style>