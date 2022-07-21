I)
- Create: tạo bảng <br>
	 <br>
    ```sql
        CREATE TABLE celebs (
		   id INTEGER, 
		   name TEXT, 
		   age INTEGER
		);
		-- tạo bảng có tên celebs có 3 cột(trường) là id kiểu dữ liệu là integer...
	```	
- Insert: thêm dữ liệu trong bảng có sẵn

	```sql 
        INSERT INTO celebs (id, name, age) 
		VALUES (1, 'Justin Bieber', 22);
		-- thêm dữ liệu vào bảng có tên celebs vào các trường có tên có các dữ liệu tương ứng theo thứ tự
	```
- Select: câu lênh dấy dữ liệu từ trong bảng của database
	```sql 
        Select * from celebs;
		-- lấy *(tất cả cột) có thể thay bằng tên cột muốn lấy dữ liệu từ bảng celebs
    ```
- Alter: câu lệnh thêm một cột mới vào bảng
	```sql 
        ALTER TABLE celebs 
		ADD COLUMN twitter_handle TEXT;
		-- ALTER TABLE là mệnh đề cho phép thay đổi celebs là tên bảng ,ADD COLUMN là mệnh đề thêm cột mới vào bảng ,twitter_handle là tên cột, TEXT là kiểu dữ liệu của cột đó
    ```
- Update: cập nhật dữ liệu ở 1 hàng
	```sql 
        UPDATE celebs 
		SET twitter_handle = '@taylorswift13' 
		WHERE id = 4; 
	    -- UPDATE là câu lệnh thay đổi dữ liệu ở hàng, SET là mệnh đề chỉ ra cột cần chỉnh sửa, WHERE là điều kiện để chỉnh sửa khi id = 4
	```
- DELETE: xoá 1 hoặc nhiều hàng ở table 
	```sql 
        DELETE FROM celebs 
		WHERE twitter_handle IS NULL;
		-- xoá hàng mà twitter_handle không có dữ liệu gì cả
	```
- CONSTRAINTS: bổ sung thông tin về cách một cột có thể được sử dụng được gọi sau khi chỉ định kiểu dữ liệu cho một cột. Chúng có thể được sử dụng để yêu cầu cơ sở dữ liệu từ chối dữ liệu được chèn vào mà không tuân theo một hạn chế nhất định. Câu lệnh dưới đây thiết lập các ràng buộc trên bảng celebs.
    ```sql
    CREATE TABLE celebs (
        id INTEGER PRIMARY KEY, 
        name TEXT UNIQUE,
        date_of_birth TEXT NOT NULL,
        date_of_death TEXT DEFAULT 'Not Applicable'
    );
    ```
	>  Các cột PRIMARY KEY 1 bảng chỉ có 1 cột có thể dùng để rằng buộc rằng nó là duy nhất nếu có dữ liệu nào bổ sung mà trùng thì sẽ không được

	> Cột có rằng buộc là UNIQUE tương tự như PRIMARY KEY nhưng có thể dùng cho nhiều cột trong cùng 1 TABLE chỉ có 1 giá trị khác nhau cho mỗi hàng.

	> Rằng buộc NOT NULL khi chèn 1 hàng mà không có giá trị thì sẽ không chèn được  vì nó chỉ chấp nhận khí có dữ liệu.

	> Rằng buộc DEFAULT khi chèn 1 hàng mà không có dữ liệu thì sẽ mặc định là dữ liêu mà được định nghĩa khi dùng DEFAULT

II) : QUERIES Khi dùng QUERIES thì các câu lệnh dài có thể xuống dòng để có thể dễ đọc hơn

- AS : khi dùng lệnh as thì sẽ đặt cho tên cột 1 bí danh không làm thay đổi tên cột nhưng kết quả hiện ra sẽ tiện theo dõi nếu muốn
    ```sql
    SELECT name AS 'Titles'
    FROM movies;
    -- kết quả sẽ hiện ra Titles thay vì name
	```
- DISTINCT: trong 1 cột sẽ có nhiều dữ liệu trùng nhau, câu lệnh này chỉ ra các kết quả khác nhau chỉ 1 lần để dễ dàng xem
	```sql 
        SELECT DISTINCT tools
		FROM inventory;
		-- khi chạy câu lệnh ko có DISTINCT thì sẽ có nhiều kết quả, nhưng dùng thì sẽ hiện những kết quả riêng biệt ko lặp lại 
	```	
