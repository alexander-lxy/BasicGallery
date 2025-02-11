##  Java 8 Stream 流操作

**接口有且只有一个抽象方法**：

- 如果接口有 **多个抽象方法**，则不能使用 Lambda 表达式。
- 如果接口只有 **一个抽象方法**，那么它就是一个函数式接口，可以使用 Lambda 表达式。

**接口的目标类型与 Lambda 匹配**：

- Lambda 表达式的形态 `(参数列表) -> 表达式` 必须符合接口中抽象方法的签名（参数类型和返回类型必须匹配）。
- 如果接口的方法参数类型或返回类型不匹配 Lambda 表达式的结构，那么 Lambda 表达式不能应用。







#### **1. `filter(Predicate<T>)`：过滤元素**
```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David");
List<String> filtered = names.stream()
    .filter(name -> name.length() > 3)  // 保留长度大于3的字符串
    .collect(Collectors.toList());     // 结果: ["Alice", "Charlie", "David"]
```

#### **2. `map(Function<T, R>)`：元素转换**
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4);
List<Integer> squares = numbers.stream()
    .map(n -> n * n)                   // 计算平方
    .collect(Collectors.toList());     // 结果: [1, 4, 9, 16]
```

#### **3. `flatMap(Function<T, Stream<R>>)`：扁平化流**
```java
List<List<Integer>> matrix = Arrays.asList(
    Arrays.asList(1, 2),
    Arrays.asList(3, 4)
);
List<Integer> flatList = matrix.stream()
    .flatMap(List::stream)            // 将嵌套集合展开为单一流
    .collect(Collectors.toList());    // 结果: [1, 2, 3, 4]
```

#### **4. `sorted()` / `sorted(Comparator<T>)`：排序**
```java
List<String> languages = Arrays.asList("Java", "Python", "C++");
List<String> sorted = languages.stream()
    .sorted()                         // 自然排序（字典序）
    .collect(Collectors.toList());    // 结果: ["C++", "Java", "Python"]

List<Integer> nums = Arrays.asList(5, 3, 9, 1);
List<Integer> reverseSorted = nums.stream()
    .sorted(Comparator.reverseOrder()) // 逆序排序
    .collect(Collectors.toList());     // 结果: [9, 5, 3, 1]
```

#### **5. `distinct()`：去重**
```java
List<Integer> duplicates = Arrays.asList(2, 3, 2, 5, 3);
List<Integer> unique = duplicates.stream()
    .distinct()                       // 去重
    .collect(Collectors.toList());    // 结果: [2, 3, 5]
```

#### **6. `limit(long)`：限制元素数量**
```java
List<Integer> nums = Arrays.asList(1, 2, 3, 4, 5);
List<Integer> firstThree = nums.stream()
    .limit(3)                        // 取前3个元素
    .collect(Collectors.toList());   // 结果: [1, 2, 3]
```

#### **7. `skip(long)`：跳过元素**
```java
List<Integer> nums = Arrays.asList(1, 2, 3, 4, 5);
List<Integer> skipped = nums.stream()
    .skip(2)                         // 跳过前2个元素
    .collect(Collectors.toList());   // 结果: [3, 4, 5]
```

---

### **二、终端操作（Terminal Operations）**

#### **1. `forEach(Consumer<T>)`：遍历元素**
```java
List<String> words = Arrays.asList("Hello", "Stream");
words.stream()
    .forEach(word -> System.out.print(word + " "));  // 输出: Hello Stream
```

#### **2. `collect(Collector<T>)`：收集结果**
```java
List<String> list = Arrays.asList("a", "b", "c");
Set<String> set = list.stream()
    .collect(Collectors.toSet());    // 转为 Set: {"a", "b", "c"}

Map<String, Integer> map = list.stream()
    .collect(Collectors.toMap(
        s -> s,                     // Key 生成规则
        s -> s.length()             // Value 生成规则
    ));                             // 结果: {"a":1, "b":1, "c":1}
```

#### **3. `reduce(BinaryOperator<T>)`：聚合操作**
```java
List<Integer> nums = Arrays.asList(1, 2, 3, 4);
Optional<Integer> sum = nums.stream()
    .reduce((a, b) -> a + b);       // 求和
System.out.println(sum.get());      // 输出: 10

// 带初始值的 reduce
int product = nums.stream()
    .reduce(1, (a, b) -> a * b);    // 计算乘积（初始值 1）
