# Database_for_Online-Store

![image](https://user-images.githubusercontent.com/130033747/230889475-02b4689b-7e6d-4abe-adbc-326d252de7a0.png)


create table Site_User     --Пользователь     
(Id_user int identity primary key not null,       
Surname nvarchar(50) not null,      
name_user nvarchar(50),      
Patronymic nvarchar(50) null,  --Отчество      
Date_of_birth date not null,      
Company nvarchar(50) null,   --Представитель компании      
City nvarchar(50) not null,      
Phone nvarchar(25) not null,     
Email nvarchar(100) null,      
is_delete bit default 0      
);      

create table User_Card   --Карта    
(Id_card int identity primary key not null,     
number_card int not null,      
Id_user int not null,     
is_delete bit default 0     
foreign key (Id_user) references Site_User (Id_user));     


create table User_Order    --Заказ     
(id_order int identity primary key not null,     
Id_user int not null,    
assembly_period int null,  --срок сборки    
id_payment int  not null,    --способ оплаты    
id_delivery int  not null,    --код доставки     
order_date date not null,     
information nvarchar(max) null,     
City nvarchar(50) not null,      
Street nvarchar(50) not null,      
house nvarchar(50) not null,     
entrance int null,  --подъезд         
num_floor int null,     
apartment int null,  --номер квартиры     
index_us int not null,     
is_delete bit default 0,     

foreign key (Id_user) references Site_User (Id_user),     
foreign key (id_payment) references Payment (id_payment),    
foreign key (id_delivery) references delivery (id_delivery));    

create table Payment    
(id_payment int identity primary key not null,    

payment_method nvarchar(50) not null,    
Currency nvarchar(50) null,   --валюта    
Id_card int not null,    
is_delete bit default 0,    

foreign key (Id_card) references user_card (Id_card)    
);     

create table Delivery     
(id_delivery int identity primary key not null,    --код доставки    
delivery_method nvarchar(100) not null,     
id_courier int null,      
id_transport int null,    
is_delete bit default 0,     

foreign key (Id_courier) references courier (Id_courier),     
foreign key (Id_transport) references transport (Id_transport)     
);     

create table Courier    
(id_courier int identity primary key not null,    
Surname nvarchar(50) not null,      
name_courier nvarchar(50),     
Patronymic nvarchar(50) null,  --Отчество     
Phone nvarchar(25) not null,    
Email nvarchar(100) null,     
rating int not null,   --рейтинг     
is_delete bit default 0      
);     

create table Transport     
(id_transport int identity primary key not null,     
transport_name nvarchar(50) not null,     
number_tr nvarchar(50) null,     
is_delete bit default 0     
);     

create table Order_Contents     --Содержимое_заказа     
(id int identity primary key not null,     
id_product int not null,     
id_order int not null,     
count_product int not null,   --количество     
packaging nvarchar(50) not null,  --упаковка     
is_delete bit default 0,     

foreign key (id_order) references user_order (id_order),     
foreign key (id_product) references product (id_product),    
foreign key (packaging) references product_packaging (packaging));     

create table Product_Packaging     
(packaging nvarchar(50) primary key not null,     
price money not null,     
quality int not null,   --качество     
is_delete bit default 0     
);      

create table Product      
(id_product int identity primary key not null,     
product_name nvarchar(50) not null,     
Category nvarchar(50) not null,      
Count_product_on_warehouse int not null,   --количество на складе     
Count_in_box int not null,   --количество в упаковке     
Color nvarchar(50) null,     
information nvarchar(max) null,     
country nvarchar(50) not null,     
id_manufacturer int not null,     
expiration_date int not null,   --срок годности     
production_date date not null,  --дата производства продукта     
price money not null,    
image_pr nvarchar(max) null,    
weight_pr decimal(10, 1) not null,    
is_delete bit default 0,    
foreign key (Category) references product_Category (Category),    
foreign key (id_manufacturer) references manufacturer (id_manufacturer));    

create table Product_Category    
(Category nvarchar(50) primary key not null,    
information nvarchar(max) not null,    
is_delete bit default 0    
);    

create table Manufacturer    
(id_manufacturer int identity primary key not null,    
Manuf_name nvarchar(50) not null,    
City nvarchar(50) not null,    
Phone nvarchar(25) not null,    
Email nvarchar(100) null,    
Street nvarchar(50) not null,    
house nvarchar(50) not null,    
entrance int null,  --подъезд    
num_floor int null,    
apartment int null,  --номер квартиры    
index_us int not null,    
is_delete bit default 0    
);
