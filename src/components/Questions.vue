<template>
	<div id='questions-wrapper'>
		<div id='progress'>
			<div
				:style='{width: `${(questionsAnswered / questions.length) * 100}%`}'
				id='bar'
			>
			</div>
			<div id='status'>{{ questionsAnswered }} out of {{ questions.length }} Questions Answered</div>
		</div>
		<TransitionGroup name='fade'>
			<div
				class='single-question'
				v-for='(question, index) in questions'
				:key='question.question'
				v-show='questionsAnswered === index'
			>
				<div class='question'>{{ question.question }}</div>
				<div class='answers'>
					<div
						class='answer'
						v-for='answer in question.answers'
						:key='answer.text'
						@click='onChooseAnswer(answer.isCorrect)'
					>
						{{ answer.text }}
					</div>
				</div>
			</div>
		</TransitionGroup>
	</div>
</template>

<script>
	export default {
		name: 'Questions',
		props: ['questions', 'questionsAnswered'],
		emits: ['answer-chosen'],
		methods: {
			onChooseAnswer(isCorrect) {
				this.$emit('answer-chosen', isCorrect);
			}
		}
	};
</script>