<template>
    <main>
        <header>
            <img src="../assets/img/logo_ssaffe_2nd.png" alt="logo_ssaffe_2nd" style="height: 72px; padding-right: 10px;">
			<div style="margin-right: 0;">
				SSAFFE®
			</div>
			<div style="margin-right: auto; font-size: 8px; transform: translateY(-8px);">
				for Manager
			</div>


				<div class="shop-name" :class="{ isfold: isFold }" @click="toggleShop">{{ shopname }} {{ tri }}
					<div v-if="isFold">
						<div class="edit-info"><hr>기본정보 수정</div>
						<div class="edit-my-menu"><hr>내 가게 메뉴 편집</div>
					</div>
				</div>
        </header>
		<hr>
		<body>
			<div class="body-container">
				<div style="width: 600px; height: 100%;">
				<!-- <div style="width: 600px; height: 100%; background-color: aqua;"> -->
					<div class="input-container">
						<div class="input">
							<div class="input-title">가게명</div>
							<div class="input-content-container">
								<input class="input-text-big" type="text">
							</div>
						</div>
						<div class="input">
							<div class="input-title">비밀번호 변경</div>
							<div class="input-content-container">
								<input class="input-text-big" type="password">
							</div>
						</div>
						<div class="input">
							<div class="input-title">비밀번호 확인</div>
							<div class="input-content-container">
								<input class="input-text-big" type="password">
							</div>
						</div>
						<div class="input">
							<div class="input-title">대표전화번호</div>
							<div class="input-content-container">
								<input class="input-text-big" type="text">
							</div>
						</div>
						<div class="input">
							<div class="input-title">주소</div>
							<div class="input-content-container">
								<input class="input-text-big" type="text">
							</div>
						</div>
						<div class="input">
							<div class="input-title">임시휴업</div>
							<div class="input-content-container" style="justify-content: space-between;">
								<input @click="closeShop" class="button" :class="{clicked: state.isClosed}" type="button" value="ON">
								<input @click="openShop" class="button" :class="{clicked: !state.isClosed}" type="button" value="OFF">
							</div>
						</div>
						<div class="input">
							<div class="input-title">최소주문금액</div>
							<div class="input-content-container">
								<input class="input-text-big" type="text">
							</div>
						</div>
					</div>
					<div class="input">
							<div class="input-title"></div>
							<div class="input-content-container" style="justify-content: space-between;">
								<input style="color: black;" @click="applyShopSetting" class="button positive" :class="{clicked: state.isApplied }" type="button" value="적용">
								<input style="color: black;" @click="cancelShopSetting" class="button negative" :class="{clicked: state.isCanceled }" type="button" value="취소">
								<label className="input-file-button" for="input-file">파일 업로드</label>
								<input type="file" id="input-file" style="display:none;"/> 
							</div>
						</div>
				</div>
			</div>
		</body>
    </main>
</template>

<script setup>
import { ref, computed, reactive, onMounted } from 'vue';
import { useRoute, useRouter } from "vue-router";
import { getCreator, getOrderList } from '@/api/after.js'
const route = useRoute();
const router = useRouter();

const shopname = ref("컴포즈커피_광주장덕수완점");
const isFold = ref(false);

const tri = computed(() => { 
	return isFold.value ? "▲": "▼"});

	const toggleShop = () => {
	console.log("toggle")
	isFold.value = !isFold.value;
};

const openShop = () => {
	state.isClosed = false;
};

const closeShop = () => {
	state.isClosed = true;
};

const applyShopSetting = () => {
	state.isApplied = true;
	state.isCanceled = false;
};

const cancelShopSetting = () => {
	state.isApplied = false;
	state.isCanceled = true;
};

const state = reactive({
	isClosed: false,
	isApplied: false,
	isCanceled: false,
})

const shopName = ref("");
const passwordToChange = ref("");
const passwordToCertify = ref("");
const managerPhoneNumber = ref("");
const shopAddress = ref("");

</script>

<style lang="scss" scoped>
	main {
		height: 100%;
	}

	header {
		display: flex;
		align-items: center;
		flex-direction: row;
		width: 100%;
		height: 72px;
		font-size: 30px;
		font-weight: bold;
        white-space: normal;
		background-color: white;
		// border: 1px solid black;
		// z-index: 20;
	}

	body {
		margin: 0px;
	}

	.body-container {
		// background-color: pink;
		width: 100%;
		height: 88vh;
		display: flex;
		flex-direction: column;
		// justify-content: center;
		// align-content: center;
	}

	.isfold {
		color: black;
		background-color: #97AFBA;
		border-radius: 10px 10px 0px 0px;
		border-top: 2px solid black;
		border-left: 2px solid black;
		border-right: 2px solid black;
	}

	hr {
		width: 90%;
		padding: 0px;
		margin: 0px;
        border: none;
        border-top: 2px solid black;
        width: 100%;
	}

	.shop-name {
		color: #296A84; 
		width: 450px; 
		height:60px; 
		line-height: 60px; 
		text-align: center; 
		margin-right: 10px; 
		display: flex; 
		flex-direction: column; 
		align-items: center; 
		margin-right: 10px;
		cursor: pointer;
		z-index: 30;
	}

	.edit-info {
		width: 450px;
		height:60px; 
		line-height: 60px;
		background-color: #97AFBA;
		border-left: 2px solid black;
		border-right: 2px solid black; 
		text-align: center;
		display: flex; flex-direction: column; align-items: center;
	} 
	.edit-my-menu {
		width: 450px;
		height:60px; 
		line-height: 60px;
		background-color: #97AFBA;
		border-left: 2px solid black;
		border-right: 2px solid black; 
		border-bottom: 2px solid black;
		text-align: center; 
		border-radius: 0px 0px 10px 10px;
		display: flex; flex-direction: column; align-items: center;
		}
	
	.input-title {
		width: 200px; 
		height: 50px; 
		text-align: center; 
		line-height: 50px; 
		font-size: 20px; 
		font-weight: bold;
	}

	.input-content-container {
		width: 100%;  
		box-sizing: content-box;
		display: flex;
	}

	.input-text-big {
		height: 100%; 
		width: 100%; 
		border: 0; 
		padding-left: 20px; 
		margin-left: 0; 
		border-radius: 25px; 
		border: 2px solid black;
		font-size: 24px;
		font-weight: bold;
	}

	.input-text-small {
		height: 100%; 
		width: 200px; 
		border: 0; 
		// padding-left: 20px;  
		border-radius: 25px; 
		border: 2px solid black;
		font-size: 24px;
		font-weight: bold;
	}

	.input {
		display: flex; 
		margin: 10px;
	}

	.button {
		font-size: 20px;
		font-weight: bold;
		border: 0px;
		padding: 10px;
		margin-left: 10px;
		border-radius: 40px;
		width: 120px;
		height: 50px;
		// line-height: ;
		color: white;
	}

	.clicked {
		filter: brightness(0.6);
	}

	.positive {
		background-color: #36BAC3;
	}

	.negative {
		background-color: #EB4E5A;
	}

	.input-file-button{
  padding: 6px 25px;
  background-color:#FF6600;
  border-radius: 4px;
  color: white;
  cursor: pointer;}
</style>