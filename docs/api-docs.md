## Train Booking API Documentation

Полная спецификация API создана и размещена в **SwaggerHub**.  
[Открыть Swagger документацию](https://app.swaggerhub.com/apis/IRINAMACIAKA_1/Train_Booking_API/1.0.0)

Mock Server (для тестирования запросов):  
`https://virtserver.swaggerhub.com/IRINAMACIAKA_1/Train_Booking_API/1.0.0`

---

1. Регистрация пользователя
<pre> 
curl -X POST https://virtserver.swaggerhub.com/IRINAMACIAKA_1/Train_Booking_API/1.0.0/auth/register 
-H "accept: application/json" 
-H "Content-Type: application/json" 
-d '{ 
 "email": "test@example.com", 
 "password": "12345" 
}' 
</pre>

Ответ (200):
{ "message": "Регистрация прошла успешно" }

Ошибка (400):
{ "error": "Такой пользователь уже существует" }

Ошибка (500):
{ "error": "Internal server error" }

2. Авторизация пользователя
<pre> 
curl -X POST https://virtserver.swaggerhub.com/IRINAMACIAKA_1/Train_Booking_API/1.0.0/auth/login 
-H "accept: application/json" 
-H "Content-Type: application/json" 
-d '{
 "email": "test@example.com", 
 "password": "12345" 
}' 
</pre>

Ответ (200):
{ "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9" }

Ошибка (401):
{ "error": "Неправильный логин или пароль" }

Ошибка (404):
{ "error": "Пользователь не найден" }

Ошибка (500):
{ "error": "Internal server error" }

3. Поиск поездов
<pre> 
curl -X GET https://virtserver.swaggerhub.com/IRINAMACIAKA_1/Train_Booking_API/1.0.0/api/trains/search?from=Минск&to=Варшава 
-H "accept: application/json" 
</pre>

Ответ (200):
[
{ "id": 1, "from": "Минск", "to": "Варшава", "time": "08:30", "price": 45 },
{ "id": 2, "from": "Минск", "to": "Москва", "time": "10:00", "price": 60 }
]

Ошибка (400):
{ "error": "Invalid query parameters" }

Ошибка (500):
{ "error": "Internal server error" }

4. Информация о поезде
<pre> 
curl -X GET https://virtserver.swaggerhub.com/IRINAMACIAKA_1/Train_Booking_API/1.0.0/api/trains/1 
-H "accept: application/json" 
</pre>

Ответ (200):
{
"id": 1,
"from": "Минск",
"to": "Варшава",
"time": "08:30",
"price": 45
}

Ошибка (404):
{ "error": "Train not found" }

Ошибка (500):
{ "error": "Internal server error" }

5. Забронировать билет
<pre> 
curl -X POST https://virtserver.swaggerhub.com/IRINAMACIAKA_1/Train_Booking_API/1.0.0/api/orders 
-H "accept: application/json" 
-H "Content-Type: application/json" 
-d '{
 "trainId": 1,
 "passenger": {
   "name": "Алекс Морозов",
   "age": 25
  } 
}' </pre>

Ответ (200):
{
"message": "Ticket booked",
"order": {
"id": 1,
"trainId": 1,
"paid": false
}
}

Ошибка (400):
{ "error": "trainId and passenger are required" }

Ошибка (500):
{ "error": "Internal server error" }

6. История заказов пользователя
<pre> 
curl -X GET https://virtserver.swaggerhub.com/IRINAMACIAKA_1/Train_Booking_API/1.0.0/api/orders 
-H "accept: application/json" 
</pre>

Ответ (200):
[
{ "id": 1, "trainId": 1, "paid": true },
{ "id": 2, "trainId": 2, "paid": false }
]

Ошибка (500):
{ "error": "Internal server error" }

7. Оплата билета
<pre> 
curl -X POST https://virtserver.swaggerhub.com/IRINAMACIAKA_1/Train_Booking_API/1.0.0/api/orders/1/pay 
-H "accept: application/json" 
</pre>

Ответ (200):
{ "message": "Payment successful" }

Ошибка (404):
{ "error": "Order not found" }

Ошибка (500):
{ "error": "Internal server error" }

