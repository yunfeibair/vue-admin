<template>

    <section>
        <!--工具条-->
        <el-col :span="24" class="toolbar" style="padding-bottom: 0px;">
            <el-form :inline="true">
                <el-form-item>
                    <el-button type="primary">接警处</el-button>
                </el-form-item>
                <el-form-item>
                    <el-button type="primary">公安</el-button>
                </el-form-item>
                <el-form-item>
                    <el-button type="primary">警力</el-button>
                </el-form-item>
                <el-form-item>
                    <el-button type="primary">视频</el-button>
                </el-form-item>
                <el-form-item>
                    <el-button type="primary">重点人员车辆</el-button>
                </el-form-item>
                <el-form-item>
                    <el-button type="primary">警情分布</el-button>
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
            var map = new BMap.Map("XSDFXPage");    // 创建Map实例
            map.centerAndZoom(new BMap.Point(116.404, 39.915), 15);  // 初始化地图,设置中心点坐标和地图级别
            map.addControl(new BMap.MapTypeControl());   //添加地图类型控件
            map.enableDragging(); //开启拖拽
            map.setCurrentCity("北京");          // 设置地图显示的城市 此项是必须设置的
            map.centerAndZoom(point, 15);
            var opts = {
                width : 800,     // 信息窗口宽度
                height: 500,     // 信息窗口高度
                title : "朝阳区派出所人员详细信息" , // 信息窗口标题
                enableMessage:true,//设置允许信息窗发送短息
                message:"亲耐滴，晚上一起吃个饭吧？戳下面的链接看下地址喔~"
            }
            // 编写自定义函数,创建标注
            function addMarker(point) {
                var marker = new BMap.Marker(point);
                map.addOverlay(marker);
                var infoWindow = new BMap.InfoWindow(sContent,opts);
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
            for (var i = 0; i < 25; i++) {
                var point = new BMap.Point(sw.lng + lngSpan * (Math.random() * 0.7), ne.lat - latSpan * (Math.random() * 0.7));
                addMarker(point);
            }
            //点击标注弹出
            /*var local = new BMap.LocalSearch(map, {
                renderOptions: {map: map, panel: "r-result"}
            });
            local.search("餐饮");*/
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
<style lang="less" scope>
    .container .main .content-container{
        >div{
            height:100%;
        }
    }
</style>