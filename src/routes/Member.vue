<template>
    <div class="container">
 		<form @submit.prevent="submitForm">
			<div>
				<label for="id">id</label>
				<input type="text" id="id" v-model="member.id" />
			</div>
			<div>
				<label for="pw">pw</label>
				<input type="text" id="pw" v-model="member.pw" />
			</div>
			<div>
				<label for="addr">addr</label>
				<input type="text" id="addr" v-model="member.addr" />
			</div>
			<div>
				<label for="tel">tel</label>
				<input type="text" id="tel" v-model="member.tel" />
			</div>
			<button type="submit">수정</button>
		</form>
    </div>
</template>
<script>
import axios from 'axios';
export default{
    data(){
        return{
            member:{}
        }
    },
    async created(){
        const url=`http://localhost:8282/mvc1/member/member.do?id=${this.$route.params.id}`;
        const res=await axios.get(url);
        this.member=res.data.member;
    },
    methods:{
        async submitForm(){
			const data=JSON.stringify({"member":this.member});
            const url=`http://localhost:8282/mvc1/member/update.do?senddata=${data}`;
			const encodeURL=encodeURI(url);
        	const res=await axios.get(encodeURL);
        	console.log(res);
			this.$router.replace('/memberlist')	
        }
    }
}
</script>
<style scoped>
input { width:200px; }
</style>