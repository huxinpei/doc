## FastCache组件
EasySwoole FastCache组件通过新开进程,使用SplArray存储,unix sock 高速通信方式,实现了多进程共享数据.

> 该组件为 3.0.8 版本新增，如需要使用，请手动增加 `FAST_CACHE.PROCESS_NUM` 配置项到配置文件里

### 使用配置:
```
FAST_CACHE.PROCESS_NUM = 1 进程数
```

### 简单示例:
```php
<?php
$cache = \EasySwoole\EasySwoole\FastCache\Cache::getInstance();
$cache->set('name','仙士可');
$cache->set('name2','仙士可2号');//设置
$cache->unset('name');//销毁
$keys = $cache->keys();//获取全部key
$str = "现在存储的数据有:";
foreach ($keys as $key) {
    $value = $cache->get($key);//获取
    $str .= "$key:$value\n";
}
echo $str;
```
### 全部例子:
```php
<?php
$cache = Cache::getInstance();
$cache->set('name', '仙士可');//设置
$cache->get('name');//获取
$cache->keys();//获取所有key
$cache->unset('name');//删除key
$cache->flush();//清空所有key
($cache->enQueue('listA', '1'));//增加一个队列数据
($cache->enQueue('listA', '2'));//增加一个队列数据
($cache->enQueue('listA', '3'));//增加一个队列数据
var_dump($cache->queueSize('listA'));//队列大小
//      var_dump(  $cache->unsetQueue('listA');//删除队列
//        var_dump($cache->queueList('listA'));//队列列表
var_dump($cache->flushQueue());//清空队列
var_dump($cache->deQueue('listA'));//出列
var_dump($cache->deQueue('listA'));//出列



```

> FastCache只能在服务启动之后使用,需要有创建unix sock权限(WSL子系统没有sock权限,请换成linux系统或虚拟机,docker等环境)