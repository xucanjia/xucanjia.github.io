---
layout: post
category: ['Thinkphp5']
title: Thinkphp5 代码片段
---
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