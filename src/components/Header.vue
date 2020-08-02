<template>
	<div class="jumbotron py-1 px-0">
		<b-nav class="d-flex justify-content-center align-self-center">	
			<b-nav-item disabled><b><h2 class="text-light badge-pill bg-secondary p-3">Random Quizzing</h2></b></b-nav-item>
		</b-nav>		
		<b-nav class="d-flex justify-content-center align-self-center">
			<b-nav-item disabled><h6 class="text-light badge-pill bg-primary p-2"> Index: {{ index+1 }}/10 </h6>  </b-nav-item>
			<b-nav-item disabled><h6 class="text-light badge-pill bg-success p-2"> Correct: {{ numCorrect }} </h6>  </b-nav-item>
			<b-nav-item disabled><h6 class="text-light badge-pill bg-danger p-2"> Incorrect: {{ numIncorrect }} </h6>  </b-nav-item>
			<b-nav-item disabled><h6 class="text-dark badge-pill bg-warning p-2"> Attempted: {{ numIncorrect + numCorrect }} </h6>  </b-nav-item>			
		</b-nav>
	</div>
</template>

<script>
export default {
	props: [
		'numCorrect',
		'numTotal',
		'numIncorrect',
		'index'
	]
}
</script>