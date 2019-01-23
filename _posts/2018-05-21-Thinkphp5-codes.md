---
layout: post
category: ['Thinkphp5']
title: Thinkphp5 代码片段
---

```php
// 在公共的common.php中

// 字符串截取并且超出显示省略号

function subtext($text, $length)

{

if(mb_strlen($text, ‘utf8’) > $length)

return mb_substr($text,0,$length,’utf8′).’ …’;

return $text;

}

// 在模版中调用则：

{$tops.title | subtext=18}
```
## 订单展示
比如上面的是一个订单的样式，可是有的订单只有一个商品，但是有的订单有多个商品，所以可能需要展示多个商品列表

也就是下面的那个框子里面要展示多个商品

而且上面的展示的是商品基本信息，下面展示的是订单商品信息

再看看我的数据表有goods商品表，order订单表，order_goods订单商品表

上面需要的所有的信息都包含在这三张表里面

有了下面的设计思路：

从order表里面查询到订单的基本信息：比如订单号、发货状态，收货人等

再从order_goods表里面找到当前订单的商品信息，并且循环在当前订单的基本信息下展示

再有就是order_goods里面没有存放商品的名称、缩略图基本信息，因为这些信息不能写死的商品订单表里面

所以还需要order_goods表关联goods商品表获取到商品的缩略图和商品名称等基本信息
```php
public function orderlist(){
        $uid = session('uid');
        $orderRes = db('order')->field('id,out_trade_no,user_id,order_total_price,order_status,pay_status,post_status,order_time,name')->where('user_id',$uid)->paginate(10,false,['query'=>request()->param()])->each(function($item, $key){
        $orderid = $item["id"]; //获取数据集中的id
        $goodsRes = db('orderGoods')->alias('og')->field('g.mid_thumb,g.goods_name,og.member_price,og.goods_attr_str,og.goods_num')->join('goods g',"g.id = og.goods_id")->where('order_id',$orderid)->select(); //根据ID查询相关其他信息
        $item['goods'] = $goodsRes; //给数据集追加字段num并赋值
        return $item;
    });
        $this->assign([
            'orderRes'=>$orderRes
            ]);
        return view();
    }
```
## paginate()分页后给结果集追加字段和数据
```php
public function index(){
    $sql = "";
    $list = "";
    $pagenumber = 20;//默认分页条数

    //查询数据
    $list = Db::name('wcmall_type','id,name,sort')->where($sql)->order('sort asc')->paginate($pagenumber,false,['query'=>request()->param()])->each(function($item, $key){
        $wctypeid = $item["id"]; //获取数据集中的id
        $num = Db::name('wcmall_type_attribute')->where("wctypeid='$wctypeid'")->count('id'); //根据ID查询相关其他信息
        $item['num'] = $num; //给数据集追加字段num并赋值
        return $item;
    });
    $page = $list->render();
    //输出到模板
    return view('type/index',['list'=>$list,'page'=>$page,'title'=>'商品类型']);

}
```
## 打印表单
```html
<button onclick="preview();" class="btn btn-success">打印表单</button>    <!-- //调用打印js代码 -->
<!--startprint--><!-- 打印开始位置符合 -->
<!-- 要打印的数据代码 -->
<!--endprint--><!-- //打印结束位置符合 -->
```
```javascript
<script type="text/javascript">
    function preview(){
         bdhtml=window.document.body.innerHTML;
         sprnstr="<!--startprint-->";//必须在页面添加<!--startprint-->和<!--endprint-->而且需要打印的内容必须在它们之间
         eprnstr="<!--endprint-->";
         prnhtml=bdhtml.substr(bdhtml.indexOf(sprnstr)+17);
         prnhtml=prnhtml.substring(0,prnhtml.indexOf(eprnstr));
         var newwin = window.open("");
         var css="<style>table{width: 100%; text-align: left; border-collapse: collapse; background: #fff; font: 16px '宋体'; color:#333;}"
         // +"table div{width: 16px; height: 16px; border: 1px solid #959595; margin: 0 auto; background: #fff;}"
         +"td {height: 22px; line-height: 22px; text-align: center; font-size: 14px;}"
         +"td.bgred { color: #ca231d; font-size:12px}"
         +"table div.current{background: url(../img/gou2.png) center no-repeat #fff;}</style>"
         newwin.document.body.innerHTML=css+prnhtml;
         newwin.print(); 
    }   

</script>
```
## 文件下载
```php
    public function downexcel()
    {
        $file_name = "fucai.xls";     //下载文件名    
        $file_dir = "./down/";        //下载文件存放目录    
        //检查文件是否存在    
        if (! file_exists ( $file_dir . $file_name )) {    
            header('HTTP/1.1 404 NOT FOUND');  
        } else {    
            //以只读和二进制模式打开文件   
            $file = fopen ( $file_dir . $file_name, "rb" ); 

            //告诉浏览器这是一个文件流格式的文件    
            Header ( "Content-type: application/octet-stream" ); 
            //请求范围的度量单位  
            Header ( "Accept-Ranges: bytes" );  
            //Content-Length是指定包含于请求或响应中数据的字节长度    
            Header ( "Accept-Length: " . filesize ( $file_dir . $file_name ) );  
            //用来告诉浏览器，文件是可以当做附件被下载，下载后的文件名称为$file_name该变量的值。
            Header ( "Content-Disposition: attachment; filename=" . $file_name );    

            //读取文件内容并直接输出到浏览器    
            echo fread ( $file, filesize ( $file_dir . $file_name ) );    
            fclose ( $file );    
            exit ();    
        }        
    }
```
## Excel导入
```php
    public function import()
    {
        //import('phpexcel.PHPExcel', EXTEND_PATH);//方法二
        vendor("PHPExcel.PHPExcel"); //方法一
        $objPHPExcel = new \PHPExcel();
 
        //获取表单上传文件
        $file = request()->file('excel');
        if (!$file) {
            $this->error('请选择文件!','index');
        }
        $path = ROOT_PATH . 'public' . DS . 'uploads'. DS . 'excel/';
        $info = $file->validate(['size'=>20480,'ext'=>'xlsx,xls,csv'])->move($path);
        if($info)
        {
            Db::startTrans();
            try{  
                $exclePath = $info->getSaveName();  //获取文件名
                $file_name = $path . $exclePath;   //上传文件的地址
                $objReader =\PHPExcel_IOFactory::createReader('Excel2007');
                if(!$objReader->canRead($file_name)){
                    $objReader = \PHPExcel_IOFactory::createReader('Excel5');
                }
                $obj_PHPExcel =$objReader->load($file_name, $encode = 'utf-8');  //加载文件内容,编码utf-8
              
                $excel_array=$obj_PHPExcel->getsheet(0)->toArray();   //转换为数组格式
                array_shift($excel_array);  //删除第一个数组(标题);
                $data = [];
                $i=0;
                foreach($excel_array as $k=>$v)
                {
                    $n = $k+2;
                    $typetxt = trim($v[0]);
                    if (!in_array($typetxt, ['单选','多选'])) throw new \think\Exception("请填写正确的类型文字!");

                    if ($typetxt =="单选") {
                        $type = 1;
                    }
                    if ($typetxt =="多选") {
                        $type = 2;
                    }

                    $data[$k]['type']    = $type;
                    $data[$k]['topic']   = trim($v[1]);
                    $data[$k]['choose1'] = trim($v[2]);
                    $data[$k]['choose2'] = trim($v[3]);
                    $data[$k]['choose3'] = trim($v[4]);
                    $data[$k]['choose4'] = trim($v[5]);
                    $data[$k]['answer']  = trim($v[6]);
                    $data[$k]['score']   = trim($v[7]);
                    $data[$k]['status']  = 1;
                    $data[$k]['create_time'] = date('Y-m-d H:i:s');
                    
                    if(!$data[$k]['topic']) throw new \think\Exception("表格第{$n}行,请填写题目!");
                    if(!$data[$k]['answer']) throw new \think\Exception("表格第{$n}行,请填写答案!");
                    if(!$data[$k]['choose1']) throw new \think\Exception("表格第{$n}行,请填写选项A!");
                    if(!$data[$k]['choose2']) throw new \think\Exception("表格第{$n}行,请填写选项B!");
                    if(!$data[$k]['choose3']) throw new \think\Exception("表格第{$n}行,请填写选项C!");
                    if(!$data[$k]['choose4']) throw new \think\Exception("表格第{$n}行,请填写选项D!");
                    if(!$data[$k]['score']) throw new \think\Exception("表格第{$n}行,请填写分值!");

                    if(!is_numeric($data[$k]['score']) || $data[$k]['score']<0) throw new \think\Exception("表格第{$n}行,请填写正确的分值!");

                    $cha = ['A','B','C','D'];
                    $answer = str_split($data[$k]['answer']);
                    foreach ($answer as $v) {
                        if (!in_array($v,$cha)) throw new \think\Exception("表格第{$n}行,答案选项只能是".implode(',', $cha));
                    }
                    $num = count($answer);
                    if ($data[$k]['type'] == 1) {
                        if ($num>1) throw new \think\Exception("表格第{$n}行,您选择了单选,请填写正确的答案!");
                    }

                    if ($data[$k]['type'] == 2) {
                        if ($num==1) throw new \think\Exception("表格第{$n}行,您选择了多选,请填写正确的答案!");
                    }     

                    $i++;
                }

                $success = Db::name('Test')->insertAll($data); //批量插入数据
   
                $error = $i-$success;

                if ($error != 0) throw new \think\Exception("插入失败,应该插入{$i}条,实际插入{$success}条");

                Db::commit();         
            } catch (\Exception $e) {
                Db::rollback();
                $this->error($e->getMessage());
            }            

            $this->success("导入成功!", 'index');            
        }
        else{
            $this->error($file->getError());            
        }
    }
```

