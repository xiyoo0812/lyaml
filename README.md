# lyaml
lua bindings for libyaml(https://github.com/yaml/libyaml.git).

# 依赖
- [lua](https://github.com/xiyoo0812/lua.git)5.3以上
- [luakit](https://github.com/xiyoo0812/luakit.git)一个luabind库
- [libyaml](https://github.com/yaml/libyaml.git)，源码已经包含在内
- 项目路径如下<br>
  |--proj <br>
  &emsp;|--lua <br>
  &emsp;|--lyaml <br>
  &emsp;|--luakit

# 接口说明
```lua
local yaml = require("lyaml")
--编码
--value: 输入的lua table
--res：输出yaml字符串
--err：错误信息
local res, err = yaml.encode(value)

--解码
--value: 输入的yaml字符串
--res：输出lua
local res = yaml.decode(value)

--保存到文件
--yamlfile: 保存的yaml文件名
--value: 输入的lua
--header: yaml的自定义头，不传使用默认
--res：成功或者失败
local ok = yaml.save("./bb.yaml", xxlua)

--从文件读取
--yamlfile: 读取的yaml文件名
--res：输出yaml字符串
--err：错误信息
local flua, ferr = yaml.open("./bb.yaml")

```

# 用法参考
```lua
--本示例使用了quanta引擎
--https://github.com/xiyoo0812/quanta.git

local log_dump  = logger.dump

local cyaml = [[
base: &base
  name: Everyone has same name
  id: 123456

foo: &foo
  <<: *base
  age: 10

bar: &bar
  <<: *base
  age: 20

]]

local xlua = yaml.decode(cyaml)
log_dump("lyxml decode yxml:{}",  xlua)
local yxml = yaml.encode(xlua)
log_dump("lyxml encode yxml:{}", yxml)

local ok = yaml.save("./bb.yaml", xlua)
log_dump("lyxml save yxml:{}", ok)
local flua = yaml.open("./bb.yaml")
log_dump("lyxml open yaml:{}", flua)


```
