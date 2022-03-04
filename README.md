# snowflake_go
分布式唯一ID生成器, snowflake golang 版本的实现

# 用法
```
import snowflake
int63_abc := snowflake.NewID63()
```

# 各公司适配
```
说明:
1. 代码不错任何改动也可以使用, 使用的机器名做hash, 服务实例太多时冲突概率变大
2. 为了更好适配本公司的业务, 可以修改如下函数 getWorkerId_1024(), 该函数作用是获取服务实例号ID, 
   比如你们公司机器名是  some_module_cn01.123.docker, 这个函数就是获取结果是123

// 最多支持1024个实例
func getWorkerId_1024() uint64 {
   hostname := getHostname()
   instNo := getInstanceId()
   if instNo < 0 {
      instNo = int64(hashString(hostname))
   }
   instNo = instNo & ((1 << workerBits) - 1) // 保留10位
   return uint64(instNo)
}
```

# 特点 
1. 基本保证单调递增顺序 (仅时钟回拨时保证不了)
2. 支持时钟回拨
3. 一个服务最多支持1024个实例
4. 数字是 int63，有符号整数，转换为字符串最长是19位
5. 并发安全
6. 纯本地操作, 无网络IO


