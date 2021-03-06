### test
#### Day03 - HAproxy配置文件操作

#### 2016/12/8
1. 完成程序的简单实现思路。
2. 画好程序的流程图。
3. 构思实现功能所需要用到的代码。
4. 实现部分查询功能，但如果查询的是第二条backend，则无法实现。经过debug后发现只用backend开头来判断是有缺陷的，第二条及以后的backend会直接break；增加标示位的检查后可以正常执行。

#### 2016/12/9
1. 实现查询功能
2. 实现文件修改操作前先备份的功能

#### 2016/12/10
1. 添加功能需要分几种情况：没有backend记录；有backend记录没有server记录；有backend记录有server记录（即重复了）。
2. 情况一：直接添加backend和server记录；情况二：添加server记录；情况三：提示信息已经存在。
3. 由于每次文件操作前都有进行备份，为防止混淆，对文件进行重命名处理。
4. 完成删除功能，并且当backend下没有server信息时，删除backend信息。

#### 2016/12/11
1. 完成修改server信息功能。
2. 尽量减少重复代码。
3. 重新测试所有功能。
4. 完善程序交互文字。
5. 完成Readme。

---
#### 难点记录及解决方法
1. 查询功能如何控制读取的行数。（加入标示位，符合条件时开启，往后全部读取。到下一backend时，关闭标示，停止读取。）
2. 向已有的backend中添加新的server信息，如何写入文件。（加入标示位，通过当行的起始字符串和标示位的值来判断是否写入。）
3. 当backend下没有server信息时，backend信息也删除。（根据server信息列表的布尔值，来判断是否写入）

---
#### 测试情况总结
##### 查询
1. 要查询的信息，文件中存在。（返回结果）
2. 要查询的信息，文件中不存在。（返回提示）

##### 添加
1. 添加全新的backend和server信息。（末尾添加）
2. 已有backend信息，添加新的server信息。（server信息添加）
3. 重复添加已有的backend和server信息。（返回提示，不添加）

##### 修改
1. 要修改的backend和server信息，文件中不存在。（返回提示，无法修改）
2. 要修改的backend和server信息，文件中均已存在。（返回提示，不修改）
3. 要修改的backend信息存在，server信息不存在。（即正常修改）

##### 删除
1. 要删除的backend和server信息，文件中不存在。（返回提示，无法删除）
2. 要删除的backend信息存在，server信息不存在。（返回提示，无法删除）
3. 要删除的backend和server信息，文件中均已存在。（即正常删除）
4. 当backend下没有server信息时，backend信息也删除。（backend行不写入）

---
#### 未完成及不满意的地方
1. 删除功能由于需要判断backend下是否有server信息，保留了不少重复代码。
2. 在backend下没有信息被删除后，会有多余空行存在。