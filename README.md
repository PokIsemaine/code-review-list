# code-review-list
自用 code review 清单

# 通用
* 自动化工具和 CI 检查
* 类、结构体、函数的必要注释
* License

## Config
* 配置文件注释比代码中注释更重要，因为用户一般不看代码
* 注释包括
  * 开启/关闭会导致什么变化，有什么好处或坏处
  * 什么时候应该开启
  * 什么时候应该关闭
  * 默认是开启还是关闭
    * 实验性功能一般默认关闭，避免不必要的负面影响
    * 上线的需求功能也要配个开关，默认应该是开启的（中间也要走灰度之类的发布流程），开关主要是用来提供处理线上问题的途径
* 对于实验性功能应该增加一个配置开关来控制

# C++
## 逻辑
* 布尔运算组合简化

## 并发
* atomic<T>, is_lock_free 或 static_assert + is_always_lock_free 检查是否是无锁操作。特别是 T 比较大或者 T 是自定义的未来可能由于扩展变成非无锁操作

## 指针

* 检查一下所有 -> 的，运行时有没有可能 nullptr->，做好 IF 或者 DCHECK

## 类/结构体
* 成员函数、变量 + const
* 成员变量如果为指针类型，注意一下是否允许为 nullptr，如果不允许的话可以在 ctor 用 DCHECK 来检查

## API 设计
* 返回值
  * 带返回值的 const 的或者纯函数用 [nodiscard]
 
## lambda
* &捕获的时候精良精准
