<template>
</template>

<script>
	export default {
		data() {
			return {
				form: {
					name: '',
					region: '',
					date1: '',
                    way:'',
                    type:[],
					date2: '',
                    pepole: '',
					type: [],
					resource: '',
					desc: '',
                    desc1:''
				}
			}
		},
		methods: {
			onSubmit() {
                this.$notify({
                    title: '成功',
                    message: '案件录入成功',
                    type: 'success'
                });
			}
		}
	}

</script>