### Задача:
Создаем Cloud-native приложение для экспериментов
1. Создаем само приложение
2. Создаем юнит тесты для приложения
3. Докеризируем: Создаем докерфайл для сборки контейнера
4. Описываем CI-сценарии для Github Actions производящие lint, unit-test, build-test
5. Куберизируем: Создаем манифесты для запуска приложения и сервисов в кластере
6. Описываем CD-сценарии для Github Actions производящие docker build и push в Docker Hub
7. Устанавливаем ArgoCD и подключаем к GitHub
8. Проверяем весь CI/CD workflow в сборе

### Ход работы:

1.Создаем репозиторий для приложения

2. Клонируем репо с гитхаба

![cicd_1](https://github.com/user-attachments/assets/58665bb9-caee-470b-9033-2c70934a398a)

3. Приложение server/application.py

![cicd_2](https://github.com/user-attachments/assets/0143c03e-ba06-4d99-bd88-13aff92de112)

4. Юнит-тесты server/test_application.py

![cicd_3](https://github.com/user-attachments/assets/9de854fc-50fe-49d6-bafa-76497209bf5d)

5. Файл с зависимостями для самих тестов requirements.txt

![cicd_4](https://github.com/user-attachments/assets/485a10ef-2373-487e-ae5e-026cd3258d67)

6. Файл для сборки образа dockerfile

![cicd_5](https://github.com/user-attachments/assets/729a8593-d293-460f-88fc-ec1b22c9fa21)

7. Проверяем, что всё пушится в гитхаб. Добавляем все созданные ранее файлы (dockerfile, requirements.txt ...)

![cicd_6](https://github.com/user-attachments/assets/b169464e-aca8-4fb3-a392-8756da5001d1)

8. Переводим разработку в отдельную ветку dev

![cicd_7](https://github.com/user-attachments/assets/c73409c1-ade2-4347-a9ba-54c613df94f6)

9. Защищаем ветку master от прямых изменений, теперь только merge-requests

![cicd_8](https://github.com/user-attachments/assets/baf8cac5-ab7d-427f-b21b-35e741f4e9dd)
![cicd_8_1](https://github.com/user-attachments/assets/49fa1b13-476e-4d1b-8121-8535887bc4a8)

10. Теперь новая работа вносится только в dev. Добавляем индексный файл, пушим, открываем pull/merge-request

![cicd_9](https://github.com/user-attachments/assets/0cc873ab-7b56-45bd-a3e5-843c2cf7f285)
![cicd_9_1](https://github.com/user-attachments/assets/ad181638-e902-464c-abac-a6427d9c72ff)
![cicd_10](https://github.com/user-attachments/assets/377943ed-98ff-48ac-bea5-842b6306b58c)
![cicd_10_1](https://github.com/user-attachments/assets/68e3c6da-0b1d-4e49-9fa0-d324ef03a594)

11. Добавляем CI-пайплайны (сценарии) – Github Actions

![cicd_11](https://github.com/user-attachments/assets/97424613-c587-431a-87e3-1e2fc4e94c56)
![cicd_12](https://github.com/user-attachments/assets/d9425c0a-fc97-4d37-a900-8ea55cfe6fc3)

12. Посмотреть как работает runner на стороне GitHub

![cicd_13](https://github.com/user-attachments/assets/447c6bc1-51d6-4c65-9465-d4eda0957e9b)

13. Добавляем сценарии CI в гит

![cicd_14](https://github.com/user-attachments/assets/c4429938-1c51-4a59-abbd-9762f9246a5d)
![cicd_15](https://github.com/user-attachments/assets/8e6c70cd-4e6a-4a0e-bbe9-ca4ae227cc7a)

14. Боевой сценарий – линтер > юнит-тесты > интеграционный тест

![cicd_16](https://github.com/user-attachments/assets/0d22d5d7-f4bc-45a8-a68d-927e432dc5a3)

15. Добавляем новый сценарий в гит

![cicd_17](https://github.com/user-attachments/assets/a6a05a40-1741-4c4a-92d3-da72f72927ea)

16. Проверяем как отрабатывает новый сценарий

![image](https://github.com/user-attachments/assets/a9b6a405-936e-4335-9f16-ea45ccb8aed8)

17. Отлаживаем приложение, чтобы все тесты прошли успешно

![cicd_18](https://github.com/user-attachments/assets/1fcef8f9-cac3-44db-9734-6ad0e40b12cc)
![cicd_20](https://github.com/user-attachments/assets/92a92151-d5a8-4814-a299-fab181fe8a75)

18. Куберизируем наше приложение. Создаём для приложения k8s-манифесты

![cicd_21](https://github.com/user-attachments/assets/483cae00-887c-4aea-ac66-6c8248fde122)

19. Добавляем публикацию докер-образа приложения в хранилище

![cicd_22](https://github.com/user-attachments/assets/63d73652-a318-457d-8074-0d3dd9c2fe06)

20. Куберизируем приложение: создаем K8s манифест

![cicd_23](https://github.com/user-attachments/assets/b592435a-c4cd-4894-b22a-b458ec63a676)

21. Проверяем/запускаем minikube

![cicd_24](https://github.com/user-attachments/assets/b687093d-9e54-4905-884c-4219877558ec)

22. Удаляем контейнеры с прошлых занятий

![cicd_25_1](https://github.com/user-attachments/assets/07d5da63-1e88-4546-adcb-10460f455aab)
![cicd_25_2](https://github.com/user-attachments/assets/9f9f18e5-dc52-4478-a74a-3d7402a27953)
![cicd_25_3](https://github.com/user-attachments/assets/8b31b717-5c70-4a5b-8228-fac665c2ce32)

23. Куберизируем наше приложение. Применяем k8s-манифесты

![cicd_26_1](https://github.com/user-attachments/assets/15857392-0aba-4b9f-8607-d5f3de5eabc3)
![cicd_26_2](https://github.com/user-attachments/assets/a58a63db-c7b9-4967-b592-e6d6ab6ec725)

24. Сохраняем манифесты в github

![cicd_27](https://github.com/user-attachments/assets/0130cdd2-c57d-44d2-9375-781cc6a7aa19)

25. Добавляем публикацию докер-образа приложения в хранилище

![cicd_28](https://github.com/user-attachments/assets/f1745eeb-296d-4d4f-a494-821563ae80e6)

26. Добавляем свои учетные данные как Action Secrets на github. Два секрета – DOCKER_USERNAME и DOCKER_TOKEN

27. Создаем пайплайн для сборки и публикации образа в Docker Hub .github/workflows/release.yml

![cicd_29_замена](https://github.com/user-attachments/assets/65e1fbf0-8fac-442b-9a57-8202747b6592)

28. Делаем коммит новых файлов в репо, создаем pull-request и выполняем merge в master.
Будет выполнен новый пайплайн release.yml
Пример отработки пайплайна

![cicd_30](https://github.com/user-attachments/assets/19db0342-f8f0-4e5c-87df-05b819a755b1)

29. Видим, что пайплайн успешно положил новый образ в докерхаб

![cicd_30_1](https://github.com/user-attachments/assets/a7d3d8f4-5dae-4f07-9187-39a3536c0ab3)

30. Устанавливаем ArgoCD

![cicd_31](https://github.com/user-attachments/assets/40b455f3-838e-4976-a635-6d67b0d814e1)
![cicd_32](https://github.com/user-attachments/assets/8dc7d6a5-4ddf-4505-a482-2b96ff461e47)

31. Подключаем к ArgoCD наш GitHub репо с использованием приватного ключа

![cicd_33](https://github.com/user-attachments/assets/9d8930bc-2031-4cf1-8c4e-3041bbcf4634)
![cicd_34](https://github.com/user-attachments/assets/1d5e7243-d482-4a0b-8995-f3915b53d763)

32. Подключаем манифесты приложения для контроля состояния

![cicd_35](https://github.com/user-attachments/assets/027f1d6d-399f-4d91-b451-44a8c1846dcc)
![cicd_35_1](https://github.com/user-attachments/assets/83c5566f-6155-4e39-be0d-79a60f10c81a)

33. Приложение установлено на контроль ArgoCD

![cicd_36](https://github.com/user-attachments/assets/cbbd0e76-10da-4c02-a778-8c6c3a3181b9)
![cicd_36_1](https://github.com/user-attachments/assets/7e487112-b969-46cc-b66a-f910b7d2d7ea)

### Проверка
1. Изменяем приложение

![cicd_37](https://github.com/user-attachments/assets/daf4b274-9c56-4ac3-8844-2e2952c3e245)
![cicd_38](https://github.com/user-attachments/assets/1c229d18-3402-46a2-86f1-099b432cd066)

2. Сохраняем изменение в ветке dev

![cicd_39](https://github.com/user-attachments/assets/3e0ff3b8-2db6-40df-9819-02174d342b03)

3. На ветке master сработает пайплайн на релиз, новый образ будет отправлен на DockerHub, манифест будет пропатчен

![cicd_40](https://github.com/user-attachments/assets/d52ed452-5c48-4e7b-84fc-9b55cb41dd60)

4. ArgoCD подхватит изменения манифеста и синхронизирует состояние в k8s

![cicd_41](https://github.com/user-attachments/assets/8cce4782-158e-4ffd-a6ab-f2742cbca8c9)
![cicd_42](https://github.com/user-attachments/assets/54b841e4-40de-4ef4-b158-9b5662dc5035)
