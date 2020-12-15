#### 类或者结构体中，数据成员在前，函数成员在后。
#### 枚举型每个类型是否都要显示指定值
#### 函数尽量不用返回值
底层函数设计时，没有返回值很正常，没有问题，设计时也可以往这个方向设计。

#### assert不要过多使用 
没必要的异常处理去掉，没必要的assert去掉。

#### 指针初始化用nullptr不要用NULL
```
MDSRankDispatcher *mds_rank = nullptr;
// tick and other timer fun
Context *tick_event = nullptr;
class MDSSocketHook *asok_hook = nullptr;
```

#### 判断值是否为0的方式
用!取反获取判断。

#### 构造函数初始化列表可以直接用this
构造函数中可以用this指针构造成成员，也可以用new来分配内存给成员，参考MDSRank::MDSRank：
```
DataManager::DataManager():
_dm_lock("dm::_dm_lock"),  _dm_state(DM_STATE_NONE),  _cache_table(new dm_hash_table_t(this)) {}
```

#### 析构函数不需要在free之后设置为nullptr
析构函数中delete指针指向的内存先判断指针是否为空，析构函数中的成员指针不需要赋值为null，参考class InoTable。

#### new返回值不需要校验是否为null
```
// start mds
mds = new MDSDaemon(g_conf()->name.get_id().c_str(), msgr, &mc, ctxpool);
```