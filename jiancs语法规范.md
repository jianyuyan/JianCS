# JianCS (C# 皮肤层) 语法规范 v2.0（公开版）

> **一句话定义：** JianCS 是 C# 的纯语法糖——用中文关键词 + 类型后置语法写 C#，语义 100% 兼容，可无损逆转换回标准 C#。
>
> **核心理念：** 让熟悉中文的 .NET 开发者零摩擦上手 C#，同时保留 C# 的所有强大特性。

---

## 一、5 秒看懂 JianCS

```jiancs
// 这是 JianCS 代码
引用 System;

kaif sjgnbao 问候 {
    kaif 说你好(名字: string) {
        Console.WriteLine($"你好, {名字}!");
    }
}

kaif sjgnbao 程序 {
    kaif quanju 入口() {
        shu 问候器 = new 问候();
        问候器.说你好("世界");
    }
}
```

编译后就是标准 C#：

```csharp
using System;

public class 问候 {
    public void 说你好(string 名字) {
        Console.WriteLine($"你好, {名字}!");
    }
}

public class 程序 {
    public static void Main() {
        问候 问候器 = new 问候();
        问候器.说你好("世界");
    }
}
```

---

## 二、核心关键词映射表

| JianCS | C# | 说明 |
| :--- | :--- | :--- |
| `kaif` | `public` | 公开访问 |
| `siyou` | `private` | 私有访问 |
| `neibu` | `internal` | 内部访问 |
| `baohu` | `protected` | 受保护访问 |
| `shu` | `var` 或显式类型 | 变量声明 |
| `gn` | 方法（含 `void`） | 功能定义 |
| `fanhui` | `return` | 返回值 |
| `ben` | `this` | 当前实例 |
| `base` | `base` | 父类调用 |
| `sjgnbao` | `class` | 引用类型（类） |
| `shujubao` | `struct` | 值类型（结构体） |
| `gnlantu` | `interface` | 接口 |
| `xuanxiangdan` | `enum` | 枚举 |
| `quanju` | `static` | 静态成员 |
| `xu` | `virtual` | 虚方法 |
| `fugai` | `override` | 重写方法 |
| `mifeng` | `sealed` | 密封类/方法 |
| `abstract` | `abstract` | 抽象类/方法 |
| `readonly` | `readonly` | 只读字段 |
| `功能盒` | `delegate` | 委托定义 |
| `event` | `event` | 事件声明 |
| `引用` | `using` | 命名空间导入 |
| `mok` | `namespace` | 命名空间 |
| `后台` | `async` | 异步方法 |
| `等` | `await` | 等待异步任务 |
| `zhuge` | `for` | for 循环 |
| `zhiyao` | `while` | while 循环 |
| `遍历` | `foreach` | foreach 循环 |
| `尝试` | `try` | 异常处理块 |
| `捕获` | `catch` | 异常捕获 |
| `最终` | `finally` | 最终执行块 |
| `抛出` | `throw` | 抛出异常 |
| `pifen` | `switch` | 模式匹配/分支 |
| `约束` | `where` | 泛型约束 |
| `原址` | `ref` | 引用传递参数 |
| `out` | `out` | 输出参数 |
| `is` | `is` | 类型检查 |
| `typeof` | `typeof` | 类型查询 |
| `默认` | `default` | 默认值表达式 |
| `new` | `new` | 对象构造 |

---

## 三、核心语法规则（用户视角）

### 3.1 变量声明（类型后置）

```jiancs
shu 年龄: int = 18;           // 显式类型
shu 名字 = "张三";             // 类型推导（var）
shu 列表 = new List[string](); // 泛型 + 推导
```

### 3.2 方法定义（无箭头返回）

```jiancs
// 有返回值
gn 相加(a: int, b: int) int {
    fanhui a + b;
}

// 无返回值（void）
gn 打印(消息: string) {
    Console.WriteLine(消息);
}

// 异步方法
后台 gn 获取数据(链接: string) Task[string] {
    shu 响应 = 等 HttpClient.GetStringAsync(链接);
    fanhui 响应;
}
```

### 3.3 类与构造方法

