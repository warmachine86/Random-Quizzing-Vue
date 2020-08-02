<template>
	<div class="question-box-container">
		<b-jumbotron class="p-3">
			<template slot="lead">
				{{ currentQuestion.question}}
			</template>

			<hr class="my-4" />
 
			<b-list-group>
				<b-list-group-item
				v-for="(answer, index) in shuffledAnswers"
				:key="index"
				:class="answerClass(index)"
				@click="selectAnswer(index)"
			>
				{{ answer }}
				</b-list-group-item>
			</b-list-group>

			<b-button 
				@click="clearAll" 
				variant="danger"
				:disabled="selectedIndex === null"
			>Clear
			</b-button>

			<b-button  
				variant="primary"
				@click="submitAnswer"
				:disabled="selectedIndex === null || answered"
			>
			Submit
			</b-button>

			<b-button 
				:class="nextCheck()"
				@click="next" 
				variant="success"
			>
			Next
			</b-button>
		</b-jumbotron>
	</div>
</template>

<script> 
import _ from 'lodash'

export default {
  props: {
    currentQuestion: Object,
	next: Function,
	increment: Function,
	nextCheck: Function
  },
  data: function() {
    return {
	selectedIndex: null,
	correctIndex: null,
	shuffledAnswers: [],
	answered: false
    }
  },
  computed: {
    answers() {
      let answers = [...this.currentQuestion.incorrect_answers]
      answers.push(this.currentQuestion.correct_answer)
      return answers
    }
  },
  watch: {
	currentQuestion: {
		immediate: true,
		handler() {
		this.selectedIndex = null;
		this.answered = false
		this.shuffleAnswers()
		}
	}
  },
  methods: {
	selectAnswer(index) {
		this.selectedIndex = index
	},
    submitAnswer() {
	let isCorrect = false
	if(this.selectedIndex === this.correctIndex) {
		isCorrect = true
	}
	this.answered = true
	this.increment(isCorrect)
    },
    shuffleAnswers(){
	let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
	this.shuffledAnswers =  _.shuffle(answers)
	this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)
	},
	clearAll(){
	this.selectedIndex = null
	},
	answerClass(index){
		if(!this.answered && this.selectedIndex === index) {
		return'selected' 
		}else if(this.answered && this.correctIndex === index){
		return 'correct'
		}else if(this.answered && this.selectedIndex===index && this.correctIndex !== index){
		return 'incorrect'
		} 		
	}
  }
}
</script>

<style scoped>
.btn{
	margin: 20px 3px 0px 3px;
}

.list-group-item:hover {
	background: #eee;
	cursor: pointer;
}

.selected{
	background-color: lightblue;
}

.correct{
	background-color: lightgreen;
}

.incorrect{
	background-color: #d9534f;
}
</style>