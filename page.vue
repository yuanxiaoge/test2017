<template>
	<div class="pagination">
		<div class="page">
			<ul v-show="totalpage != 0">
				<li class="pageNormal" :class="{'active': current == 1}" @click="goto(1)">首页</li>
				<li class="pageNormal" :class="{'active': current == 1}" @click="current-- && goto(current)">上一页</li>
				<li class="pageNumber" v-for="item in pages" :key="item" :class="{'active':current == item}" @click="goto(item)">{{item}}</li>
				<li class="pageNormal" :class="{'active': current == totalpage}" @click="current++ && goto(current)">下一页</li>
				<li class="pageNormal" :class="{'active': current == totalpage}" @click="goto(totalpage)">尾页</li>
			</ul>
		</div>
		<span class="pageMsg" >共{{allItems}}条,当前{{current}}/{{totalpage}}页</span>
	</div>
</template>

<script>
	export default {
	 
	  data(){
	    return {
	    	current: 1,
            showItem: 7,	//页面上显示7页
            allItems: 1000,	//数据总条数
            eachpage: 10,	//每页10条数据
	    }
	  },
	  computed:{
	  	totalpage() {	//总页数
	  		return Math.ceil(this.allItems / this.eachpage)
	  	},
	    pages:function(){
	    	var pag = [];
	    	if((this.totalpage <= this.showItem) || (this.current <= Math.ceil(this.showItem/2)) ){ //如果总页数很少或者当前项是中间项的前几项

               var i = Math.min(this.showItem, this.totalpage);
               while(i){
                   pag.unshift(i--);
               }
           }else{ //当前项不是中间项
               var middle = this.current - Math.floor(this.showItem / 2 ),//开始项
                   i = this.showItem;
               if( middle >  (this.totalpage - this.showItem)  ){
                   middle = (this.totalpage - this.showItem) + 1
               }
               while(i--){
                   pag.push( middle++ );
               }
           }       
         return pag
    	 }	  	
      },
	  filters:{
	    
	  },
	  methods:{
	  	goto:function(item){
          if(item == this.current) return;
            this.current = item;
            
        }
	  },
	  mounted(){
	   
	  },
	  watch:{
	    
	  }
	}

</script>
<style>
	.pagination {
		position: relative;
		font-family: MicrosoftYaHei;
	}
	.page {
		min-width: 200px;
		height: 38px;
		display: inline-block;
		background: #FFFFFF;
		border: 1px solid #D9E2E9;
		border-right: none;
		margin-right: 10px;
	}
	li{
		list-style: none;
	}
	ul{
		letter-spacing: -4px;
	}
	.page ul li{
		text-align: center;
		display: inline-block;
		font-family: MicrosoftYaHei;
		font-size: 14px;
		letter-spacing: 0px;
		cursor: pointer;		
	}
	.page li:hover{
		color: #FFFFFF;
		background: #0A7AFF;
	}
	.pageNormal {
		width: 84px;
		height: 38px;
		line-height: 38px;
		border-right: 1px solid #D9E2E9;
		margin: 0;
		padding: 0;
		color: #0187FF;
		background-color: #FFFFFF; 
	}
	.pageNumber {
		width: 34px;
		height: 38px;
		line-height: 38px;
		border-right: 1px solid #D9E2E9;
		margin: 0;
		padding: 0;
		color: #0187FF;
	}
	.pageMsg {
		width: 142px;
		height: 14px;
		font-size: 12px;
		color: #8B97A5;
		letter-spacing: 0px;
		line-height: 14px;
		position: absolute;
		bottom: 0;
	}
	.active {
		color: #DDE1E4;
		pointer-events:none;
	}

</style>



