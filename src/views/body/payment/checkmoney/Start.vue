<template>
    <div class="content">
        
    </div>
</template>




<script>

var root = process.env.API_ROOT;

export default {
    data () {
        return {
            pageInitUrl: root + '/payment/checkmoney/start' ,
            errormsg:''
        }
    },
    created: function(){
        this.pageInit();
    },
    
    methods: {
        pageInit: function(){
            var self = this;
            self.errormsg = '';
            self.correctmsg = '';
            $.showIndicator();
            $.ajax({
                url: self.pageInitUrl,
                async: true,
                timeout: 120000,
                type: 'post',
                headers: self.getRequestHeader(),
                data:{ 
                },
                success:function(data, textStatus,request){
                    $.hideIndicator();
                    if(data.code == 200){
                        var traceData = {};
                        self.reloadTraceJs(traceData);
                        self.$router.push('/payment/success');
                    }
                    
                },
                error:function(){
                    $.hideIndicator();
                    console.log('');
                }
            });
        }  
    }
    
}
</script>