- WHERE là câu điều kiện kiểm tra các giá trị logic khi đạt điều kiện nào đó	
	```sql 
        SELECT *
		FROM movies
		WHERE imdb_rating > 8;
		--chỉ ở bảng movies cột imdb_rating có giá trị lớn hơn 8
    ```
- LIKE 1: để so sánh giá trị tương tự dùng các kí tự wilcard
	```sql 
        SELECT *
		FROM movies
		WHERE name LIKE 'Se_en';
		--các phim có tên Seven, Se7en, .. tìm thấy, kí tự _ là có thể thay thế bất cứ kí tự nào vào chỗ trống này
    ```
- LIKE 2 : có thể thêm bất cứ kí tự 'Wildcard' các vào để tìm chuỗi tương ứng ( giống regex)
	```sql 
        SELECT * 
		FROM movies 
		WHERE name LIKE '%man%';
		-- kí tự '%' có thể thay thế bất cứ chuỗi kí tự nào hoẵc ko chứa kí tự nào
		-- kết quả có thể là man, 1man1, quyenman, manquyen, quyenmancaij, quyen man quyen, man gaga, quyen man gaga,...
    ```
- IS NULL: khi tạo bảng thì không gán giá trị thì nó sẽ mặc định là không có giá trị đó chính là NULL có thể kiếm tra bằng = hoặc != , hoặc có thể dùng
  2 loại toán tử
    > IS NULL
    
	> IS NOT NULL
	
	```sql 
        SELECT name
		FROM movies 
		WHERE imdb_rating IS NOT NULL;
		-- lấy cột name từ bảng movies cái imdb_rating của nó có giá trị cụ thể
    ```
- BETWEEN: là 1 toán tử thường dùng trong câu lệnh WHERE để lấy dữ liệu nằm trong 1 vùng nào đó có thể là số, kí tự hoặc ngày tháng
	```sql 
    SELECT *
		FROM movies
		WHERE year BETWEEN 1990 AND 1999;
		-- lấy tất cả dữ liệu của bảng movies nơi mà có năm sản xuất từ 1990 đến 1999
	```

	```sql 
    SELECT *
    FROM movies
    WHERE name BETWEEN 'A' AND 'J';
    --lấy tất cả dữ liệu bắt đầu từ A đến J nên khi tên phim là 'J' thì sẽ match còn thêm kí tự như là 'JACK' thì sẽ ko được match vì nó chỉ match từ A đến J thôi.
    ```
- AND: toán tử và ( tất cả thoả mãn điều kiện cho trước mới chọn)
	```sql 
    SELECT * 
    FROM movies
    WHERE year BETWEEN 1990 AND 1999
    AND genre = 'romance';
	-- Lấy tất cả dữ liệu trong bảng năm sản xuât trong thập niên 1990's và genre là romance đáp ứng đủ cả 3 điều kiện này.
    ```
- OR: toán tử hoặc ( thoả mãn 1 trong các điều kiện là đủ )
	```sql 
    SELECT *
    FROM movies
    WHERE year > 2014
    OR genre = 'action';
    -- chọn phim có năm sản xuất từ 2015 hoặc thể loại là hành động
    ```
- ORDER BY: khi tìm được dữ liệu thì ta cần phải sắp xếp lại dữ liệu để dễ đọc, đây là công dụng của câu lệnh ORDER BY( mặc định sắp xếp tăng dần theo bảng chữ cái)
	```sql 
    SELECT *
    FROM movies
    WHERE imdb_rating > 8
    ORDER BY year DESC;
	/*
	1. DESC giảm dần nếu sắp xếp
	2. ASC tăng dần
	3. nếu có WHERE thì ORDER BY thường đứng sau WHERE
	*/
    ```
- LIMIT: thông thường thì các database sẽ có rất nhiều dòng(bản ghi) khi đó nếu dùng select thì sẽ hiển thị ra rất nhiều khiến cho máy tính chậm nên cần dùng câu lệnh LIMIT để giới hạn số bản ghi được in ra màn hình
	```sql 
    SELECT *
    FROM movies
    LIMIT 10;
    -- chỉ xem 10 dòng đầu 
    ```
