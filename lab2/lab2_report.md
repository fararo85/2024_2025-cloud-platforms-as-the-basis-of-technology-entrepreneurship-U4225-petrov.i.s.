University: ITMO University

Faculty: FTMI

Course: Cloud platforms as the basis of technology entrepreneurship

Year: 2024

Group: U4225

Author: Petrov Ilya Stanislavovich

Lab: Lab2

Date of create: 25.10.2024

Date of finished: 26.10.2024

1.	Создал Cloud Run из представленного дефолтного сервиса Hello. 
![image_2024-10-25_21-13-42](https://github.com/user-attachments/assets/81ed4515-a88d-4f80-9eb5-1bd73f98d66b)

2.	Перешел по ссылке предоставленной Cloud Run и протестировал сервис.
![image_2024-10-25_21-14-19](https://github.com/user-attachments/assets/3049cb87-e1e6-4e2f-af0d-1fe0b5b4fa54)

3.	Перешел в разделы метрики:
![image](https://github.com/user-attachments/assets/55f15724-9391-4678-a22b-6b3bc9f24e4b)
![image](https://github.com/user-attachments/assets/1a322cb6-0e1a-4ba6-9021-508dea04dff2)
![image](https://github.com/user-attachments/assets/b4f42c95-37c2-4310-bd7b-5d500591aadb)
![image](https://github.com/user-attachments/assets/b7aa8b81-d3af-437d-8908-21528f3c5027)
Метрики показывают различные стандартные параметры контейнера, такие как: число запросов, задержка запросов, подсчет инстанций контейнера, сколько памяти использует контейнер и так далее.

4.	Перешел в разделы логи:
![image](https://github.com/user-attachments/assets/d886d68f-45c5-45cc-90fe-e53f1c73f40c)
•	В начале система создает новый сервис в Cloud Run с именем "ipetrov-lab2". Это сопровождается записями типа Services.CreateService, что означает успешное создание сервиса.

•	Затем отмечается событие создания новой инстанции (контейнера). Причина — OVERFLOW, что указывает на необходимость запуска дополнительной инстанции из-за нехватки текущих ресурсов для обработки трафика. Это нормальная ситуация, когда контейнеры автоматически масштабируются в зависимости от нагрузки.

•	После этого контейнер был успешно запущен, о чем говорит сообщение Hello from Cloud Run!, а также указано, что контейнер ожидает HTTP-запросов на порту 8080. Лог показывает, что контейнер начал прослушивать порт 8080, а также произошло успешное подключение через протокол TCP на этот порт.

•	После запуска контейнера система начала обрабатывать HTTP-запросы (метод GET) с клиента Chrome. Время ответа на каждый запрос было достаточно быстрым (6-7 мс), что свидетельствует о нормальной работе сервиса и адекватном времени отклика.

5.	Изменил наш Cloud Run, поменяв порт на 8090.
![image](https://github.com/user-attachments/assets/2b567939-3e1f-4a64-bfa4-ef139d6b5832)

• Контейнер снова успешно запустился, что подтверждается сообщением Hello from Cloud Run!. Контейнер теперь прослушивает HTTP-запросы на порту 8090. Это указывает на то, что конфигурация порта была изменена, и сервис начал работать на новом порту.

• Далее TCP probe прошел успешно с первой попытки. Это означает, что система проверила доступность контейнера на новом порту 8090, и контейнер ответил корректно на проверку. Это стандартная процедура проверки того, что контейнер готов к работе.

• Затем логи показывают операцию ReplaceService, что означает, что Cloud Run заменяет старый сервис на новый с обновленными конфигурациями. Это подтверждает, что сервис был перезапущен с изменениями, которые включают новый порт 8090.

• Последняя запись указывает на то, что контейнер успешно обработал HTTP-запрос от браузера Chrome. Как и в предыдущем случае, запрос был выполнен быстро (4 мс), что указывает на корректную работу сервиса на новом порту.

• Изначально трафик был распределен 80 на 20, далее перераспределил его 50 на 50:
![image](https://github.com/user-attachments/assets/865544c5-1c6a-417a-9321-fbcd61ee0f82)
Container Instance Time:
Время использования контейнера показывает 2 всплеска, что связано с изменением нагрузки. Сначала один контейнер обрабатывал 80% трафика, после перераспределения на 50/50 оба контейнера стали обрабатывать примерно равные объёмы трафика.
![image](https://github.com/user-attachments/assets/7d30b618-e78a-4f6b-8cf9-06929fa3df1a)
При перераспределении трафика до 50/50 память обоих контейнеров уравновесилась, так как нагрузка была распределена равномерно.

Вывод: Система запустила контейнер с новой конфигурацией порта, проверила его доступность через TCP, и контейнер начал обслуживать HTTP-запросы. Логи показывают нормальную работу сервиса без каких-либо ошибок. При измнении трафика на 50/50 мы видим уменьшении нагрузки, так как нагрузка распределена равномерно.
