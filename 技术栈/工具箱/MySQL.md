# 数据库管理命令
1. **显示所有数据库**：
   ```sql
   SHOW DATABASES;
   ```

2. **创建新数据库**：
   ```sql
   CREATE DATABASE database_name;
   ```

3. **删除数据库**：
   ```sql
   DROP DATABASE database_name;
   ```

4. **选择数据库**：
   ```sql
   USE database_name;
   ```

# 表管理命令
1. **显示所有表**：
   ```sql
   SHOW TABLES;
   ```

2. **创建新表**：
   ```sql
   CREATE TABLE table_name (
       column1_name data_type constraints,
       column2_name data_type constraints,
       ...
   );
   ```

3. **删除表**：
   ```sql
   DROP TABLE table_name;
   ```

4. **修改表结构**（添加列）：
   ```sql
   ALTER TABLE table_name ADD column_name data_type;
   ```

5. **修改表结构**（删除列）：
   ```sql
   ALTER TABLE table_name DROP COLUMN column_name;
   ```

6. **查看表结构**：
   ```sql
   DESCRIBE table_name;
   ```

# 数据操作命令
1. **插入数据**：
   ```sql
   INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...);
   ```

2. **查询数据**：
   ```sql
   SELECT column1, column2 FROM table_name WHERE condition;
   ```

3. **更新数据**：
   ```sql
   UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
   ```

4. **删除数据**：
   ```sql
   DELETE FROM table_name WHERE condition;
   ```

# 其他常用命令
1. **显示当前数据库**：
   ```sql
   SELECT DATABASE();
   ```

2. **显示当前用户**：
   ```sql
   SELECT USER();
   ```

3. **查看表中的数据行数**：
   ```sql
   SELECT COUNT(*) FROM table_name;
   ```

4. **使用 LIKE 进行模糊查询**：
   ```sql
   SELECT * FROM table_name WHERE column_name LIKE 'pattern';
   ```

5. **排序结果**：
   ```sql
   SELECT * FROM table_name ORDER BY column_name ASC|DESC;
   ```

6. **分组查询**：
   ```sql
   SELECT column_name, COUNT(*) FROM table_name GROUP BY column_name;
   ```