- CASE: Giúp chúng ta hiển thị kết quả tuỳ chỉnh có thể bằng 1 cột riêng biệt( giống câu lệnh điều kiện if-then)
	```sql 
    SELECT name,
        CASE
        WHEN imdb_rating > 8 THEN 'Fantastic'
        WHEN imdb_rating > 6 THEN 'Poorly Received'
        ELSE 'Avoid at All Costs'
        END AS 'Review'
    FROM movies;

    --Cột này thể hiện kết quả khi imdb_rating > 8 thì kq là Fantasic , imdb_rating > 6 thì kq là Poorly Received, còn lại là Avoid at All Cost cột này thường có tên rất dài nên sau END ta phải để tên nó thành 1 tên ngắn gọn.
    ```
III) Các lênh tính toán dùng Sql( aggregate)

- COUNT: tính đếm các các hàng(bao nhiêu bản ghi) hoặc tổng,...
    >VD1
	```sql 
    SELECT COUNT(*)
    FROM fake_apps;
    ```
    >VD2
	```sql 
    --đếm số free-app
    SELECT COUNT(*)
    FROM fake_apps
    WHERE price = 0.0;
    ```
- SUM: tổng giá trị
	```sql 
    SELECT SUM(downloads)
    FROM fake_apps;
    -- khác với đếm thì tính tổng ta phải chỉ ra tên trường cụ thể cần tính
    ```
- MAX/ MIN: tính giá trị lớn nhất/ nhỏ nhất của 1 trường cụ thể
	```sql
    SELECT MIN(downloads)
    from fake_apps;
    -- max thì tương tự
	```	
- AVG: viết tắt của average(trung bình) tính giá trị trung bình của 1 trường cụ thể
	```sql
    SELECT AVG(downloads)
    FROM fake_apps;
    -- tính giá trị trung bình của trường có tên là downloads
    ```
- ROUND: thông thường sql sẽ hiển thị số chính xác nhất có thể. Để có thể làm tròn thì ta dùng hàm này.
	- hàm này nhận 2 đối số truyền vào
        >1. Đối số thứ nhất là tên cột(trường)

        >2. Đối số thứ hai là 1 số nguyên( nó sẽ làm tròn bằng cách thêm số số 0 sau dấu phẩy)
	
	```sql
    SELECT ROUND(price, 0)
    FROM fake_apps;
    ```
	>VD2: 
    ```sql
    SELECT ROUND(AVG(price), 2)
		FROM fake_apps;
		-- hoặc có thể dùng để làm tròn giá trị được lấy trung bình bằng hàm AVG hoặc các hàm tính toán MIN/MAX, SUM, ...
	```
- GROUP BY: khi chúng ta muốn tính toán cho 1 vài đặc điểm nhất định. thường đứng sau WHERE và thường đứng trước ORDER BY và LIMIT.
    ```sql
    SELECT AVG(imdb_rating)
    from movies
    Where year = 1999;
    --Ta muốn tính AVG(imdb_rating) của các phim theo từng năm nếu ko dùng GROUP BY thì sẽ viết rất cồng kềnh 

    SELECT AVG(imdb_rating)
    from movies
    Where year = 2000;
    
    SELECT AVG(imdb_rating)
    from movies
    Where year = 2001;
	```

		
	```sql
    --Còn dùng  GROUP BY
    SELECT year,
    AVG(imdb_rating)
    from movies
    GROUP BY year
    ORDER BY year;
    ```

    ```sql
    -- hoặc có thể dùng để kết hơp với các hàm tính toán khác
    
    SELECT price, count(*)
    from fake_apps
    group by price;
    -- mỗi giá khác nhau có bao nhiêu loại
    ```

    ```sql
    select price, count(*)
    from fake_apps;
    where downloads > 20000
    group by price;
    -- đếm số app có lượt downloads lớn hơn 20000 theo từng giá khác nhau
	```
	```sql
     select category, sum(downloads)
    from fake_apps
    group by category;
    -- tính tổng số lượt downloads theo từng thể loại khác nhau
    ```
