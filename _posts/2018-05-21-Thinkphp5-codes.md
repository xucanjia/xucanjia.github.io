---
layout: post
category: ['Thinkphp5']
title: Thinkphp5 代码片段
---

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