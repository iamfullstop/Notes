# Project Setup CRUD on WINDOWS app

    - Create a new project
    - Windows Form App 
    - Fill the options
    - Open SQL SERVER
    - paste the code

``` sql
create database FruitBasket;
use FruitBasket;
create table ProductCategory(
        catId int primary key,
        catName nvarchar(50) not null unique
);

create table Product(
        pId int primary key,
        pName nvarchar(40) not null unique,
        catId int not null foreign key references ProductCategory(catId),
        mrp decimal(12,2) not null default(0) check(mrp>=0),
        stockBalance int not null default(0) check(stockBalance>=0)
);

create table StockEntry(
        eId bigint primary key,
        pId int not null foreign key references Product(pId),
        quantity int check(quantity<>0), -- positive for stock in/negative for stockout
        stockDate date not null ,
        stockTime nvarchar(40) not null
);

-- Auto update Stock Info | sidebyside execution 
create or alter trigger tgr_StockEntry on StockEntry after insert,update,delete
as
begin
        declare @delQuantity as int=0,@insQuantity as int=0, @pId as int;
        select @pId=case when pId is not null then pid end,@delQuantity=case when quantity is null then 0 else quantity end from deleted;
        select @pId=case when pId is not null then pid end,@insQuantity=case when quantity is null then 0 else quantity end from inserted;
        update Product set stockBalance=stockBalance-@delQuantity+@insQuantity where pId=@pId;
end;

insert into ProductCategory(catid,catName) values(1,'kitchen item');
insert into Product(pId,pName,catId) values (1,'Rice cooker',1);
insert into StockEntry(eId,pId,quantity,stockDate,stockTime) values (1,1,4,getdate(),convert(time,getdate()));

select * from ProductCategory;
select * from Product;
select * from StockEntry;
delete from StockEntry;
disable trigger dbo.tgr_StockEntry on StockEntry
```
