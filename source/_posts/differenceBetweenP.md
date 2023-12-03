---
title: Ruby | Puts,Print & P 之間的差異
date: 2023-11-21 22:00:46
categories:
- Ruby
tags:
- Ruby
- puts
---

在學習的期間看到了使用```puts```、```print```還有```p```來列印出文字訊息或是查看物件的值，但是對於什麼時候該用```print```，什麼時後用```puts```和```p```實在是有點模糊，所以寫一篇文章來區分這三者的差別。

## Print vs Puts
### 印值
首先是```print```，按字面意思來看就是列印。
那效果呢？
```ruby=
print "123"
print "456"
print "789"
```
![Alt text](<../uploads/ruby1120/2023-11-21 下午10.15.32.png>)

可以發現全部印在同一行了，那來試試```puts```印出來會有什麼不同：
```ruby
puts "123"
puts "456"
puts "789"
```

![Alt text](<../uploads/20231121/截圖 2023-11-21 下午10.30.19.png>)
可以看到和```print```的列印結果不同，是因為```puts``` **會在最後加上換行的效果**。

除了基本換行差異外，對列印陣列時兩個印出的內容也有不同：
```ruby
puts ["A","B"]
# 結果：
A
B

print ["a","b"]
# 結果：
["a","b"]
```
- ```puts```會將<font style="color:red;">陣列內容</font>一個一個使用```.to_s```並加上換行後印出。
- ```print```將陣列使用```.to_s```印出。

那如果試著列印含有```nil```的陣列會怎樣呢？
```ruby
puts ["A",nil,"B"]

# 結果：
A

B

print ["a",nil]

# 結果：
["a", nil]
```

上述結果可以看出```puts```印```nil```會印出空字串(Empty String)，```print```將整個陣列以字串印出。


那```print``` 單獨印```nil```呢？

```ruby
print "c"
print nil
print "d"

# 結果：
cd
```

顯然```print``` 印 ```nil```也是一樣會印出空字串(Empty String)。

以上面的結果做個總結：

- **print & puts**
  - 嘗試將所有內容轉換為字串（```to_s```），印```nil```會印出空白內容。
- **print** 
  - 不會換行
- **puts**
  - 會換行
  - 列印陣列時會將內容值依序換行印出。

### 返回值
```ruby
print 123 
# nil
puts 123 
#nil

```

![Alt text](<../uploads/20231121/截圖 2023-11-22 上午12.22.50.png>)

- ```print``` 和 ```puts``` 的返回值都是 ```nil```

## Puts vs P
### 印值
> p is a method that shows a more “raw” version of an object.
> p 是一種顯示物件更「原始」版本的方法。

原始版本是什麼呢？
試著使用```p```來印一些東西看看：
```ruby
p 123
p "123"
p [123, "456", nil]
p nil

# 結果：
123
"123"
[123, "456", nil]
nil
```
從上面印出的內容可以明確地一眼看出印出的是數字、字串還是```nil```。

開發的時候使用```p```印出明確的內容就不用再去追蹤是字串還是數字，可以加速我們除錯的速度及準確度。

- ```p```和```puts```都會在印出內容後面加上換行符號。
- ```p```會印出型態樣式。

### 返回值
```ruby=
print 123 # nil
puts 123 # nil
p 123 # 123
```
![Alt text](<../uploads/20231121/截圖 2023-11-22 上午12.21.45.png>)

- ```print```返回```nil```。
- ```puts```返回```nil```。
- ```p```會將值返回。

## 差異表

| | Print | Puts | P |
|---|:-:|:-:|:-:|
| 自帶換行 | 不會 | 會 | 會 |
| 印出原形 | 不會 | 不會 | 會 |
| 印nil或換行符號 |	Empty String | Empty String | nil 、\n |
| 返回值 | nil | nil | 印出的目標值 |



---
> 參考來源
> [1] 五倍紅寶石學院 ASTRO Camp課程
> [2] Understanding The Differences Between Puts, Print & P by Jesus Castello
>     https://www.rubyguides.com/2018/10/puts-vs-print/
