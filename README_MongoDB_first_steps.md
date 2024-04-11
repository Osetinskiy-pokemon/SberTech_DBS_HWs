# SberTech_DBS_MongoDB_first_steps

## Задание:
* Установить MongoDB одним из способов: на локальный компьютер, в Docker или на виртуальную машину (облачный сервис);
* Создать базу данных и заполнить её данными из предложенных датасетов (примеры датасетов https://habr.com/ru/company/edison/blog/480408/ );
* Написать несколько запросов на выборку, обновление и удаление данных (все CRUD операции);
* Создать индекс и сравнить производительность запросов выборки.

Создаем базу данных. Датасет содержит информацию о Титанике про пассажиров (возраст, пол, родственники на борту и пр) 891 в тренировочном сете и 418 — в тестовом.
![image](https://github.com/Osetinskiy-pokemon/SberTech_DBS_MongoDB_first_steps/assets/71440118/7298a552-6eeb-4920-afeb-0934c25ce196)

Создали пустую:
![image](https://github.com/Osetinskiy-pokemon/SberTech_DBS_MongoDB_first_steps/assets/71440118/ce4b192d-4d48-49dc-bc53-d04617a4e49b)

Заливаем данные:
![image](https://github.com/Osetinskiy-pokemon/SberTech_DBS_MongoDB_first_steps/assets/71440118/4f09f727-a51f-4573-8ae7-c5992cc21c1b)

Начнем с операций поиска (ниже пойдут просто примерные операции, разные виды:

![image](https://github.com/Osetinskiy-pokemon/SberTech_DBS_MongoDB_first_steps/assets/71440118/a90b750c-e21a-4641-ae4a-ee1a29fb4a5d)

![image](https://github.com/Osetinskiy-pokemon/SberTech_DBS_MongoDB_first_steps/assets/71440118/56d94ba5-2b08-46a6-89d3-733295124dfc)

![image](https://github.com/Osetinskiy-pokemon/SberTech_DBS_MongoDB_first_steps/assets/71440118/c92178b3-7e2c-433c-b55d-bb8dac6a88ba)

![image](https://github.com/Osetinskiy-pokemon/SberTech_DBS_MongoDB_first_steps/assets/71440118/97087e06-b0a8-483e-abef-22372a30f90d)

![image](https://github.com/Osetinskiy-pokemon/SberTech_DBS_MongoDB_first_steps/assets/71440118/e7aca8f2-9705-46e7-afdc-ddbfbb99f876)

![image](https://github.com/Osetinskiy-pokemon/SberTech_DBS_MongoDB_first_steps/assets/71440118/2a9ea3f1-59ac-4a10-9b5e-6ece94b94973)

Обновляем данные:

![image](https://github.com/Osetinskiy-pokemon/SberTech_DBS_MongoDB_first_steps/assets/71440118/54cd172a-abc6-4e8e-9bbb-5aef470efaa1)

Смотрим, что получилось:

![image](https://github.com/Osetinskiy-pokemon/SberTech_DBS_MongoDB_first_steps/assets/71440118/b9fe2e26-6ea2-44c7-a759-34ba2b25e0cc)

Удалим эту запись:

![image](https://github.com/Osetinskiy-pokemon/SberTech_DBS_MongoDB_first_steps/assets/71440118/92c0eb75-e239-4f01-8917-48e93ad42cb5)

Так, ну замерить нормально время выполнения запросов у меня на этой базе не получилось, потому что она слишком маленькая (800+ строк данных) и время было 0-9мс. Поэтому что мы делаем? Закачиваем новую базу!

![image](https://github.com/Osetinskiy-pokemon/SberTech_DBS_MongoDB_first_steps/assets/71440118/f8cb3ddc-9267-4531-b2ec-acf3cfb9433e)

Проверим, сколько выполняется операция поиска. Ого:

![image](https://github.com/Osetinskiy-pokemon/SberTech_DBS_MongoDB_first_steps/assets/71440118/a70f5c7b-bea6-432c-a6d3-15af617979cc)

Попробуем навесить индекс:

![image](https://github.com/Osetinskiy-pokemon/SberTech_DBS_MongoDB_first_steps/assets/71440118/7a7671c3-0ea4-4bea-9217-1f0cbacee1c0)

Вновь проверяем операцию поиска и ого:

![image](https://github.com/Osetinskiy-pokemon/SberTech_DBS_MongoDB_first_steps/assets/71440118/43cc6fac-e26d-44f9-97c6-a6fca7d7d250)

Неплохо!
Теперь проверим изменение данных:

![image](https://github.com/Osetinskiy-pokemon/SberTech_DBS_MongoDB_first_steps/assets/71440118/88a92fd9-0802-4550-8bcc-db8816d871ba)

С индексом время изменения данных вообще увеличилось…

![image](https://github.com/Osetinskiy-pokemon/SberTech_DBS_MongoDB_first_steps/assets/71440118/7191934a-2145-436a-90a9-2d1f35077c5b)

С Удалением тоже лучше было до индекса:

Без индекса:

![image](https://github.com/Osetinskiy-pokemon/SberTech_DBS_MongoDB_first_steps/assets/71440118/66e1feee-672b-47ae-887a-35b46ec7564e)

С индексом:

![image](https://github.com/Osetinskiy-pokemon/SberTech_DBS_MongoDB_first_steps/assets/71440118/7cb4f055-0bfd-47d6-9c06-34aba7e0fa8d)

Операция вставки:

Без индекса:

![image](https://github.com/Osetinskiy-pokemon/SberTech_DBS_MongoDB_first_steps/assets/71440118/32357780-3818-4e80-9437-742ab254f28f)

Занимает 8 мс:

![image](https://github.com/Osetinskiy-pokemon/SberTech_DBS_MongoDB_first_steps/assets/71440118/1ee39c8c-158c-45f9-9d1b-7d202e219cf6)

С индексом:

![image](https://github.com/Osetinskiy-pokemon/SberTech_DBS_MongoDB_first_steps/assets/71440118/06d3b302-86b7-472d-bc87-c48e53a4df10)

Намного больше:

![image](https://github.com/Osetinskiy-pokemon/SberTech_DBS_MongoDB_first_steps/assets/71440118/603f22dc-1a8b-438a-83e5-bb7603c4c719)

### Небольшой вывод:
Таким образом индексирование нужно использовать очень внимательно и с умом. Да, оно повышает производительность при чтении данных, однако при других операциях индекс обновляется, из-за чего время выполнения операции может быть дольше. Чем больше индексов и записей, тем больше может быть затрачено времени.