- GROUP BY: (tiếp theo) thỉnh thoảng thì chúng ta ko nhóm theo cột mà nhóm theo 1 phép tính thì các làm trên sẽ dài dòng vì thế nên có cách thứ 2 này
	```sql
     --đây là cách thứ 1
    select round(imdb_rating), count(name)
    from movies
    group by round(imdb_rating)
    order by round(imdb_rating)
    -- cách này dài dòng thì thường khiến khả năng mắc lỗi cao hơn
    
    -- đây là cách thứ 2
    select round(imdb_rating), count(name)
    from movies
    group by 1;
    order by 1;
    -- khi select đến các cột thì để đỡ phải viết dài dòng ta có thể tham chiếu đến các cột theo thứ tự như trong trường hợp này cột thứ 1 là round(imdb_rating)
    -- cột 2 là count(name) , nếu nhiều cột thì ta sẽ cứ như thế mà gán số thứ tự cho chúng 
    ```
- HAVING: khi chúng ta lọc thông tin bằng group by ví dụ chúng ta chỉ cần biết bao nhiêu phim khác nhau với tiêu chí như thể loại thế nào,... Nhưng bây giờ không thể dùng WHERE được vì ta muốn nhóm dữ liệu lại 
 và thống kê trên vài dòng để dễ đọc thì chúng ta sẽ dùng HAVING(  thường đứng sau GROUP BY , nhưng thường đứng trước ORDER BY  và LIMIT )
	```sql 
    SELECT year, genre,  count(name) 
    from movies
    group by 1, 2
    having count(name) > 10;
    -- khi chúng ta muốn giới hạn kết quả trên các hàng riêng lẻ thì ta dùng WHERE 
    -- khi chúng ta muốn giới hạn kết quả trên một thuộc tính tổng hợp thì ta dùng HAVE
    ```
IV) 
- MULTIPLE TABLE: Để lưu dữ liệu một cách hiệu quả chúng ta thường lưu trong nhiều bảng vì nếu 1 bảng lưu thông tin của 1 khách hàng:<br>
    - order_id<br>
    - customer_id<br>
    - customer_name<br>
    - customer_address<br>
    - subscription_id<br>
    - subscription_description<br>
    - subscription_monthly_price<br>
    - subscription_length<br>
    - purchase_date<br>
	Tuy nhiên 1 số lượng lớn dữ liệu sẽ lặp lại khi khác hàng mua hàng nhiều mà các thông tin như địa chỉ, tên sẽ lặp lại. Nếu 1 sản phẩm mà nhiều khách hàng khác nhau mua cũng gây ra sự lặp lại gây lãng phí rất lớn
	nên ta phải chia thành các bảng theo từng loại khác nhau<br>
    1. orders: bao gồm thông tin những sản phẩm đã được đăng kí<br>
        VD: order_id, customer_id, subscription_id, purchase_date<br>
    2. subscriptions: bao gồm thông tin đăng kí<br>
        VD: subscription_id, description, price_per_month, subscription_length<br>
    3. customers: bao gồm thông tin của khách hàng<br>
	VD: customer_id, customer_name, address
	```sql
	SELECT *
	FROM orders
	LIMIT 5;
	 
	SELECT *
	FROM subscriptions
	LIMIT 5;
	 
	SELECT * 
	FROM customers
	LIMIT 5;
	```
    >it wil show

    

   | order_id |customer_id	|subscription_id|	purchase_date|
    | ------------- | ------------- | -------- |-------- |
   | 1	|3	|2	|01-10-2017|
   | 2	|2	|4	|01-9-2017|
   | 3	|3	|4	|01-26-2017|
   | 4	|9	|9	|01-4-2017|
   | 5	|7	|5	|01-25-2017|

   |subscription_id	|description	|price_per_month	|subscription_length|
    | ------------- | ------------- | -------- |-------- |
    |1	|Politics Magazine	|10	|12 months|
    |2	|Politics Magazine	|11	|6 months|
    |3	|Politics Magazine	|12	|3 months|
    |4	|Fashion Magazine	|15	|12 months|
    |5	|Fashion Magazine	|17	|6 months|

    |customer_id	|customer_name	|address|
    | ------------- | -------- |-------- |
    |1	|Allie Rahaim	|123 Broadway|
    |2	|Jacquline Diddle	|456 Park Ave.|
    |3	|Lizabeth Letsche	|789 Main St.|
   |4	|Jessia Butman	|1 Columbus Ave.|
    |5	|Inocencia Goyco	|12 Amsterdam Ave.|