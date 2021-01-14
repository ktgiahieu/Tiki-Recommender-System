# Tiki-Recommender-System

| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |

_Author: Hieu Khuong_

-------
### Table of Contents
[Web Scraping Notebook](TikiScraper.ipynb)  
[Data Cleaning Notebook](TikiDataCleaning.ipynb)  
[Feature Engineering & Recommender Model](TikiRecommender.ipynb)

## Executive Summary

**Problem Statement**

The world of retail is changing at a rapid pace.  Many brick and mortar locations are closing and being replaced by online stores.  However, while the breadth of assortment that comes with shopping online is something that drives customers to a website, a lot of eCommerce platforms fail to sell through a high percent of their merchandise.  This is often due to a poor user browsing experience. Customers can spend hours scrolling through hundreds, sometimes thousands of items of merchandise never finding an item they want to buy.  

#### Project Goal
This goal of this project is to create both content-based and collaborative user- and item-based recommender systems, that will help solve this problem. Customers should be provided suggestions based on their likes and needs in order to create a better shopping environment that boosts sales and increases their time spent on a website. 

#### Data Source

Since TIKI does not granted permission to its OpenAPI (except for sellers and co-operator), I have to scrape all the most relevant data on the web page [tiki.vn](https://tiki.vn). Details can be found in [this notebook](TikiScraper.ipynb)  

#### Data Cleaning
[Data Cleaning Notebook](TikiDataCleaning.ipynb)  
The data consists of many unrelevant information and NaNs. Therefore, I have drop multiple columns and only keep useful features.
For the products' info dataset, I have extracted the whole description using BeautifulSoup and then tokenizing it with PyVi for Vietnamese language.
For the products' review dataset, I have extracted the user's info using BeautifulSoup, including their full names, purchase time, comment time, etc.
All timestamp provided are converted into Datetime format for further investigation.

#### Modeling
[Feature Engineering & Recommender Model](TikiRecommender.ipynb)
2 different methods (Content-based Filtering and Collaborative Filtering) were tested, and the results are much more promising using the latter one.
I have tested multiple similarity metrics:
- Weighted Pearson Correlation Coefficient(WPCC)
- New Heuristic Similarity Model (NHSM)
- MJaccard similarity
- User Rating Preference similarity (URP)
and I have achieved the best prediction performance using MJaccard similarity. Therefore, the recommender system are going to use MJaccard similarity for Collaborative Filtering to recommend products for each user using their past reviews.

The best prediction performance was achieved with a SVM, using part of the features in the dataset, and resulted in the following metrics:

## Results
An example of the recommend products for user ID 2105483 (Huỳnh Đức Toàn)
#### Bought Products
+----+---------+-----------------------------------------------------------------------------------------------+-------------------------------------------------------+---------------------------------------------+
|    |      id | name                                                                                          | description                                           | category_name                               |
+====+=========+===============================================================================================+=======================================================+=============================================+
| 23 | 2293833 | Combo 2 hộp Nhang Xanh 30cm-500g (Chân Tăm Mộc ) Nhang Trầm Sạch 100% Vì Sức Khỏe Nhang Thiền | Thành phần:  bột trầm hương, keo bời lời, tăm tre.... | Nhà Cửa - Đời Sống/Đồ thờ cúng/Hương, nhang |
+----+---------+-----------------------------------------------------------------------------------------------+-------------------------------------------------------+---------------------------------------------+

#### Recommended Products with this System
+-------+----------+------------------------------------------------------------------------------------------------------+-------------------------------------------------------+-------------------------------------------------------------------------------------------------------------+
|       |       id | name                                                                                                 | description                                           | category_name                                                                                               |
+=======+==========+======================================================================================================+=======================================================+=============================================================================================================+
|   117 | 54734250 | Dây Nhảy Tập Thể Dục Cao Cấp Tại Nhà                                                                 | Dây thiết kế bằng PVC bọc lõi thép nên có độ bền c... | Thể Thao - Dã Ngoại/Dụng cụ - thiết bị tập thể thao/Dây nhảy                                                |
+-------+----------+------------------------------------------------------------------------------------------------------+-------------------------------------------------------+-------------------------------------------------------------------------------------------------------------+
|  2020 |  4539349 | Bộ Vệ Sinh Laptop                                                                                    | Bộ vệ sinh laptop gồm cọ, khăn lau, dụng cụ thổi b... | Thiết Bị Số - Phụ Kiện Số/Phụ kiện máy tính và Laptop/Dụng Cụ Vệ Sinh và Sửa Chữa/Dụng Cụ Vệ Sinh           |
+-------+----------+------------------------------------------------------------------------------------------------------+-------------------------------------------------------+-------------------------------------------------------------------------------------------------------------+
|  2549 |  3951133 | Chăn Lông Cừu Siêu Mềm Mịn (2m x 2m3)                                                                | Lông mềm mại mịn màng, màu sắc nhã nhặn Trọng lượn... | Nhà Cửa - Đời Sống/Đồ dùng phòng ngủ/Chăn, mền và phụ kiện/Chăn chần gòn                                    |
+-------+----------+------------------------------------------------------------------------------------------------------+-------------------------------------------------------+-------------------------------------------------------------------------------------------------------------+
|  3411 | 59200580 | Adapter Sạc Nhanh Xiaomi ZMI HA711 USB Type-C 18W - Hàng chính hãng                                  | Tham số đầu vào: 100-240V~50/60Hz 0.5A Tham số đầu... | Thiết Bị Số - Phụ Kiện Số/Phụ Kiện Điện Thoại và Máy Tính Bảng/Adapter - Củ Sạc/Adapter Sạc - Củ Sạc Thường |
+-------+----------+------------------------------------------------------------------------------------------------------+-------------------------------------------------------+-------------------------------------------------------------------------------------------------------------+
|  5054 | 49047291 | Đồng hồ nam FOURRON F1128 santafe watch 2020 Lịch ngày dây thép không gỉ cao cấp                     | Thương hiệu: FOURRON Kiểu Máy: Quartz Kích thước m... | Đồng hồ và Trang sức/Đồng hồ nam/Đồng hồ business nam                                                       |
+-------+----------+------------------------------------------------------------------------------------------------------+-------------------------------------------------------+-------------------------------------------------------------------------------------------------------------+
|  9933 | 42901507 | Áo thun Nam Nữ unisex ASALA  (ux-901)                                                                | áo thun thoáng mát đa năng unisex nam nữ đều mặc đ... | Thời trang nam/Áo thun nam                                                                                  |
+-------+----------+------------------------------------------------------------------------------------------------------+-------------------------------------------------------+-------------------------------------------------------------------------------------------------------------+
| 10354 | 41067638 | Áo giữ nhiệt lót nỉ nam                                                                              | Chất liệu vải thun mềm mai, dày dặn ấm áp Thiết kế... | Thời trang nam/Đồ ngủ, đồ mặc nhà nam/Đồ mặc nhà nam - Bộ ngắn                                              |
+-------+----------+------------------------------------------------------------------------------------------------------+-------------------------------------------------------+-------------------------------------------------------------------------------------------------------------+
| 14352 | 26334237 | Giày Thể Thao Nam DOL Cao Cổ tăng 7 cm chiều cao phối màu cá tính Ulzzangboy đường phố               | GIÀY BÍ MẬT TĂNG 7CM chiều cao (TẶNG 1 MIẾNG ĐỆM T... | Giày - Dép nam/Giày thể thao nam/Giày thể thao nam cổ cao                                                   |
+-------+----------+------------------------------------------------------------------------------------------------------+-------------------------------------------------------+-------------------------------------------------------------------------------------------------------------+
| 16041 | 72673068 | Quần Thể Thao Nam 5S (TK004) Cao Cấp Vải Gió Dáng Thể Thao, Ống Suông Trẻ Trung, Lưng Thun Thoải Mái | Tên sản phẩm: Quần Thể Thao Nam 5S (TK004) Cao Cấp... | Thời trang nam/Quần nam/Quần jogger nam                                                                     |
+-------+----------+------------------------------------------------------------------------------------------------------+-------------------------------------------------------+-------------------------------------------------------------------------------------------------------------+
| 17236 |   980470 | Bóng Đèn Philips LED Ecobright 8W 3000K E27 A60 - Ánh Sáng Vàng - Hàng Chính Hãng                    | Thiết kế nhỏ gọn, dễ dàng tháo lắp Công suất 8W, n... | Nhà Cửa - Đời Sống/Đèn & thiết bị chiếu sáng/Bóng đèn                                                       |
+-------+----------+------------------------------------------------------------------------------------------------------+-------------------------------------------------------+-------------------------------------------------------------------------------------------------------------+

## Conclusion
I have created a model using data scraped from TIKI website with the help of BeautifulSoup to train, deploy the final model. The deployment of the model is in development.

