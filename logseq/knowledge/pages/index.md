- ## 创建全文索引
- 给 sku 表的 title 字段添加全文索引
-
- ```
  create fulltext index text_title
    on t_sku (title);
  ```
- ```
  - ```
  - ```
  Copied!
  ```
- 查询
-
- ```
  select id, title, images, price
  from t_sku
  where match(title) against('小米9');
  ```
- ```
- ```
- ```
- ```
-
- ## 建 Lucene 索引
- ![image-20200614111515949.8347e769.png](../assets/image-20200614111515949.8347e769_1694340702426_0.png)