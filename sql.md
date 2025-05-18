Работа с базой данных
Задание 1

Представь: тебе нужно проверить, отображается ли созданный заказ в базе данных.
Для этого: выведи список логинов курьеров с количеством их заказов в статусе «В доставке» (поле inDelivery = true). 


SELECT c.login, Count(o.id) AS "deliveryCount" 
FROM "Couriers" AS c 
LEFT JOIN "Orders" AS o ON c.id = o."courierId"
WHERE o."inDelivery" = true
Group BY c.login;


![image](https://github.com/user-attachments/assets/08e5935c-a1a3-47e5-8149-8122308898a1)


Задание 2
Ты тестируешь статусы заказов. Нужно убедиться, что в базе данных они записываются корректно.
Для этого: выведи все трекеры заказов и их статусы. 
Статусы определяются по следующему правилу:
Если поле finished == true, то вывести статус 2.
Если поле canсelled == true, то вывести статус -1.
Если поле inDelivery == true, то вывести статус 1.
Для остальных случаев вывести 0.


SELECT track, 
    CASE 
        WHEN finished = true THEN 2 
	WHEN cancelled = true THEN -1 
        WHEN "inDelivery" = true THEN 1 
        ELSE 0 END AS status 
FROM "Orders";



![image](https://github.com/user-attachments/assets/9565d6c6-2ac9-4a80-ba41-18eda357119c)





Технические примечания:
Доступ к базе осуществляется с помощью команды psql -U morty -d scooter_rent. Пароль: smith.
У psql есть особенность: если таблица в базе данных с большой буквы, то её в запросе нужно брать в кавычки. Например, select * from “Orders”.
