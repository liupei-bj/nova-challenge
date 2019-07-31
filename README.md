# nova-challenge
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>NOVA</title>
    <script type="text/javascript" src='echarts.js'></script>
</head>
<body>
	<div>
		<h2 align="center" style="color: #8D6103">目标客户匹配程度对比</h3>
		<div id="jscs" align="center" style="margin: 10px">出行频率: <input type="text" id="cxpl" name="cxpl" placeholder="0~3">
			&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp飞行里程: <input type="text" id="fxlc" name="fxlc" placeholder="0~3">
			<br>
			雇主评价: <input type="text" id="gzpj" name="gzpj" placeholder="0~5">
			可持续增长率: <input type="text" id="kcxzzl" name="kcxzzl" placeholder="0~40">
			<br><br><input type="submit" value="提交" style="width: 100px;background-color:#BCA9DB" onClick="newechart()"></div>
		<div id="chart" style="width:1000px;height:500px;margin: auto;border: #F40E5D"></div>
	</div>
</body>
<script type="text/javascript">
    // 初始化图表标签
    var myChart = echarts.init(document.getElementById('chart'));
	
    var option = {
    title : {
        text: '产品 vs 企业（Product vs Targets）',
    },
    tooltip : {
        trigger: 'axis'
    },
    legend: {
        orient : 'vertical',
        x : 'right',
        y : 'bottom',
        data:['产品（Product）','企业（Targets）']
    },
    toolbox: {
        show : true,
        feature : {
            mark : {show: true},
            dataView : {show: true, readOnly: false},
            restore : {show: true},
            saveAsImage : {show: true}
        }
    },
    polar : [
       {
           indicator : [
               { text: '雇主评价（Employer valuation）', max: 5},
               { text: '出行频率（Travel frequency）', max: 3},
               { text: '飞行里程（Flight mileage）', max: 3},
               { text: '可持续增长率（Substantial growth rate）', max: 40},
     
            ]
        }
    ],
    calculable : true,
    series : [
        {
            name: '产品 vs 企业（Product vs Targets）',
            type: 'radar',
            data : [
                {
                    value : [2,1.2,1.2,10],
                    name : '产品（Product）'
                },
                 {
                    value : [2.1,1.2,2,22],
                    name : '企业（Targets）'
                }
            ]
        }
    ]
};
	function newechart(){    
    function fetchData(cb) {
	
    // 通过 setTimeout 模拟异步加载
    setTimeout(function () {
       cb({
		   gzpj:document.getElementById("gzpj").value,
		   cxpl:document.getElementById("cxpl").value,
		   fxlc:document.getElementById("fxlc").value,
		   kcxzzl:document.getElementById("kcxzzl").value,
	   });
},1000);
	}
 
fetchData(function (data) {
    myChart.setOption({
        series: [{
            // 根据名字对应到相应的系列
            data : [
                {
                    value : [2,1.2,1.2,10],
                    name : '产品（Product）'
                },
                 {
                    value : [data.gzpj,data.cxpl,data.fxlc,data.kcxzzl],
                    name : '企业（Targets）'
                }
        ]
    }]
		});
});
        myChart.setOption(option);
}
                    
                    
    myChart.setOption(option);
	
	
</script>
</html>
