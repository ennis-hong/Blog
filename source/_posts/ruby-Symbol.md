---
title: Ruby | Symbol
date: 2023-11-19 21:32:50
categories:
  - Ruby
tags:
  - Ruby
  - Symbol
---

在 Ruby 中有許多的型態

- Integer
- Float
- String
- Array
- Hash
- Symbol
- Boolean
- Regular Expression
- Class
- Module
- Range

今天要來說一下 Symbol，這個對我來說非常陌生的型態。
那「Symbol」是什麼呢? 它翻譯叫符號...

在 Ruby 中的 Symbol 長這樣:

```ruby
:name
#冒號加上自定義名
```

## Symbol 的特性是

**<font color=#FF0000>1. 唯一性</font>**

**<font color=#FF0000>2. 不可變</font>**

一旦創建了之後就不能改變它的值且記憶體位置不變。

```ruby
:name
name = :name
p :name.object_id # 72028
p name.object_id # 72028
```

當我們試著想改變它

```ruby
 :name = 123
 # 出現錯誤 syntax error, unexpected '=', expecting end-of-input
```

符號不能被改變，但是字串可以

```ruby
tempStr = "test"
p tempStr.object_id # 179600

# 修改文字內容
tempStr.insert(1, 'bar')
p tempStr # tbarst
p tempStr.object_id # 179600
```

由上述程式碼結果可知文字即使被修改了，記憶體位置仍相同。

```ruby
p "hello".object_id #285160
p "hello".object_id #288980
p "hello".object_id #292800
```

字串可以被創建很多次，但是每次創建都會指向新的記憶體位置。

## 適用情境

那既不能修改也沒有具體的值那什麼時候可以用呢?
以訂單狀態來舉例好了，假設訂單有狀態為待處理(pending)、完成(complete)。

1. 使用字串

```ruby
class Order
    attr_reader :status

    def initialize(items, status = "pending")
      @items = items
      @status = status
    end

    def compete
      @status = "complete"
    end
  end

  order = Order.new(["item A", "item B", "item C"])

  if order.status == "pending"
    puts "order is pending"
  end

  order.compete

  if order.status == "complete"
    puts "order is complete"
  end
```

2. 使用 Symbol

```ruby
class Order
    attr_reader :status

    def initialize(items, status = :pending)
      @items = items
      @status = status
    end

    def compete
      @status = :complete
    end
  end

  order = Order.new(["item A", "item B", "item C"])

  if order.status == :pending
    puts "order is pending"
  end

  order.compete

  if order.status == :complete
    puts "order is complete"
  end
```

上面兩個在結果上來看是差不多的，但是如果今天有很多個訂單實例，那每一個訂單的狀態都指向一個新的字串就可能會造成記憶體的浪費。

如果是使用 Symbol，即使訂單數量多了，狀態指向的 Symbol 都是同一個位置這樣就不會造成記憶體浪費了。

雖然說 Symbol 可以降低記憶體空間的浪費，<font color=#FF0000>But!</font>不是所有的字串都改成用 Symbol 唷!

## 回收機制(Garbage Collection)

字串等其他型態會在程式運行期間就可能會被回收，

**Symbol 從程式開始執行就會生成一直存在直到程式結束運行!**
