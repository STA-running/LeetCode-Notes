# `unordered_set`

## 声明

```cpp
#include <unordered_set>

unordered_set<int> s;               // 空集合
unordered_set<int> s(nums.begin(), nums.end());  // 从迭代器构造
```

## 核心操作

| 操作 | 写法 | 说明 |
|------|------|------|
| 查找 | `s.find(x) != s.end()` | 找到返回 true |
| 插入 | `s.insert(x)` | 已存在则什么都不做 |
| 删除 | `s.erase(x)` | 删除所有值为 x 的元素 |
| 清空 | `s.clear()` | |
| 大小 | `s.size()` | |
| 判空 | `s.empty()` | |

## 注意事项

- `find()` 返回迭代器，不能当布尔用
  ```cpp
  if (s.find(x))           // ❌
  if (s.find(x) != s.end()) // ✅ 找到了
  if (s.find(x) == s.end()) // ✅ 没找到
  ```

- `erase(x)` 会删除所有值为 x 的元素，不返回值

---

# `unordered_map`

## 声明

```cpp
#include <unordered_map>

unordered_map<int, int> map;             // 空字典
unordered_map<int, int> map = {{1, 2}};  // 初始化
```

## 核心操作

| 操作 | 写法 | 说明 |
|------|------|------|
| 键值访问 | `map[key]` | 不存在则创建默认值（int 为 0） |
| 安全访问 | `map.at(key)` | 不存在抛异常 |
| 查找 | `map.find(key) != map.end()` | |
| 存在判断 | `map.count(key)` | 返回 0 或 1 |
| 插入 | `map[key] = val` | 推荐 |
| 插入 | `map.insert({key, val})` | 已存在则不覆盖 |
| 删除 | `map.erase(key)` | |

## 注意事项

- `map[key]` 如果 key 不存在会创建默认值，这可能不是你想要的。如果只想判断存在性，用 `count()` 或 `find()`
- `map.find(key)` 返回迭代器，指向 `pair<const Key, Value>`，通过 `it->first` 取 key，`it->second` 取 value

---

# `vector`

## 声明

```cpp
#include <vector>

vector<int> v;                // 空
vector<int> v(10);            // 10 个元素，默认 0
vector<int> v(10, 5);         // 10 个元素，全是 5
vector<int> v = {1, 2, 3};    // 初始化列表
```

## 核心操作

| 操作 | 写法 | 说明 |
|------|------|------|
| 访问 | `v[i]` | 越界为未定义行为 |
| 安全访问 | `v.at(i)` | 越界抛异常 |
| 首元素 | `v.front()` | 返回引用，可修改 |
| 尾元素 | `v.back()` | 返回引用，可修改 |
| 末尾追加 | `v.push_back(x)` | |
| 末尾删除 | `v.pop_back()` | |
| 大小 | `v.size()` | 注意是 `size_t` 无符号整数 |
| 判空 | `v.empty()` | |
| 排序 | `sort(v.begin(), v.end())` | 需 `#include <algorithm>` |
| 反转 | `reverse(v.begin(), v.end())` | |

## 注意事项

- `v.size()` 返回 `size_t`（无符号），空 vector 时 `v.size() - 1` 会下溢成一个极大值
- 推荐先用 `int n = v.size()` 保存长度，避免下标运算中的类型问题
- `v.back()` 和 `v.front()` 在空 vector 上调用是未定义行为，先检查 `!v.empty()`

---

# 常用 STL 速查

## 容器选择

| 容器 | 特点 | 查 | 增 | 删 |
|------|------|----|----|----|
| `unordered_set` | 哈希集合、无序、O(1) | `find` | `insert` | `erase` |
| `unordered_map` | 哈希字典、无序、O(1) | `find` / `count` | `[]` / `insert` | `erase` |
| `set` | 有序、O(log n) | `find` | `insert` | `erase` |
| `map` | 有序字典、O(log n) | `find` | `[]` / `insert` | `erase` |
| `vector` | 动态数组、O(1)索引 | `[]` / `at` | `push_back` | `pop_back` |

## 刷题够用的操作

```cpp
// 通用
.size()     // 元素个数
.empty()    // 是否为空

// 所有集合/字典
.find(x) != .end()   // 存在
.find(x) == .end()   // 不存在
.count(x)            // 存在性（0 或 1）
.insert(x)           // 插入
.erase(x)            // 删除

// unordered_map 特有
map[key]    // 访问/创建，不存在则创建默认值
map.at(key) // 安全访问，不存在抛异常
```
