<template>
    <div>
		<h1>当前求和为：{{sum}}</h1>
		<h3>当前求和乘10倍为：{{bigSum}}</h3>
		<h3>我在{{school}}，学习{{subject}}</h3>
		<h3 style="color:red">下方组件的总人数是：{{personList.length}}</h3>
		<select v-model.number="n">
			<option :value="1">1</option>
			<option :value="2">2</option>
			<option :value="3">3</option>
		</select>
		<button @click="increment(n)">+</button>
		<button @click="decrement(n)">-</button> 
		<button @click="incrementOdd(n)">当前求和为奇数再加</button>
		<button @click="incrementWait(n)">等一等再加</button>
	</div>
</template>

<script>
	import { mapState,mapGetters,mapMutations, mapActions } from 'vuex'
    export default {
        name:'Count',
		data() {
			return {
				n:1,
			}
		},
		computed: {
			//数组写法
			...mapState('countAbout',['sum','school','subject']),
			...mapState('personAbout',['personList']),

			/* ************************************************************************** */

			//数组写法
			...mapGetters('countAbout',['bigSum'])
		},
		methods: {
			//借助mapMutations生成对应的方法，方法中会调用commit去联系mutations（对象写法）
			...mapMutations('countAbout',{increment:'JIA',decrement:'JIAN'}),

			//对象写法
			...mapActions('countAbout',{incrementOdd:'jiaOdd',incrementWait:'jiaWait'})

		},
		mounted() {
		},
	}
</script>

<style scoped>
	button{
		margin-left: 5px;
	}
</style>