8. Получить данные профиля
<pre> 
curl -X GET https://virtserver.swaggerhub.com/IRINAMACIAKA_1/Train_Booking_API/1.0.0/api/profile 
-H "accept: application/json" 
</pre>

Ответ (200):
{
"name": "Алекс Морозов",
"phone": "+375291234567",
"city": "Минск"
}

Ошибка (500):
{ "error": "Internal server error" }

9. Обновить профиль
<pre> 
curl -X PUT https://virtserver.swaggerhub.com/IRINAMACIAKA_1/Train_Booking_API/1.0.0/api/profile 
-H "accept: application/json" 
-H "Content-Type: application/json" 
-d '{ "name": "Алекс Морозов", "phone": "+375291234567", "city": "Минск" }' 
</pre>

Ответ (200):
{ "message": "Profile updated" }

Ошибка (400):
{ "error": "Invalid input data" }

Ошибка (500):
{ "error": "Internal server error" }

10. Получить список акций
<pre> 
curl -X GET https://virtserver.swaggerhub.com/IRINAMACIAKA_1/Train_Booking_API/1.0.0/api/promotions 
-H "accept: application/json" 
</pre>

Ответ (200):
[
{
"id": 1,
"title": "Скидка 10% на ночные рейсы",
"description": "Действует с 22:00 до 6:00"
},
{
"id": 2,
"title": "2 билета по цене одного",
"description": "Действует по выходным"
}
]

Ошибка (500):
{ "error": "Internal server error" }

11. Получить список пассажиров
<pre> 
curl -X GET https://virtserver.swaggerhub.com/IRINAMACIAKA_1/Train_Booking_API/1.0.0/api/passengers 
-H "accept: application/json" 
</pre>

Ответ (200):
[
{ "name": "Алекс Морозов", "age": 25 },
{ "name": "Анна Петрова", "age": 30 }
]

Ошибка (500):
{ "error": "Internal server error" }

12. Добавить пассажира
<pre> 
curl -X POST https://virtserver.swaggerhub.com/IRINAMACIAKA_1/Train_Booking_API/1.0.0/api/passengers 
-H "accept: application/json" 
-H "Content-Type: application/json" 
-d '{ "name": "Ольга Иванова", "age": 28 }' 
</pre>

Ответ (200):
{ "message": "Passenger added" }

Ошибка (400):
{ "error": "Invalid passenger data" }

Ошибка (500):
{ "error": "Internal server error" }

13. Получить список обращений
<pre> 
curl -X GET https://virtserver.swaggerhub.com/IRINAMACIAKA_1/Train_Booking_API/1.0.0/api/support/tickets 
-H "accept: application/json" 
</pre>

