# golang


##### 1.golang range map 获取的是值的备份，都是同一个指针
![1_range_map.png ](https://jk-97.github.io/my_note/golang/sources/images/1_range_map.png)
**result:**
![1_range_map_res.png ](https://jk-97.github.io/my_note/golang/sources/images/1_range_map_res.png)
**solve**
需要在range体内声明一个变量来存储value，再将指针赋予map