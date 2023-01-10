<template>
	<Header_component :correctCount="correctCount" :totalCount="totalCount" />
	<Content_component v-if="questionlist.length" :question="questionlist[index]" :next="next"
		:checkAnswer="checkAnswer" :msg="msg" />
</template>

<script>
import Header_component from './components/Header_component.vue';
import Content_component from './components/Content_component.vue';

export default {
	name: 'App',
	components: {
		Header_component,
		Content_component
	},
	data() {
		return {
			questionlist: [],
			index: 0,
			correctCount: 0,
			totalCount: 0,
			msg : ''
		}
	},
	mounted: function () {
		fetch('https://opentdb.com/api.php?amount=20').then((re) => {
			return re.json()
		}).then((result) => {
			this.questionlist = result.results;
		})
	},
	methods: {
		next() {
			if (this.index < this.questionlist.length - 1) {
				this.index++;
			}
		},
		checkAnswer(is_correct) {
			if (is_correct) {
				this.correctCount++;

			}
			if(this.totalCount < this.questionlist.length){
				this.totalCount++;
			}if(this.totalCount === this.questionlist.length){
				this.msg = `You finish the exam and you answer ${this.correctCount} out of ${this.totalCount} Correctly`
			}
			
		}
	}
}


</script>