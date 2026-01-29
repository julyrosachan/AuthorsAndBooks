create database Library;

 use Library;

create table authors(
    id int primary key identity,
    name nvarchar(50) not null,
    surname nvarchar(60) not null 
);

INSERT INTO Authors (Name, Surname)
VALUES 
('George', 'Orwell'),
('Fyodor', 'Dostoyevski'),
('Elchin', 'Huseynbeyli')

 create table books(
    id int primary key identity,
    authorid int not null,
    name nvarchar(100) not null check(LEN(name) >= 2),
    pagecount int not null check (pagecount >= 10),

    constraint FK_books_authors
    foreign key (authorid) references authors(id)
 );

 insert into books (authorid, name, pagecount)
values
(1, '1984', 328),
(1, 'Animal Farm', 112),
(2, 'Crime and Punishment', 671),
(2, 'The Idiot', 656),
(3, 'Balaca Shahzade', 96)

select * from authors;
select * from books;

create view vw_bookswithauthors
 as 
 select 
 b.id,
 b.name,
 b.pagecount,
 a.name + ' ' + a.surname as authorfullname
 from books b 
 join authors a on b.authorid = a.id

 select * from vw_bookswithauthors

 create procedure usp_searchbooks
 @search nvarchar(50)
 as 
 begin 
 select
 b.id,
 b.name,
 b.pagecount,
 a.name + ' ' + a.surname as authorfullname
 from books b 
 join authors a on b.authorid = a.id
 where b.name like '%' + @search + '%'
 or a.name like '%' + @search +'%'
 end



create function fn_BookCountByPage
(
    @MinPageCount int = 10
)
returns int
as
begin
    declare @Count int

    select @Count = COUNT(*)
    from
     books
    WHERE PageCount > @MinPageCount

    RETURN @Count
END

CREATE TABLE DeletedBooks (
    Id INT,
    AuthorId INT,
    Name NVARCHAR(100),
    PageCount INT,
    DeletedDate DATETIME DEFAULT GETDATE()
)

CREATE TRIGGER trg_Books_Delete
ON Books
AFTER DELETE
AS
BEGIN
    INSERT INTO DeletedBooks (Id, AuthorId, Name, PageCount)
    SELECT Id, AuthorId, Name, PageCount
    FROM deleted
END

DELETE FROM Books WHERE Id = 1
SELECT * FROM DeletedBooks



