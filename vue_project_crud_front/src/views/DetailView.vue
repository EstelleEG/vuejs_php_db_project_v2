<template>
	<div>
		<div class="courses-container" >
			<div class="course" >
				<div class="course-preview">
					<img :src="book.imageURL" :alt="book.name" />
          {{book.imageURL}}
				</div>
				<div class="course-info">
					<div>{{ book.name }}</div>
					<br>
					<div>{{ book.author }}</div>
					<br>
					<div>{{ book.collection }}</div>
					<br>
					<div>{{ book.ISBN }}</div>
					<br>
					<div>{{ book.dimensions }}</div>
					<span></span>
				</div>
			</div>
		</div>
	</div>
</template>

<script>

import axios from "axios"

export default {
	name: 'DetailView',
	data: () => ({
		book: {}
	}),

	async created() {
		const { bookId } = this.$route.params
		console.log(bookId)
		const apiDetailsUri = 'http://picwebloire.fr/estelle/back/api/single_read.php/?id=' + bookId
		const oneBook = await axios.get(apiDetailsUri) //wait for the server to send me back the book
		this.book = oneBook.data
		console.log(this.book)

	},
}
</script>
<style scoped>
.courses-container {
	font-family: "Muli", sans-serif;
	display: flex;
	align-items: center;
	justify-content: center;
	color: black;
	flex-direction: column;
}

.course {
	background-color: #fff;
	border-radius: 10px;
	box-shadow: 0 10px 10px rgba(0, 0, 0, 0.2);
	display: flex;
	max-width: 100%;
	margin: 20px;
	overflow: hidden;
	width: 700px;
}

.course h6 {
	opacity: 0.6;
	margin: 0;
	letter-spacing: 1px;
	text-transform: uppercase;
}

.course h2 {
	letter-spacing: 1px;
	margin: 10px 0;
}

.course-preview {
	background-color: royalblue;
	color: #fff;
	padding: 30px;
	max-width: 250px;
}

.course-preview img {
	max-height: 250px;
}

.course-preview a {
	color: #fff;
	display: inline-block;
	font-size: 12px;
	opacity: 0.6;
	margin-top: 30px;
	text-decoration: none;
}

.course-info {
	padding: 30px;
	position: relative;
	width: 100%;
}


</style>