```jiancs
kaif sjgnbao 用户 {
    kaif 姓名: string { get; set; }
    kaif 年龄: int { get; siyou set; }

    kaif 用户(姓名: string, 年龄: int) {
        ben.姓名 = 姓名;
        ben.年龄 = 年龄;
    }

    kaif 获取描述() string {
        fanhui $"姓名: {ben.姓名}";
    }
}
```

### 3.4 继承与接口实现

```jiancs
kaif sjgnbao 管理员 : 用户, IAuthenticate {
    kaif fugai 获取描述() string {
        fanhui $"管理员: {base.获取描述()}";
    }

    kaif 功能盒 通知处理(消息: string);
    kaif event 通知事件: 通知处理;
}
```

### 3.5 泛型（使用 `[]`）

```jiancs
// 泛型类
kaif sjgnbao 仓库[T] {
    kaif 数据: T { get; set; }
}

// 泛型方法
gn 转换[TInput, TResult](输入: TInput) TResult {
    fanhui (TResult)(object)输入;
}

// 使用
shu 仓库 = new 仓库[int]();
shu 结果 = 转换[string, int]("123");
```

### 3.6 索引访问（使用 `【】`）

```jiancs
shu 数组 = new int[5];
shu 第一个 = 数组【0】;

shu 字典 = new Dictionary[string, int]();
shu 值 = 字典【"键"】;

// 索引器定义
kaif ben【索引: int】: string {
    get { fanhui 数据【索引】; }
    set { 数据【索引】 = value; }
}
```

### 3.7 属性（Property）

```jiancs
// 自动属性
kaif 全名: string { get; set; }

// 只读属性
kaif 创建时间: DateTime { get; siyou set; }

// 完整属性
kaif 名字: string {
    get { fanhui ben.字段; }
    set { ben.字段 = value; }
}
```

### 3.8 委托与事件

```jiancs
// 委托定义
kaif 功能盒 日志回调(消息: string);
kaif 功能盒 计算器(a: int, b: int) int;

// 使用委托
kaif sjgnbao 演示 {
    kaif 执行() {
        shu 加法: 计算器 = (a, b) => a + b;
        shu 结果 = 加法(3, 5);
    }
}

// 事件
kaif sjgnbao 按钮 {
    kaif 功能盒 点击处理(发送者: object, 参数: EventArgs);
    kaif event 点击事件: 点击处理;

    kaif 触发点击() {
        点击事件?.Invoke(ben, new EventArgs());
    }
}
```

### 3.9 异常处理

```jiancs
尝试 {
    shu 值: int = int.Parse(文本);
} 捕获 (FormatException ex) {
    Console.WriteLine($"格式错误: {ex.Message}");
} 捕获 (Exception) {
    Console.WriteLine("未知错误");
} 最终 {
    Console.WriteLine("清理资源");
}
```

### 3.10 模式匹配（pifen）

```jiancs
gn 描述(值: object) string {
    fanhui pifen(值) {
        s: string when s.Length == 0 => "空字符串",
        s: string => $"字符串: {s}",
        i: int when i > 0 => "正整数",
        i: int => "非正整数",
        _ => "未知类型"
    };
}
```

### 3.11 LINQ 表达式

```jiancs
shu 结果 = 列表
    .Where(x => x.年龄 > 18)
    .Select(x => x.姓名)
    .ToList();
```

### 3.12 特性（Attribute）

```jiancs
[Serializable]
kaif sjgnbao 数据传输对象 {
    [DisplayName("ID")]
    kaif 主键: int { get; set; }
}
```

---

## 四、泛型与索引的括号分工

| 语法场景 | JianCS | C# | 说明 |
| :--- | :--- | :--- | :--- |
| 泛型类型/方法 | `List[string]` | `List<string>` | `[]` 内含**类型** |
| 数组索引 | `数组【0】` | `数组[0]` | `【】` 内含**值** |
| 字典键访问 | `字典【"键"】` | `字典["键"]` | `【】` 内含**值** |
| 索引器定义 | `ben【索引: int】` | `this[int 索引]` | 索引器语法 |
| 比较运算 | `a < b` | `a < b` | 原样透传 |

---

## 五、与 C# 的主要区别速查表

