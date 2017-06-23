<template>
	<section>
		<!--工具条-->
		<el-col :span="24" class="toolbar" style="padding-bottom: 0px;">
			<el-form :inline="true">
				<el-form-item>
					<el-button @click="seachF()" type="primary">法轮功涉案者</el-button>
					<el-button @click="seachJ()" type="primary">精神病患者</el-button>
					<el-button @click="seachX()" type="primary">涉疆人员</el-button>
					<el-button type="primary">备案人员</el-button>
				</el-form-item>
			</el-form>
		</el-col>
		<el-col :span="24" style="padding-bottom: 0px;height: 100%">
			<div id="XSDFXPage" class="XSDFXPage"></div>
		</el-col>

	</section>
</template>
<script>
    export default {
        name: '',
        data () {
            return {}
        },
        mounted() {
            // 百度地图API功能
            var sContent = `<div class="content-info">
                                 <div class="info-title">
                                   在职人数：200人
                                 </div>
                                 <div class="info">
                                    <table class="table table-bordered el-table__body">
                                        <thead>
                                          <tr>
                                            <th>编号</th>
                                            <th>姓名</th>
                                            <th>职位</th>
                                            <th>联系方式</th>
                                            <th>是否外勤</th>
                                          </tr>
                                        </thead>
                                        <tbody>
                                          <tr>
                                            <td>1</td>
                                            <td>王小虎</td>
                                            <td>所长</td>
                                            <td>158555334344</td>
                                            <td>否</td>
                                          </tr>
                                          <tr>
                                            <td>2</td>
                                            <td>王小虎</td>
                                            <td>所长</td>
                                            <td>158555334344</td>
                                            <td>否</td>
                                          </tr>
                                          <tr>
                                            <td>3</td>
                                            <td>王小虎</td>
                                            <td>所长</td>
                                            <td>158555334344</td>
                                            <td>否</td>
                                          </tr>
                                          <tr>
                                            <td>4</td>
                                            <td>王小虎</td>
                                            <td>所长</td>
                                            <td>158555334344</td>
                                            <td>否</td>
                                          </tr>
                                          <tr>
                                            <td>5</td>
                                            <td>王小虎</td>
                                            <td>所长</td>
                                            <td>158555334344</td>
                                            <td>否</td>
                                          </tr>
                                        </tbody>

                                    </table>
                                 </div>
                            </div>`;
            var people=`<table class="table table-bordered el-table__body"  align="center">
					<tr>
					<td>姓名</td>
					<td>李四 </td>
					<td>性别</td>
					<td>男</td>
					<td>出生年月</td>
					<td>1980.01.01</td>
					<td rowspan="3"><img width="100" src="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1497420561354&di=d0763da5dcbca38f5626a008eb9bdb91&imgtype=0&src=http%3A%2F%2Fs2.sinaimg.cn%2Forignal%2F3fe4678274aebc5849681"></td>
					</tr>
					<tr>
					<td>民族</td>
					<td>汉</td>
					<td>政治面貌</td>
					<td>群众</td>
					<td>身高</td>
					<td>175</td>
					</tr>
					<tr>
					<td>学制</td>
					<td>3</td>
					<td>学历</td>
					<td>高中</td>
					<td>户籍</td>
					<td>新疆</td>
					</tr>
					<tr>
					<td colspan="7">联系方式</td>
					</tr>
					<tr>
					<td>地址</td>
					<td colspan="2">某大厦某小区6号楼5-101</td>
					<td>联系电话</td>
					<td colspan="3">12222222222</td>
					</tr>
					<tr>
					<td>E-mail</td>
					<td colspan="2">222222222@163.com</td>
					<td>邮编</td>
					<td colspan="3">000000</td>
					</tr>
					<tr>
					<td colspan="7">备案信息</td>
					</tr>
					<tr>
					<td colspan="7" style="text-align: left" >
						xxxx年xx月xx日：拿刀伤害XX，被收留X天。</br>
						xxxx年xx月xx日:与某人公共场所打架
					</td>
					</tr>
                </table>`;
            var people1=`<table class="table table-bordered el-table__body"  align="center">
                <tr>
                <td>姓名</td>
                <td>张三 </td>
                <td>性别</td>
                <td>男</td>
                <td>出生年月</td>
                <td>1980.01.01</td>
                <td rowspan="3"><img width="100" src="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1497517760383&di=349a4561fdd6f42c244b995d0e0c7192&imgtype=0&src=http%3A%2F%2Fwww.ygjj.com%2Fbookpic%2F2009-01-26%2Fnew227681-20090126005350168318.jpg"></td>
                </tr>
                <tr>
                <td>民族</td>
                <td>汉</td>
                <td>政治面貌</td>
                <td>群众</td>
                <td>身高</td>
                <td>175</td>
                </tr>
                <tr>
                <td>学制</td>
                <td>3</td>
                <td>学历</td>
                <td>高中</td>
                <td>户籍</td>
                <td>新疆</td>
                </tr>
                <tr>
                <td colspan="7">联系方式</td>
                </tr>
                <tr>
                <td>地址</td>
                <td colspan="2">某大厦某小区6号楼5-101</td>
                <td>联系电话</td>
                <td colspan="3">12222222222</td>
                </tr>
                <tr>
                <td>E-mail</td>
                <td colspan="2">222222222@163.com</td>
                <td>邮编</td>
                <td colspan="3">000000</td>
                </tr>
                <tr>
                <td colspan="7">备案信息</td>
                </tr>
                <tr>
                <td colspan="7" style="text-align: left" >
                	xxxx年xx月xx日：拿刀伤害XX，被收留X天。</br>
                	xxxx年xx月xx日:与某人公共场所打架
				</td>
                </tr>
                </table>`
            var people2=`<table class="table table-bordered el-table__body"  align="center">
                <tr>
                <td>姓名</td>
                <td>王大虎 </td>
                <td>性别</td>
                <td>男</td>
                <td>出生年月</td>
                <td>1980.01.01</td>
                <td rowspan="3"><img width="100" src="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1497517906642&di=a95241c40cde7af0370dcc26ad34ce90&imgtype=0&src=http%3A%2F%2Fwanhuajing.com%2Fpic%2F1510%2F0513%2F4835571%2F12_263_361.jpg"></td>
                </tr>
                <tr>
                <td>民族</td>
                <td>汉</td>
                <td>政治面貌</td>
                <td>群众</td>
                <td>身高</td>
                <td>175</td>
                </tr>
                <tr>
                <td>学制</td>
                <td>3</td>
                <td>学历</td>
                <td>高中</td>
                <td>户籍</td>
                <td>新疆</td>
                </tr>
                <tr>
                <td colspan="7">联系方式</td>
                </tr>
                <tr>
                <td>地址</td>
                <td colspan="2">某大厦某小区6号楼5-101</td>
                <td>联系电话</td>
                <td colspan="3">12222222222</td>
                </tr>
                <tr>
                <td>E-mail</td>
                <td colspan="2">222222222@163.com</td>
                <td>邮编</td>
                <td colspan="3">000000</td>
                </tr>
                <tr>
                <td colspan="7">备案信息</td>
                </tr>
                <tr>
                <td colspan="7" style="text-align: left" >
                	xxxx年xx月xx日：拿刀伤害XX，被收留X天。</br>
                	xxxx年xx月xx日:与某人公共场所打架
				</td>
                </tr>

                </table>`
            var map = new BMap.Map("XSDFXPage");    // 创建Map实例
            map.centerAndZoom(new BMap.Point(116.404, 39.915), 15);  // 初始化地图,设置中心点坐标和地图级别
            map.addControl(new BMap.MapTypeControl());   //添加地图类型控件
            map.setCurrentCity("北京");          // 设置地图显示的城市 此项是必须设置的
            map.enableScrollWheelZoom(true);     //开启鼠标滚轮缩放
            map.centerAndZoom(point, 15);
            var opts = {
                width : 800,     // 信息窗口宽度
                height: 500,     // 信息窗口高度
                title : "朝阳区派出所人员详细信息" , // 信息窗口标题
                enableMessage:true,//设置允许信息窗发送短息
                message:"亲耐滴，晚上一起吃个饭吧？戳下面的链接看下地址喔~"
            };
            var opts = {
                width : 800,     // 信息窗口宽度
                height: 500,     // 信息窗口高度
                title : "法轮功修炼者李四详细信息" , // 信息窗口标题
                enableMessage:true,//设置允许信息窗发送短息
            };
            var opts1 = {
                width : 800,     // 信息窗口宽度
                height: 500,     // 信息窗口高度
                title : "精神病患者张三详细信息" , // 信息窗口标题
                enableMessage:true,//设置允许信息窗发送短息
            };
            var opts2 = {
                width : 800,     // 信息窗口宽度
                height: 500,     // 信息窗口高度
                title : "涉疆人员王大虎详细信息" , // 信息窗口标题
                enableMessage:true,//设置允许信息窗发送短息
            };
            // 编写自定义函数,创建标注
            function addMarker(point) {
                var marker=new BMap.Marker(point);
                map.addOverlay(marker);
                var infoWindow = new BMap.InfoWindow(people,opts);
                marker.addEventListener("click", function() {
                    this.openInfoWindow(infoWindow);
                })
            }
            function addMarker1(point) {
                var myIcon = new BMap.Icon("http://api.map.baidu.com/img/markers.png", new BMap.Size(23, 25), {
                    offset: new BMap.Size(10, 25), // 指定定位位置
                    imageOffset: new BMap.Size(0, 0 - 12 * 25) // 设置图片偏移
                });
                var marker=new BMap.Marker(point,{icon:myIcon});
                map.removeOverlay(marker);
                map.addOverlay(marker);
                var infoWindow = new BMap.InfoWindow(people1,opts1);
                marker.addEventListener("click", function() {
                    this.openInfoWindow(infoWindow);
                })
            }
            //涉疆人员
			function addMarker2(point) {
                var myIcon = new BMap.Icon("http://api.map.baidu.com/img/markers.png", new BMap.Size(23, 25), {
                    offset: new BMap.Size(10, 25), // 指定定位位置
                    imageOffset: new BMap.Size(0, 0 - 10 * 25) // 设置图片偏移
                });
                var marker=new BMap.Marker(point,{icon:myIcon});
                map.removeOverlay(marker);
                map.addOverlay(marker);
                var infoWindow = new BMap.InfoWindow(people2,opts2);
                marker.addEventListener("click", function() {
                    this.openInfoWindow(infoWindow);
                })
            }
            // 随机向地图添加25个标注
            var bounds = map.getBounds();
            var sw = bounds.getSouthWest();
            var ne = bounds.getNorthEast();
            var lngSpan = Math.abs(sw.lng - ne.lng);
            var latSpan = Math.abs(ne.lat - sw.lat);
            for (var i = 0; i < 5; i++) {
                var point = new BMap.Point(sw.lng + lngSpan * (Math.random() * 0.7), ne.lat - latSpan * (Math.random() * 0.7));
                addMarker(point);
            }
            for (var i = 0; i < 10; i++) {
                var point1 = new BMap.Point(sw.lng + lngSpan * (Math.random() * 0.7), ne.lat - latSpan * (Math.random() * 0.7));
                addMarker1(point1);
            }
            for (var i = 0; i < 15; i++) {
                var point2 = new BMap.Point(sw.lng + lngSpan * (Math.random() * 0.7), ne.lat - latSpan * (Math.random() * 0.7));
                addMarker2(point2);
            }
        },
        methods:{
            seachF:function () {
                var people=`<table class="table table-bordered el-table__body"  align="center">
                <tr>
                <td>姓名</td>
                <td>王小虎 </td>
                <td>性别</td>
                <td>男</td>
                <td>出生年月</td>
                <td>1980.01.01</td>
                <td rowspan="3"><img width="100" src="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1497420561354&di=d0763da5dcbca38f5626a008eb9bdb91&imgtype=0&src=http%3A%2F%2Fs2.sinaimg.cn%2Forignal%2F3fe4678274aebc5849681"></td>
                </tr>
                <tr>
                <td>民族</td>
                <td>汉</td>
                <td>政治面貌</td>
                <td>群众</td>
                <td>身高</td>
                <td>175</td>
                </tr>
                <tr>
                <td>学制</td>
                <td>3</td>
                <td>学历</td>
                <td>高中</td>
                <td>户籍</td>
                <td>新疆</td>
                </tr>
                <tr>
                <td colspan="7">联系方式</td>
                </tr>
                <tr>
                <td>地址</td>
                <td colspan="2">某大厦某小区6号楼5-101</td>
                <td>联系电话</td>
                <td colspan="3">12222222222</td>
                </tr>
                <tr>
                <td>E-mail</td>
                <td colspan="2">222222222@163.com</td>
                <td>邮编</td>
                <td colspan="3">000000</td>
                </tr>
                <tr>
                <td colspan="7">备案信息</td>
                </tr>
                <tr>
                <td colspan="7" style="text-align: left" >
                	xxxx年xx月xx日：拿刀伤害XX，被收留X天。</br>
                	xxxx年xx月xx日:与某人公共场所打架
				</td>
                </tr>

                </table>`
                var map = new BMap.Map("XSDFXPage");    // 创建Map实例
                map.centerAndZoom(new BMap.Point(116.404, 39.915), 15);  // 初始化地图,设置中心点坐标和地图级别
                map.addControl(new BMap.MapTypeControl());   //添加地图类型控件
                map.setCurrentCity("北京");          // 设置地图显示的城市 此项是必须设置的
                map.enableScrollWheelZoom(true);     //开启鼠标滚轮缩放
                map.centerAndZoom(point, 15);
                var opts = {
                    width : 800,     // 信息窗口宽度
                    height: 500,     // 信息窗口高度
                    title : "王小虎详细信息" , // 信息窗口标题
                    enableMessage:true,//设置允许信息窗发送短息
                    message:"亲耐滴，晚上一起吃个饭吧？戳下面的链接看下地址喔~"
                }
                var opts = {
                    width : 800,     // 信息窗口宽度
                    height: 500,     // 信息窗口高度
                    title : "王小虎详细信息" , // 信息窗口标题
                    enableMessage:true,//设置允许信息窗发送短息
                }
                // 编写自定义函数,创建标注
                function addMarker(point) {
                    var marker=new BMap.Marker(point);
                    map.removeOverlay(marker);
                    map.addOverlay(marker);
                    var infoWindow = new BMap.InfoWindow(people,opts);
                    marker.addEventListener("click", function() {
                        this.openInfoWindow(infoWindow);
                    })
                }
                var bounds = map.getBounds();
                var sw = bounds.getSouthWest();
                var ne = bounds.getNorthEast();
                var lngSpan = Math.abs(sw.lng - ne.lng);
                var latSpan = Math.abs(ne.lat - sw.lat);
                for (var i = 0; i < 5; i++) {
                    var point = new BMap.Point(sw.lng + lngSpan * (Math.random() * 0.7), ne.lat - latSpan * (Math.random() * 0.7));
                    addMarker(point);
                }
            },
            seachJ:function () {
                var people=`<table class="table table-bordered el-table__body"  align="center">
                <tr>
                <td>姓名</td>
                <td>王大虎 </td>
                <td>性别</td>
                <td>男</td>
                <td>出生年月</td>
                <td>1980.01.01</td>
                <td rowspan="3"><img width="100" src="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1497517906642&di=a95241c40cde7af0370dcc26ad34ce90&imgtype=0&src=http%3A%2F%2Fwanhuajing.com%2Fpic%2F1510%2F0513%2F4835571%2F12_263_361.jpg"></td>
                </tr>
                <tr>
                <td>民族</td>
                <td>汉</td>
                <td>政治面貌</td>
                <td>群众</td>
                <td>身高</td>
                <td>175</td>
                </tr>
                <tr>
                <td>学制</td>
                <td>3</td>
                <td>学历</td>
                <td>高中</td>
                <td>户籍</td>
                <td>新疆</td>
                </tr>
                <tr>
                <td colspan="7">联系方式</td>
                </tr>
                <tr>
                <td>地址</td>
                <td colspan="2">某大厦某小区6号楼5-101</td>
                <td>联系电话</td>
                <td colspan="3">12222222222</td>
                </tr>
                <tr>
                <td>E-mail</td>
                <td colspan="2">222222222@163.com</td>
                <td>邮编</td>
                <td colspan="3">000000</td>
                </tr>
                <tr>
                <td colspan="7">备案信息</td>
                </tr>
                <tr>
                <td colspan="7" style="text-align: left" >
                	xxxx年xx月xx日：拿刀伤害XX，被收留X天。</br>
                	xxxx年xx月xx日:与某人公共场所打架
				</td>
                </tr>

                </table>`
                var map = new BMap.Map("XSDFXPage");    // 创建Map实例
                map.centerAndZoom(new BMap.Point(116.404, 39.915), 15);  // 初始化地图,设置中心点坐标和地图级别
                map.addControl(new BMap.MapTypeControl());   //添加地图类型控件
                map.setCurrentCity("北京");          // 设置地图显示的城市 此项是必须设置的
                map.enableScrollWheelZoom(true);     //开启鼠标滚轮缩放
                map.centerAndZoom(point, 15);

                var opts = {
                    width : 800,     // 信息窗口宽度
                    height: 500,     // 信息窗口高度
                    title : "朝阳区派出所人员详细信息" , // 信息窗口标题
                    enableMessage:true,//设置允许信息窗发送短息
                    message:"亲耐滴，晚上一起吃个饭吧？戳下面的链接看下地址喔~"
                }
                var opts = {
                    width : 800,     // 信息窗口宽度
                    height: 500,     // 信息窗口高度
                    title : "王大虎详细信息" , // 信息窗口标题
                    enableMessage:true,//设置允许信息窗发送短息
                }
                // 编写自定义函数,创建标注
                function addMarker(point) {
                    var myIcon = new BMap.Icon("http://api.map.baidu.com/img/markers.png", new BMap.Size(23, 25), {
                        offset: new BMap.Size(10, 25), // 指定定位位置
                        imageOffset: new BMap.Size(0, 0 - 12 * 25) // 设置图片偏移
                    });
                    var marker=new BMap.Marker(point,{icon:myIcon});
                    map.removeOverlay(marker);
                    map.addOverlay(marker);
                    var infoWindow = new BMap.InfoWindow(people,opts);
                    marker.addEventListener("click", function() {
                        this.openInfoWindow(infoWindow);
                    })
                }
                var bounds = map.getBounds();
                var sw = bounds.getSouthWest();
                var ne = bounds.getNorthEast();
                var lngSpan = Math.abs(sw.lng - ne.lng);
                var latSpan = Math.abs(ne.lat - sw.lat);
                for (var i = 0; i < 5; i++) {
                    var point = new BMap.Point(sw.lng + lngSpan * (Math.random() * 0.7), ne.lat - latSpan * (Math.random() * 0.7));
                    addMarker(point);
                }
            },
            seachX:function () {
                var people=`<table class="table table-bordered el-table__body"  align="center">
                <tr>
                <td>姓名</td>
                <td>王大虎 </td>
                <td>性别</td>
                <td>男</td>
                <td>出生年月</td>
                <td>1980.01.01</td>
                <td rowspan="3"><img width="100" src="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1497517760383&di=349a4561fdd6f42c244b995d0e0c7192&imgtype=0&src=http%3A%2F%2Fwww.ygjj.com%2Fbookpic%2F2009-01-26%2Fnew227681-20090126005350168318.jpg"></td>
                </tr>
                <tr>
                <td>民族</td>
                <td>汉</td>
                <td>政治面貌</td>
                <td>群众</td>
                <td>身高</td>
                <td>175</td>
                </tr>
                <tr>
                <td>学制</td>
                <td>3</td>
                <td>学历</td>
                <td>高中</td>
                <td>户籍</td>
                <td>新疆</td>
                </tr>
                <tr>
                <td colspan="7">联系方式</td>
                </tr>
                <tr>
                <td>地址</td>
                <td colspan="2">某大厦某小区6号楼5-101</td>
                <td>联系电话</td>
                <td colspan="3">12222222222</td>
                </tr>
                <tr>
                <td>E-mail</td>
                <td colspan="2">222222222@163.com</td>
                <td>邮编</td>
                <td colspan="3">000000</td>
                </tr>
                <tr>
                <td colspan="7">备案信息</td>
                </tr>
                <tr>
                <td colspan="7" style="text-align: left" >
                	xxxx年xx月xx日：拿刀伤害XX，被收留X天。</br>
                	xxxx年xx月xx日:与某人公共场所打架
				</td>
                </tr>

                </table>`
                var map = new BMap.Map("XSDFXPage");    // 创建Map实例
                map.centerAndZoom(new BMap.Point(116.404, 39.915), 15);  // 初始化地图,设置中心点坐标和地图级别
                map.addControl(new BMap.MapTypeControl());   //添加地图类型控件
                map.setCurrentCity("北京");          // 设置地图显示的城市 此项是必须设置的
                map.enableScrollWheelZoom(true);     //开启鼠标滚轮缩放
                map.centerAndZoom(point, 15);

                var opts = {
                    width : 800,     // 信息窗口宽度
                    height: 500,     // 信息窗口高度
                    title : "朝阳区派出所人员详细信息" , // 信息窗口标题
                    enableMessage:true,//设置允许信息窗发送短息
                    message:"亲耐滴，晚上一起吃个饭吧？戳下面的链接看下地址喔~"
                }
                var opts = {
                    width : 800,     // 信息窗口宽度
                    height: 500,     // 信息窗口高度
                    title : "王大虎详细信息" , // 信息窗口标题
                    enableMessage:true,//设置允许信息窗发送短息
                }
                // 编写自定义函数,创建标注
                function addMarker(point) {
                    var myIcon = new BMap.Icon("http://api.map.baidu.com/img/markers.png", new BMap.Size(23, 25), {
                        offset: new BMap.Size(10, 25), // 指定定位位置
                        imageOffset: new BMap.Size(0, 0 - 10 * 25) // 设置图片偏移
                    });
                    var marker=new BMap.Marker(point,{icon:myIcon});
                    map.removeOverlay(marker);
                    map.addOverlay(marker);
                    var infoWindow = new BMap.InfoWindow(people,opts);
                    marker.addEventListener("click", function() {
                        this.openInfoWindow(infoWindow);
                    })
                }
                var bounds = map.getBounds();
                var sw = bounds.getSouthWest();
                var ne = bounds.getNorthEast();
                var lngSpan = Math.abs(sw.lng - ne.lng);
                var latSpan = Math.abs(ne.lat - sw.lat);
                for (var i = 0; i < 5; i++) {
                    var point = new BMap.Point(sw.lng + lngSpan * (Math.random() * 0.7), ne.lat - latSpan * (Math.random() * 0.7));
                    addMarker(point);
                }
            }
		}

    }
</script>

<style lang="less">
	section {
		height: 100%;
	}
	.XSDFXPage{
		height: 80%;
	}
	.BMap_cpyCtrl {
		display: none;
	}

	.anchorBL {
		display: none;
	}
	.table-bordered {
		border: 1px solid #ddd;
		border-spacing: 0;
		border-collapse: collapse;
		margin:0 auto;
		width: 100%;
	}
	.table-bordered>tbody>tr>td, .table-bordered>tbody>tr>th, .table-bordered>tfoot>tr>td, .table-bordered>tfoot>tr>th, .table-bordered>thead>tr>td, .table-bordered>thead>tr>th {
		border: 1px solid #ddd;
		text-align: center;
	}
	.table>tbody>tr>td, .table>tbody>tr>th, .table>tfoot>tr>td, .table>tfoot>tr>th, .table>thead>tr>td, .table>thead>tr>th {
		padding: 8px;
		line-height: 1.42857143;
		vertical-align: top;
	}
	.content-info{
		overflow: auto;
	}
	.BMap_bubble_title{
		text-align: center!important;
		line-height: 35px !important;
	}
</style>