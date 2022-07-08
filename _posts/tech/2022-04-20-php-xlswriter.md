---
layout: post
category: 技术
title: php-xlswriter 使用
---
# 优点
导大表excel时，PhpSpreadsheet会占用大量内存，
使用php-xlswriter，可以降低内存使用峰值，速度快。

# 缺点
样式、单元格操作不丰富。

# 下载
[文档地址](https://xlswriter-docs.viest.me/zh-cn/an-zhuang)
需根据安装的php版本进行下载，注意分nts或ts，
若为phpstudy，放置对应版本的ext目录下即可，启用对应扩展。

# 示例
```php
// phpinfo();

$config = [
  'path' => '/code/move/excel'
];

$excel = new \Vtiful\Kernel\Excel($config);

// 导出
$excel->fileName('rets.xlsx', 'sheet1')
    ->header(['Item', 'Cost'])
    ->data([
        ['Rent', 1000],
        ['Gas',  100],
        ['Food', 300],
        ['Gym',  50],
    ])
    ->output();

// 读取测试文件
$data = $excel->openFile('ceshi.xlsx')
    ->openSheet()
    ->getSheetData();

echo "<pre>";
var_dump($data);

// 插入图片
$excel = new \Vtiful\Kernel\Excel($config);

$freeFile = $excel->fileName("free.xlsx");

$freeFile->insertImage(5, 0, '/code/move/test.jpg');

$rs = $freeFile->output();
// var_dump($rs);
```
