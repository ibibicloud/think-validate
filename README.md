
## think-validate
基于版本 https://github.com/top-think/think-validate/tree/v3.0.7
文档地址 https://doc.thinkphp.cn/v8_0/validate.html
文档地址 https://doc.thinkphp.cn/@think-validate/default.html

### 安装
~~~
composer require ibibicloud/think-validate
~~~

### 主要特性
- 基于PHP8和强类型实现
- 内置丰富的验证规则
- 支持验证器类、数组和链式方法定义验证规则
- 支持验证场景和验证分组
- 支持独立数据验证
- 支持枚举验证
- 支持批量验证
- 支持抛出异常

### 用法 -> 独立验证
~~~
use think\facade\Validate;

$validate = Validate::rule([
    'name'  => 'require|max:25',
    'email' => 'email'
]);
$data = [
    'name'  => 'thinkphp',
    'email' => 'thinkphp#qq.com'
];
if ( !$validate->check($data) ) {
    var_dump($validate->getError());
}
~~~

### 用法 -> 验证器验证
~~~
<?php

namespace app\test\validate;

use think\Validate;

class User extends Validate
{
    protected $rule = [
        'name'  => 'require|max:25',
        'age'   => 'number|between:1,120',
        'email' => 'email',    
    ];
    
    protected $message = [
        'name.require' => '名称必须',
        'name.max'     => '名称最多不能超过25个字符',
        'age.number'   => '年龄必须是数字',
        'age.between'  => '年龄只能在1-120之间',
        'email'        => '邮箱格式错误哦，再瞅瞅',    
    ];
    
}
~~~

调用验证器代码如下：
~~~
$data = [
    'name'  => 'thinkphp',
    'email' => 'thinkphp#qq.com',
];

$validate = new \app\test\validate\User;

if ( !$validate->check($data) ) {
    var_dump($validate->getError());
}
~~~