<template>
	<div class="newsList">
		<towtop></towtop>
		<div class="container" style="min-height: 735px;">
			<div class="newTitle">
				{{title}}
			</div>
			<span class="newsTime">{{time}}</span>
			<div class="newContent">
				<p>{{content}}</p>
			</div>
		</div>
		<towbottom></towbottom>
	</div>
	
</template>

<script>
	import towtop from '@/components/testTop'
	import towbottom from '@/components/testBottom'
	export default {
		data() {
			return {
				title: this.$route.query.title,
				time: this.$route.query.time,
				content: this.$route.query.content,
			}
			
		},
		created() {

		},
		components: {
			towtop,
			towbottom
		},
		methods: {
			
		},

	}
</script>

<style>
	.newsList{margin-top: 160px;text-align: center;}
	.newTitle{font-size: 24px;}
	.newsTime{margin-bottom:60px;display: block;}
	.newContent {text-indent: 2em;line-height: 22px;}
</style>