Ответ (200):
[
{ "id": 1, "message": "Не работает оплата", "user": "test@example.com
" },
{ "id": 2, "message": "Ошибка при бронировании", "user": "test@example.com
" }
]

Ошибка (500):
{ "error": "Internal server error" }

14. Создать обращение
<pre> 
curl -X POST https://virtserver.swaggerhub.com/IRINAMACIAKA_1/Train_Booking_API/1.0.0/api/support/tickets 
-H "accept: application/json" 
-H "Content-Type: application/json" 
-d '{ 
 "message": "Не удаётся оплатить билет" 
}' 
</pre>

Ответ (200):
{ "message": "Ticket created" }

Ошибка (400):
{ "error": "Message is required" }

Ошибка (500):
{ "error": "Internal server error" }

15. Получить список всех поездов (админ)
<pre> 
curl -X GET https://virtserver.swaggerhub.com/IRINAMACIAKA_1/Train_Booking_API/1.0.0/api/admin/flights 
-H "accept: application/json" 
</pre>

Ответ (200):
[
{ "id": 1, "from": "Минск", "to": "Варшава", "time": "08:30", "price": 45 },
{ "id": 2, "from": "Минск", "to": "Москва", "time": "10:00", "price": 60 }
]

Ошибка (500):
{ "error": "Internal server error" }

16. Добавить новый поезд (админ)
<pre> 
curl -X POST https://virtserver.swaggerhub.com/IRINAMACIAKA_1/Train_Booking_API/1.0.0/api/admin/flights 
-H "accept: application/json" 
-H "Content-Type: application/json" 
-d '{ "from": "Минск", "to": "Вильнюс", "time": "15:30", "price": 70 }' 
</pre>

Ответ (200):
{ "message": "Train added" }

Ошибка (400):
{ "error": "Invalid train data" }

Ошибка (500):
{ "error": "Internal server error" }

17. Обновить поезд (админ)
<pre> curl -X PUT https://virtserver.swaggerhub.com/IRINAMACIAKA_1/Train_Booking_API/1.0.0/api/admin/flights/1 -H "accept: application/json" -H "Content-Type: application/json" -d '{ "price": 75 }' </pre>

Ответ (200):
{ "message": "Train updated" }

Ошибка (404):
{ "error": "Train not found" }

Ошибка (500):
{ "error": "Internal server error" }

18. Удалить поезд (админ)
<pre> 
curl -X DELETE https://virtserver.swaggerhub.com/IRINAMACIAKA_1/Train_Booking_API/1.0.0/api/admin/flights/1 
-H "accept: application/json" 
</pre>

Ответ (200):
{ "message": "Train deleted" }

Ошибка (404):
{ "error": "Train not found" }

Ошибка (500):
{ "error": "Internal server error" }

19. Получить статистику обращений (админ)
<pre> 
curl -X GET https://virtserver.swaggerhub.com/IRINAMACIAKA_1/Train_Booking_API/1.0.0/api/admin/support/statistics 
-H "accept: application/json" </pre>

Ответ (200):
{
"totalTickets": 25,
"resolved": 20,
"pending": 5
}

Ошибка (500):
{ "error": "Internal server error" }

20. Получить все акции (админ)
<pre> 
curl -X GET https://virtserver.swaggerhub.com/IRINAMACIAKA_1/Train_Booking_API/1.0.0/api/admin/promotions 
-H "accept: application/json" </pre>

Ответ (200):
[
{ "id": 1, "title": "Скидка 10%", "description": "На ночные рейсы" }
]

Ошибка (500):
{ "error": "Internal server error" }

21. Добавить акцию (админ)
<pre> 
curl -X POST https://virtserver.swaggerhub.com/IRINAMACIAKA_1/Train_Booking_API/1.0.0/api/admin/promotions 
-H "accept: application/json" 
-H "Content-Type: application/json" -d '{ "title": "Скидка 15% на утренние рейсы", "description": "Действует до конца месяца" }' </pre>

Ответ (200):
{ "message": "Promotion added" }

Ошибка (400):
{ "error": "Invalid promotion data" }

Ошибка (500):
{ "error": "Internal server error" }

22. Обновить акцию (админ)
<pre> 
curl -X PUT https://virtserver.swaggerhub.com/IRINAMACIAKA_1/Train_Booking_API/1.0.0/api/admin/promotions/1 
-H "accept: application/json" 
-H "Content-Type: application/json" 
-d '{ "description": "Обновлено: действует до декабря" }' </pre>

Ответ (200):
{ "message": "Promotion updated" }

Ошибка (404):
{ "error": "Promotion not found" }

Ошибка (500):
{ "error": "Internal server error" }

23. Удалить акцию (админ)
<pre> curl -X DELETE https://virtserver.swaggerhub.com/IRINAMACIAKA_1/Train_Booking_API/1.0.0/api/admin/promotions/1 
-H "accept: application/json" </pre>

Ответ (200):
{ "message": "Promotion deleted" }

Ошибка (404):
{ "error": "Promotion not found" }

Ошибка (500):
{ "error": "Internal server error" }

24. Получить список пользователей (админ)
<pre> curl -X GET https://virtserver.swaggerhub.com/IRINAMACIAKA_1/Train_Booking_API/1.0.0/api/admin/users 
-H "accept: application/json" </pre>

Ответ (200):
[
{ "email": "test@example.com
" },
{ "email": "user2@example.com
" }
]

Ошибка (500):
{ "error": "Internal server error" }

25. Получить бизнес-статистику (админ)
<pre> curl -X GET https://virtserver.swaggerhub.com/IRINAMACIAKA_1/Train_Booking_API/1.0.0/api/admin/statistics 
-H "accept: application/json" </pre>

Ответ (200):
{
"totalSales": 15200,
"totalUsers": 340
}

Ошибка (500):
{ "error": "Internal server error" }
