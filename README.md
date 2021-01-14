# Smtp
---
# 介绍
电子邮件是—种用电子手段提供信息交换的通信方式，是互联网应用最广的服务。电子邮件几乎是每个web应用程序不可或缺的，无论是时事通讯还是订单确认。本库采用swoole协程客户端实现了电子邮件的发送，基于easyswoole/smtp修改增加设置发送者昵称

# 安装
```php
composer require lujihong/hyperf-smtp
```
# 用法
```php
use EasySwoole\Smtp\Mailer;
use EasySwoole\Smtp\MailerConfig;
use EasySwoole\Smtp\Message\Html;
use EasySwoole\Smtp\Message\Attach;
go(function (){
    
    $config = new MailerConfig();
    $config->setServer('smtp.163.com');
    $config->setSsl(true);
    $config->setUsername('username');
    $config->setPassword('password');
    $config->setMailFrom('mail from');
	$config->setFromNickname('nickname');//发送者昵称
    $config->setTimeout(10);//设置客户端连接超时时间
    $config->setMaxPackage(1024*1024*5);//设置包发送的大小：5M
    
    //设置文本或者html格式
    $mimeBean = new Html();
    $mimeBean->setSubject('Hello Word!');
    $mimeBean->setBody('<h1>Hello Word</h1>');
    
    //添加附件
    $mimeBean->addAttach(Attach::create('filepath'));
    
    
    $mailer = new Mailer($config);
    $mailer->sendTo('maile', $mimeBean);
});
```