| 项目 | C# | JianCS |
| :--- | :--- | :--- |
| 变量声明 | `var x = 1` | `shu x = 1` |
| 显式类型 | `int x = 1` | `shu x: int = 1` |
| 方法定义 | `void Foo()` | `gn Foo()` |
| 有返回值方法 | `int Foo()` | `gn Foo() int` |
| 类定义 | `class` | `sjgnbao` |
| 结构体 | `struct` | `shujubao` |
| 接口 | `interface` | `gnlantu` |
| 枚举 | `enum` | `xuanxiangdan` |
| 命名空间 | `namespace` | `mok` |
| using | `using` | `引用` |
| public | `public` | `kaif` |
| private | `private` | `siyou` |
| protected | `protected` | `baohu` |
| internal | `internal` | `neibu` |
| static | `static` | `quanju` |
| virtual | `virtual` | `xu` |
| override | `override` | `fugai` |
| sealed | `sealed` | `mifeng` |
| abstract | `abstract` | `abstract` |
| delegate | `delegate` | `功能盒` |
| this | `this` | `ben` |
| base | `base` | `base` |
| return | `return` | `fanhui` |
| async/await | `async`/`await` | `后台`/`等` |
| for/while/foreach | `for`/`while`/`foreach` | `zhuge`/`zhiyao`/`遍历` |
| try/catch/finally | `try`/`catch`/`finally` | `尝试`/`捕获`/`最终` |
| switch | `switch` | `pifen` |
| 泛型 | `List<T>` | `List[T]` |
| 索引 | `arr[i]` | `arr【i】` |

**除此之外，C# 的所有特性（LINQ、异步、反射、特性、元组等）全部保留。**

---

## 六、完整示例

```jiancs
引用 System;
引用 System.Collections.Generic;
引用 System.Linq;

mok MyApp {

    kaif sjgnbao 订单项 {
        kaif 产品名: string { get; set; }
        kaif 单价: double { get; set; }
        kaif 数量: int { get; set; }

        kaif 小计() double {
            fanhui 单价 * 数量;
        }
    }

    kaif sjgnbao 订单 {
        kaif 项目列表: List[订单项] { get; } = new List[订单项]();

        kaif 添加项目(产品: string, 价格: double, 数量: int) {
            项目列表.Add(new 订单项 {
                产品名 = 产品,
                单价 = 价格,
                数量 = 数量
            });
        }

        kaif 总金额() double {
            shu 总和: double = 0;
            遍历 (shu 项目 in 项目列表) {
                总和 += 项目.小计();
            }
            fanhui 总和;
        }

        kaif ben【索引: int】: string {
            get { fanhui 项目列表【索引】.产品名; }
            set { 项目列表【索引】.产品名 = value; }
        }
    }

    kaif sjgnbao 程序 {
        kaif quanju 入口() {
            shu 订单 = new 订单();
            订单.添加项目("苹果", 3.5, 2);
            订单.添加项目("香蕉", 2.0, 3);

            Console.WriteLine($"总金额: {订单.总金额()}");
            Console.WriteLine($"第一个商品: {订单【0】}");
        }
    }
}
```

---

## 七、工具链

| 工具 | 说明 |
| :--- | :--- |
| **编译器** | `jiancs` 将 `.jiancs` 文件编译为标准 C# |
| **转换器** | `cs2jian` 将 C# 代码转换为 JianCS（双向） |
| **VSCode 插件** | 语法高亮 + 自动补全 |
| **dotnet 集成** | `dotnet jiancs` 直接运行 `.jiancs` 文件 |

---

## 八、许可证

**JianCS 语法规范**采用 **Jian 社区许可协议（JCL）**：

- ✅ 个人学习、开源非商业项目：**免费使用**
- ✅ 商业内部使用（员工 ≤ 50 人）：**免费使用**
- ⚠️ 商业发行版语言或云平台服务：**须购买商业授权**
- ❌ 禁止将本规范用于闭源商业竞品开发

详细协议条款请参阅 [LICENSE](./LICENSE) 文件。

---

## 九、获取帮助

- 📖 [完整教程](https://blog.csdn.net/2501_92449685)
- 💻 [在线 Playground](https://jiancs.dev/playground)
- 💬 [GitHub Discussions](https://github.com/jianyuyan/jianCs/discussions)
- 🐛 [Issue 反馈](https://blog.csdn.net/2501_92449685)

---

**Happy Coding! 🚀**

---
 