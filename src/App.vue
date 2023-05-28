<template>
	<div id='wrapper'>
		<Transition name='fade' mode='out-in'>
			<Questions
				:questions='questions'
				:questionsAnswered='questionsAnswered'
				@answer-chosen='onAnswerChosen'
				v-if='questionsAnswered < questions.length'
			/>
			<Result :results='results' :correctAnswers='correctAnswers' v-else />
		</Transition>
		<button id='reset-button' @click='reset' v-show='questionsAnswered === questions.length'>Reset</button>
	</div>
</template>

<script>
	import Questions from '@/components/Questions.vue'
	import Result from '@/components/Result.vue'

	export default {
		name: 'App',
		components: {
			Questions,
			Result
		},
		data() {
			return {
				questionsAnswered: 0,
				correctAnswers: 0,
				questions: [
					{
						question: 'What is 2 + 2?',
						answers: [
							{
								text: '4',
								isCorrect: true
							},
							{
								text: '3',
								isCorrect: false
							},
							{
								text: 'fish',
								isCorrect: false
							},
							{
								text: '5',
								isCorrect: false
							}
						]
					},
					{
						question: 'How many letters are in the word \'banana\'?',
						answers: [
							{
								text: '5',
								isCorrect: false
							},
							{
								text: '7',
								isCorrect: false
							},
							{
								text: '6',
								isCorrect: true
							},
							{
								text: '12',
								isCorrect: false
							}
						]
					},
					{
						question: 'find the missing letter: c_ke',
						answers: [
							{
								text: 'e',
								isCorrect: false
							},
							{
								text: 'a',
								isCorrect: true
							},
							{
								text: 'i',
								isCorrect: false
							}
						]
					},
				],
				results: [
					{
						minimum: 0,
						maximum: 2,
						title: 'Try Again!',
						description: 'Do a Little More Studying and You May Succeed!'
					},
					{
						minimum: 3,
						maximum: 3,
						title: 'Wow, You\'re a Genius!',
						description: 'Studying has Definitely Paid Off for You!'
					}
				]
			}
		},
		methods: {
			onAnswerChosen(isCorrect) {
				if (isCorrect) {
					this.correctAnswers++;
				};

				this.questionsAnswered++;
			},
			reset() {
				this.questionsAnswered = 0;
				this.correctAnswers = 0;
			}
		}
	};
</script>