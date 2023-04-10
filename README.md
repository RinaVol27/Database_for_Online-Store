# Database_for_Online-Store

![image](https://user-images.githubusercontent.com/130033747/230872447-d8d172b3-fd80-464a-8413-5f8ce1ca0568.png)


create table Site_User     --Пользователь ✅ </br>
(Id_user int identity primary key not null,</br>  
Surname nvarchar(50) not null,</br>
name_user nvarchar(50),</br>
Patronymic nvarchar(50) null,  --Отчество</br>
Date_of_birth date not null,</br>
Company nvarchar(50) null,   --Представитель компании</br>
City nvarchar(50) not null,</br>
Phone nvarchar(25) not null,</br>
Email nvarchar(100) null</br>
);</br>

create table User_Card   --Карта ✅ </br>
(Id_card int primary key not null,</br>
Id_user int not null</br>
foreign key (Id_user) references Site_User (Id_user));</br>


create table User_Order    --Заказ  ✅ </br>
(id_order int identity primary key not null,</br>
Id_user int not null,</br>
assembly_period int null,  --срок сборки</br>
id_payment int  not null,    --способ оплаты</br>
id_delivery int  not null,    --код доставки</br>
order_date date not null,</br>
information nvarchar(max) null,</br>
City nvarchar(50) not null,</br>
Street nvarchar(50) not null,</br>
house nvarchar(50) not null,</br>
entrance int null,  --подъезд</br>
num_floor int null,</br>
apartment int null,  --номер квартиры</br>
index_us int not null,</br>

foreign key (Id_user) references Site_User (Id_user),</br>
foreign key (id_payment) references Payment (id_payment),</br>
foreign key (id_delivery) references delivery (id_delivery));</br>

create table Payment  ✅ </br>
(id_payment int identity primary key not null,</br>

payment_method nvarchar(50) not null,</br>
Currency nvarchar(50) null,   --валюта</br>
Id_card int not null,</br>

foreign key (Id_card) references user_card (Id_card)</br>
);</br>

create table Delivery  ✅ </br>
(id_delivery int identity primary key not null,    --код доставки</br>
delivery_method nvarchar(100) not null,</br>
id_courier int null,</br>
id_transport int null,</br>

foreign key (Id_courier) references courier (Id_courier),</br>
foreign key (Id_transport) references transport (Id_transport)</br>
);</br>

create table Courier ✅ </br>
(id_courier int identity primary key not null,</br>
Surname nvarchar(50) not null,  </br>
name_courier nvarchar(50),</br>
Patronymic nvarchar(50) null,  --Отчество</br>
Phone nvarchar(25) not null,</br>
Email nvarchar(100) null,</br>
rating int not null   --рейтинг</br>
);</br>

create table Transport ✅ </br>
(id_transport int identity primary key not null,</br>
transport_name nvarchar(50) not null,</br>
number_tr nvarchar(50) null</br>
);

create table Order_Contents     --Содержимое_заказа ✅ </br>
(id_product int not null,</br>
id_order int not null,</br>
count_product int not null,   --количество</br>
packaging nvarchar(50) not null,  --упаковка</br>

foreign key (id_order) references user_order (id_order),</br>
foreign key (id_product) references product (id_product),</br>
foreign key (packaging) references product_packaging (packaging));</br>

create table Product_Packaging ✅ </br>
(packaging nvarchar(50) primary key not null,</br>
price money not null,</br>
quality int not null   --качество</br>
);</br>

create table Product ✅ </br>
(id_product int identity primary key not null,</br>
product_name nvarchar(50) not null,</br>
Category nvarchar(50) not null,</br>
Count_product_on_warehouse int not null,   --количество на складе</br>
Count_in_box int not null,   --количество в упаковке</br>
Color nvarchar(50) null,</br>
information nvarchar(max) null,</br>
country nvarchar(50) not null,</br>
id_manufacturer int not null,</br>
expiration_date int not null,   --срок годности</br>
production_date date not null,  --дата производства продукта</br>
price money not null,</br>
image_pr nvarchar(max) null,</br>
weight_pr decimal(10, 1) not null</br>
foreign key (Category) references product_Category (Category),</br>
foreign key (id_manufacturer) references manufacturer (id_manufacturer));</br>

create table Product_Category ✅ </br>
(Category nvarchar(50) primary key not null,</br>
information nvarchar(max) not null</br>
);</br>
 
create table Manufacturer ✅ </br>
(id_manufacturer int identity primary key not null,</br>
Manuf_name nvarchar(50) not null,</br>
City nvarchar(50) not null,</br>
Phone nvarchar(25) not null,</br>
Email nvarchar(100) null,</br>
Street nvarchar(50) not null,</br>
house nvarchar(50) not null,</br>
entrance int null,  --подъезд</br>
num_floor int null,</br>
apartment int null,  --номер квартиры</br>
index_us int not null</br>
);