## 整合Ueditor
[百度编辑器下载](http://ueditor.baidu.com/website/download.html)

```html
<div class="box box-primary">
    {include file="template/form_header" /}
    <form id="dataForm" class="dataForm form-horizontal" action="__URL__/updatespremark/proid/{$data.productid}/v/1" method="post" enctype="multipart/form-data">
        <div class="box-body">
             <div class="form-group">
                <label for="name" class="col-sm-2 control-label">商品详情</label>
                <div class="col-sm-10 col-md-4">
                    <textarea class="e1"  type="text/plain"  name="spremark1" id="EditorId1" placeholder="请输入内容">{$data.spremark1}</textarea>  
                </div>
            </div>      
            {include file="template/form_footer" /}
        </div>
    </form>
</div>

<script type="text/javascript" charset="utf-8">//初始化编辑器  
     window.UEDITOR_HOME_URL = "/ueditor/";//配置路径设定为UEditor所放的位置  
     window.onload=function(){  
        window.UEDITOR_CONFIG.initialFrameHeight=300;//编辑器的高度  
        window.UEDITOR_CONFIG.initialFrameWidth=600;//编辑器的宽度  
        var editor = new UE.ui.Editor({  
            imageUrl : '',  
            fileUrl : '',  
            imagePath : '',  
            filePath : '',  
            imageManagerUrl:'', //图片在线管理的处理地址  
            imageManagerPath:'__ROOT__/'  
        });  
        editor.render("EditorId1");//此处的EditorId与<textarea name="content" id="EditorId">的id值对应 </textarea>  
    }  
</script>  
```

# 查 增 改
```php
    // 查
    public static function findByOrderno($orderno)
    {
    $list = Db::name('orderkill')
        ->field('
            orderno,    
            killid,
            o.shopid,
            o.userid,
            o.product_id,
            o.product_num,
            post_time,
            post_amount,
            amount,
            addid,
            o.remark,
            o.update_time,
            s.shopname,
            k.title,
            u.username,
            p.spmc,
            sp.spgg,
            ad.province,
            ad.city,
            ')
        ->alias('o')
        ->join("bll_product p"," o.product_id = p.productid") // 商品名称
        ->join("bll_shop s"," o.shopid = s.shopid")// 门店名称
        ->join("bll_productkill k"," o.killid = k.id") // 秒杀主题
        ->join("bll_userinfo u"," o.userid = u.userid") // 用户名字
        ->join("bll_productspec sp"," o.pspecid = sp.pspecid")// 规格
        ->join("bll_useraddr ad"," o.addid = ad.rid")// 地址
        ->where(['orderno'=>$orderno])
        ->order('create_time desc')
        ->find();

    return $list;
}

// 增加
public static function add($data)
{
	return db('productgroup')->insert($data);
}

// 处理数据 并更新数据
$data['post_time'] =strtotime($data['post_time']);
$data['post_amount'] *=100;
$data['amount'] *=100;
$data['update_time'] =time();

return Db::name('orderkill')->where('orderno', $data['orderno'])->update($data);


```
----------
# 列表常用
```html
<!-- 列表页面常用 -->
<td>{$list.price_old/100}</td>
<td>{$list.price/100}</td>
<td>{$list.product_num}</td>
<td>{$list.bg_time|date="Y-m-d H:i",###}</td>
<td>{$list.ed_time|date="Y-m-d H:i",###}</td>
<td>{$list.peo_num}</td>
<td>{$list.limit_buy}</td>
<td>
	{switch name="list.post_status"}
	    {case value="0"}不包邮{/case}
	    {case value="1"}包邮{/case}
	{/switch}                        	
</td>

<td>
	{switch name="list.kstatus"}
	    {case value="0"}未开启{/case}
	    {case value="1"}已开启{/case}
	{/switch}
</td>
<td class="td-do">
    <a href="__URL__/view/id/{$list.id}"><button type="button" class="btn btn-primary btn-xs">查看</button></a>
    						
    <a href="__URL__/update/id/{$list.id}"><button type="button" class="btn btn-xs btn-danger">修改</button></a>   
</td>


<!-- 详情页或者修改页常用 -->
<div class="form-group">
    <label for="status" class="col-sm-2 control-label">订单状态</label>
    <div class="col-sm-10 col-md-4">
        {if condition="$list.status==1"}
            {foreach $list.status_text as $kk=>$status} 
                <div class="radio">
                  <label>
                    <input type="radio" name="status" id="" value="{$kk}" {if condition="$kk==$list.status"} checked {/if} disabled> 
                        {$status}{$kk}
                  </label>
                </div>
            {/foreach}
        {else /}
            {foreach $list.status_text as $kk=>$status} 
                <div class="radio">
                  <label>
                    <input type="radio" name="status" id="" value="{$kk}" {if condition="$kk==$list.status"} checked {/if} {if condition="$kk==1"} disabled {/if}> 
                        {$status}{$kk}
                  </label>
                </div>
            {/foreach}
        {/if}                            

    </div>
</div>
```
-----------
# ajax上传图片
```php
/**
 * 上传
 */
public function upload_photo()
{
    $file = $this->request->file('file');
    $uid = session('ydyl_weixin_user.id');
    $path = ROOT_PATH . 'public' . DS . 'uploads/banner';
    // if(empty($uid)){
    //     return ['code'=>404,'msg'=>'用户未登录'];
    // }
            if(!empty($file)){
                // 移动到框架应用根目录/public/uploads/ 目录下
                $info = $file->validate(['size'=>1048576,'ext'=>'jpg,png,gif'])->rule('uniqid')->move($path);
                $error = $file->getError();
                //验证文件后缀后大小
                if(!empty($error)){
                    dump($error);exit;
                }
                if($info){
                    // 成功上传后 获取上传信息
                    // 输出 jpg
                    $info->getExtension();
                    // 输出 20160820/42a79759f284b767dfcb2a0197904287.jpg
                    $info->getSaveName();
                    // 输出 42a79759f284b767dfcb2a0197904287.jpg
                    $photo = $info->getFilename();

                }else{
                    // 上传失败获取错误信息
                    $file->getError();
                }
            }else{
                $photo = '';
            }
    if($photo !== ''){
        return ['code'=>1,'msg'=>'成功','photo'=>'/uploads/banner/'.$photo];
    }else{
        return ['code'=>404,'msg'=>'失败'];
    }
}
 
```
```html
<div class="col-sm-10 col-md-4">
    <input class="form-control" value="{$list.url}"  type='hidden' name="url"
           id="url" maxlength=""
           placeholder="">
   <!-- 上传图片 -->
    <img class="imgurl" src="{$list.url}">
    <div class="upload-btn">
        <input type="file" name="pic1" id="pic" accept="image/gif,image/jpeg,image/x-png"/>
    </div>                   
</div>


<script>
    //上传图片
    $('#pic').change(function(event) {
        var formData = new FormData();
        formData.append("file", $(this).get(0).files[0]);
        $.ajax({
            url:'__URL__//upload_photo',
            type:'POST',
            data:formData,
            cache: false,
            contentType: false,    //不可缺
            processData: false,    //不可缺
            success:function(data){
                console.log(data);
                if (data.code != 1) {
                    $("#successMsg").html("上传失败,请检查图片大小或格式!").show(300).delay(200).fadeOut(900);  
                }else{
                    console.log(data.photo);
                    $(".imgurl").attr("src",data.photo);
                    $("#url").attr("value",data.photo);
                    $("#successMsg").html("上传成功!").show(300).delay(200).fadeOut(900);  
                }
            },

        });
    });
</script>
```