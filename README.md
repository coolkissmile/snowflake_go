# snowflake_go
分布式唯一ID生成器, snowflake golang 版本的实现



# 特点 
1. 基本保证单调递增顺序 (仅时钟回拨时保证不了)
2. 支持时钟回拨
3. 时钟回拨时不保证递增
4. 数字是 int63，有符号整数，转换为字符串最长是19位
5. 并发安全
6. 纯本地操作, 无网络IO


# 用法
```
import snowflake
int63_abc := snowflake.NewID63()
```
