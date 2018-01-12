- remove duplicates in a query response
orm: posts = Post.all.unique
sql: select distinct * from posts;
- filter records using inequalities, pattern matching, ranges, and boolean logic
orm: posts = Post.all.in_last_month
sql: select * from post where date > current_date - 30;
- sort records in a particular order
orm: users = User.all.sort_by_last_name
sql: select * from users order by last_name desc;

- limit the number of records returned
orm: posts = Post.last_ten
sql: select * from posts limit 10;
- group records into sections
orm: posts = Post.all.group_by_user
sql: select * from posts group by user_id;
- perform calculations using aggregate functions
orm: usercount = User.all.count
sql: select count(id) from users;
- join tables using cross join, inner join, and outer join
orm: Order.join(:customers)
sql: select o.orderid, c.name from orders o inner join customers c on o.customerid = c.customerid;
