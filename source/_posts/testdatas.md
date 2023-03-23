---
title: 创建1000w测试数据
date: 2023-02-21 17:25:38
tags: 测试
categories: 技术
---
假如需要创建1000w 测试数据的话,可以尝试使用存储过程.

```
CREATE TABLE `data` 
(
  `id`         bigint(20) NOT NULL      AUTO_INCREMENT,
  `datetime`   timestamp  NULL          DEFAULT CURRENT_TIMESTAMP,
  `channel`    int(11)                  DEFAULT NULL,
  `value`      float                    DEFAULT NULL,

  PRIMARY KEY (`id`)
);


CREATE PROCEDURE generate_data(IN n int)
BEGIN
  DECLARE i INT DEFAULT 0;
  WHILE i < n DO
    INSERT INTO `data` (`datetime`,`value`,`channel`) VALUES (
      FROM_UNIXTIME(UNIX_TIMESTAMP('2014-01-01 01:00:00')+FLOOR(RAND()*31536000)),
      ROUND(RAND()*100,2),
      1
    );
    SET i = i + 1;
  END WHILE;

  CALL generate_data(10000);
 
```

删除存储过程执行如下:
```
DROP PROCEDURE generate_data;
```