System.out.println(product);        // 输出: 24
```

#### **4. `count()`：统计元素数量**
```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
long count = names.stream()
    .filter(name -> name.length() > 3)
    .count();                       // 结果: 2
```

#### **5. `anyMatch(Predicate<T>)`：是否存在匹配元素**
```java
List<Integer> nums = Arrays.asList(2, 4, 6, 8);
boolean hasEven = nums.stream()
    .anyMatch(n -> n % 2 == 0);     // 是否包含偶数（始终为 true）
```

#### **6. `allMatch(Predicate<T>)`：是否全部匹配**
```java
List<Integer> nums = Arrays.asList(2, 4, 6, 8);
boolean allEven = nums.stream()
    .allMatch(n -> n % 2 == 0);     // 是否全部为偶数（true）
```

#### **7. `noneMatch(Predicate<T>)`：是否无匹配**
```java
List<Integer> nums = Arrays.asList(1, 3, 5, 7);
boolean noEven = nums.stream()
    .noneMatch(n -> n % 2 == 0);    // 是否没有偶数（true）
```

#### **8. `findFirst()` / `findAny()`：查找元素**
```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
Optional<String> first = names.stream()
    .findFirst();                   // 结果: Optional["Alice"]

// 并行流中 findAny 可能更快
Optional<String> any = names.parallelStream()
    .findAny();                     // 可能返回任意元素
```

---

### **三、原始类型流（避免装箱开销）**

#### **1. `IntStream` / `LongStream` / `DoubleStream`**
```java
int[] numbers = {1, 2, 3, 4, 5};
IntStream intStream = Arrays.stream(numbers);

// 直接计算平均值
OptionalDouble avg = intStream.average();
System.out.println(avg.getAsDouble());  // 输出: 3.0
```

#### **2. 转换操作**
```java
List<String> strings = Arrays.asList("1", "2", "3");
int sum = strings.stream()
    .mapToInt(Integer::parseInt)     // 转为 IntStream
    .sum();                          // 结果: 6
```

---

### **四、并行流（Parallel Stream）**

```java
List<Integer> nums = Arrays.asList(1, 2, 3, 4, 5);

// 并行计算平方和
int sumOfSquares = nums.parallelStream()
    .map(n -> n * n)
    .reduce(0, Integer::sum);        // 结果: 55

// 注意：非线程安全操作需同步
List<Integer> unsafeList = new ArrayList<>();
nums.parallelStream()
    .forEach(unsafeList::add);       // ❌ 可能引发并发问题
```

---

### **五、操作符速查表**

| **操作类型**   | **操作符**  | **示例**                             | **输出示例**          |
| -------------- | ----------- | ------------------------------------ | --------------------- |
| **过滤**       | `filter`    | `.filter(n -> n > 5)`                | 保留大于5的元素       |
| **转换**       | `map`       | `.map(String::toUpperCase)`          | 转为大写              |
| **扁平化**     | `flatMap`   | `.flatMap(list -> list.stream())`    | 展开嵌套集合          |
| **排序**       | `sorted`    | `.sorted(Comparator.reverseOrder())` | 逆序排序              |
| **去重**       | `distinct`  | `.distinct()`                        | 移除重复元素          |
| **限制数量**   | `limit`     | `.limit(3)`                          | 取前3个元素           |
| **跳过元素**   | `skip`      | `.skip(2)`                           | 跳过前2个元素         |
| **遍历**       | `forEach`   | `.forEach(System.out::println)`      | 打印每个元素          |
| **收集结果**   | `collect`   | `.collect(Collectors.toList())`      | 转为 List             |
| **聚合计算**   | `reduce`    | `.reduce(0, Integer::sum)`           | 求和（初始值0）       |
| **统计数量**   | `count`     | `.count()`                           | 元素总数              |
| **匹配存在性** | `anyMatch`  | `.anyMatch(s -> s.contains("a"))`    | 是否存在包含"a"的元素 |
| **查找元素**   | `findFirst` | `.findFirst()`                       | 返回第一个元素        |

**注意**

- **流的一次性**：流只能被消费一次，重复使用会抛出 `IllegalStateException`。
- **并行流风险**：避免在并行流中修改共享可变状态（如非线程安全集合）。
- **原始类型优先**：处理数值时优先使用 `IntStream`/`LongStream` 减少装箱开销。、
