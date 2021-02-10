# Tiki-Recommender-System


_Author: Hieu Khuong_

-------
### Table of Contents
[Data Scraping](TikiScraper.ipynb)  
[Data Cleaning](TikiDataCleaning.ipynb)  
[Feature Engineering & Recommender Model](TikiRecommender.ipynb)

## Executive Summary

#### Project Goal
Recommender systems are widely used in product recommendations such as recommendations of music, movies, books, news, research articles, restaurants, etc.
The goal of this project is to create both content-based and collaborative-filtering-based recommender systems to help solve this problem. Customers should be provided suggestions based on their likes and needs in order to create a better shopping environment that boosts sales and increases their time spent on a website. 

#### [Data Scraping](TikiScraper.ipynb)  

Since TIKI does not granted permission to its OpenAPI (except for sellers and co-operator), I have to scrape all the most relevant data on the web page [tiki.vn](https://tiki.vn).

#### [Data Cleaning](TikiDataCleaning.ipynb)  
The data consists of many unrelevant information and NaNs. Therefore, I have drop multiple columns and only keep useful features.
For the products' info dataset, I have extracted the whole description using BeautifulSoup and then tokenizing it with PyVi for Vietnamese language.
For the products' review dataset, I have extracted the user's info using BeautifulSoup, including their full names, purchase time, comment time, etc.
All timestamp provided are converted into Datetime format for further investigation.

#### [Feature Engineering & Recommender Model](TikiRecommender.ipynb)
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

|       |       id | name                                                                                          | description                                           | category_name                                                  |
|------:|---------:|:----------------------------------------------------------------------------------------------|:------------------------------------------------------|:---------------------------------------------------------------|
|    23 |  2293833 | Combo 2 hộp Nhang Xanh 30cm-500g (Chân Tăm Mộc ) Nhang Trầm Sạch 100% Vì Sức Khỏe Nhang Thiền | Thành phần:  bột trầm hương, keo bời lời, tăm tre.... | Nhà Cửa - Đời Sống/Đồ thờ cúng/Hương, nhang                    |
|   751 | 22689010 | Combo 3 áo thun trơn nam thời trang Everest màu trắng đen xám                                 | Chất liệu thun mềm mại co giãn tốt , thoáng mát Th... | Thời trang nam/Áo thun nam                                     |
|  2131 | 29115771 | Quần Jogger Nam Thun Nỉ Ống Bó Có Big Size                                                    | Quần jogger nỉ được may bằng chất liệu thun nỉ và ... | Thời trang nam/Quần nam/Quần jogger nam                        |
|  6070 |  4616949 | Mũ len kèm khăn                                                                               | Chất liệu len cao cấp không bông xù. Mặt trong lót... | Phụ kiện thời trang/Phụ kiện thời trang nam/Nón nam            |
| 10271 | 56337264 | Xe đạp tập thể dục T-366                                                                      | Xe đạp tập thể dục T366 MẪU MÃ SẢN PHẨM ĐẸP MẮT KI... | Thể Thao - Dã Ngoại/Dụng cụ - thiết bị tập thể thao/Xe đạp tập |

#### Recommended Products with this System

|       |       id | name                                                                                                 | description                                           | category_name                                                  |
|------:|---------:|:-----------------------------------------------------------------------------------------------------|:------------------------------------------------------|:---------------------------------------------------------------|
|  5054 | 49047291 | Đồng hồ nam FOURRON F1128 santafe watch 2020 Lịch ngày dây thép không gỉ cao cấp                     | Thương hiệu: FOURRON Kiểu Máy: Quartz Kích thước m... | Đồng hồ và Trang sức/Đồng hồ nam/Đồng hồ business nam          |
|  9933 | 42901507 | Áo thun Nam Nữ unisex ASALA  (ux-901)                                                                | áo thun thoáng mát đa năng unisex nam nữ đều mặc đ... | Thời trang nam/Áo thun nam                                     |
| 10354 | 41067638 | Áo giữ nhiệt lót nỉ nam                                                                              | Chất liệu vải thun mềm mai, dày dặn ấm áp Thiết kế... | Thời trang nam/Đồ ngủ, đồ mặc nhà nam/Đồ mặc nhà nam - Bộ ngắn |
| 14352 | 26334237 | Giày Thể Thao Nam DOL Cao Cổ tăng 7 cm chiều cao phối màu cá tính Ulzzangboy đường phố               | GIÀY BÍ MẬT TĂNG 7CM chiều cao (TẶNG 1 MIẾNG ĐỆM T... | Giày - Dép nam/Giày thể thao nam/Giày thể thao nam cổ cao      |
| 16041 | 72673068 | Quần Thể Thao Nam 5S (TK004) Cao Cấp Vải Gió Dáng Thể Thao, Ống Suông Trẻ Trung, Lưng Thun Thoải Mái | Tên sản phẩm: Quần Thể Thao Nam 5S (TK004) Cao Cấp... | Thời trang nam/Quần nam/Quần jogger nam                        |

## Conclusion
I have created a model using data scraped from TIKI website with the help of BeautifulSoup to train, deploy the final model. The deployment of the model is in development.

