# Домашнее задание к занятию 12.3. «SQL. Часть 1» - `Виноградова Татьяна`

---

### Задание 1
Получите уникальные названия районов из таблицы с адресами, которые начинаются на “K” и заканчиваются на “a” и не содержат пробелов.
``` SQL
select distinct a.district 
  from address a
  where a.district like "K%" and a.district like "%a" and a.district not like "% %" ;
```

### Задание 2
Получите из таблицы платежей за прокат фильмов информацию по платежам, которые выполнялись в промежуток с 15 июня 2005 года 
по 18 июня 2005 года **включительно** и стоимость которых превышает 10.00.
``` SQL
select *  
  from payment  
  where Date(payment_date)  between '2005-06-15' and '2005-06-18' and amount > 10;
```

### Задание 3
Получите последние пять аренд фильмов.
``` SQL
 select *  
  from rental 
  order by rental_date desc 
  limit 5 ;
``` 

### Задание 4
Одним запросом получите активных покупателей, имена которых Kelly или Willie. 

Сформируйте вывод в результат таким образом:
- все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр,
- замените буквы 'll' в именах на 'pp'.
``` SQL
select replace (lower(first_name),'ll', 'pp') as new_Name, customer_id 
  from customer
  where (first_name = 'kelly' or first_name = 'willie') and active = 1 ;
``` 

### Задание 5*
Выведите Email каждого покупателя, разделив значение Email на две отдельных колонки: в первой колонке должно быть значение, 
указанное до @, во второй — значение, указанное после @.
``` SQL
select substr(c.email , 1, position('@' in c.email ) - 1) as Name, substr(c.email, position('@' in c.email ) + 1) as Domain
  from customer c  
``` 

### Задание 6*
Доработайте запрос из предыдущего задания, скорректируйте значения в новых колонках: первая буква должна быть заглавной, остальные — строчными.
``` SQL
 select concat(upper(substr(c.email, 1, 1)), lower(substr(c.email , 2, position('@' in c.email ) - 2))) as Name, 
  concat(upper(substr(c.email, position('@' in c.email ) + 1, 1)), lower(substr(c.email, position('@' in c.email ) + 2))) as Domain
  from customer c
``` 
