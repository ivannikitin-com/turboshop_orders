Turboshop Orders
================

**Версия 1.0.1**

Плагин для регистрации в WooCommerce заказов, сделанных в магазине Яндекс.Турбо.

При оформлении заказа в магазине Яндекс.Турбо может быть передана информация о заказе
на внешний сервер. Яндекс.Турбо передает магазину информацию об оформлении заказа 
и ожидает подтверждение принятия заказа или отказ. Информации о покупателе передается 
после подтверждения заказа в уведомлении о новом статусе заказа.

Подробнее можно почитать в разделе [Яндекс Настройки API магазина](https://yandex.ru/dev/turbo-shop/doc/settings/shop-api.html).

Этот плагин реализует конечные точки для принятия такой информации и регистрации
заказа в WooCommerce. Конечные точки следующие
1. https://example.com/wp-json/turboshop_orders/v1/order/accept -- Принятие заказа
2. https://example.com/wp-json/turboshop_orders/v1/order/status -- Обновление заказа


Установка и настройка плагина
-----------------------------

1. Скачайте последнюю версию плагина со страницы [релизов плагина](https://github.com/ivannikitin-com/turboshop-orders/releases).
2. Штатно установите плагин в WordPress и активируйте его.
3. Подключите Ваш магазин к Яндекс.Турбо согласно [инструкции](https://yandex.ru/dev/turbo-shop/doc/quick-start/markets.html).
4. Откройте в панели [Яндекс.Вебмастер](https://webmaster.yandex.ru/) свой сайт и перейдите на страницу
   "Турбо‑страницы для интернет-магазинов → Настройки → Настройки API".
5. Включите настройки API и скопируйте (сохраните) токен.
6. Откройте страницу настроек плагина "WooCommerce → Настройки → Яндекс.Турбо" и введите там полученный токен, сохраните изменения.
7. На странице Настройки API Яндекс.Вебмастера в поле "URL для запросов API" введите значение, которое можно скопировать на странице
настроек плагина. В общем виде это значение следующее:

   ```
   https://ВАШ_ДОМЕН.РУ/wp-json/turboshop_orders/v1
   ```
   `ВАШ_ДОМЕН.РУ` следует заменить на домен вашего магазина. 

8. Обязательно сохраните изменения.


Обновление плагина
------------------

Если вы устанавливали плагин через загрузку плагина в WordPress, начала удалите ранее загруженный плагин, и установите его снова.
Все настройки и ранее обработанные заказы будут сохранены.


Отображение заказов Яндекс.Турбо в списке заказов
-------------------------------------------------

Все заказы, сделанные в Яндекс.Турбо теперь отображаются в общем списке заказов WooCommerce. 
Чтобы отличить заказы Яндекс.Турбо выводится дополнительная колонка "Заказ в Яндекс.Турбо"
в таблице заказов. Вы можете включить или выключить эту колонку с помощью параметра "Настройки экрана"
справа сверху страницы "WooCommerce → Заказы".

Хуки плагина
------------

В плагине реализованы следующие фильтры (хуки):
* `turboshop_orders_update_status` -- Значение статуса заказа
* `turboshop_orders_add_shipping` -- Объект `WC_Shipping_Rate`, который будет добавлен в создаваемый заказ
* `turboshop_orders_update_shipping_cost` -- Значение стоимости доставки, которое будет обновлено в заказе
* `turboshop_orders_set_payment_method` -- Метод оплаты, который будет установлен в заказе
* `turboshop_orders_set_customer_note` -- Значение комментария пользователя, которое добавляется в заказ
* `turboshop_orders_set_billing_phone` -- Значение телефона пользователя
* `turboshop_orders_set_name` -- Значение полного имени пользователя. Если есть записывается как `billing_last_name`
* `turboshop_orders_set_last_name` -- Значение фамилии пользователя. Если есть записывается как `billing_last_name`
* `turboshop_orders_set_first_name` -- Значение имени пользователя. Если есть записывается как `billing_first_name`
* `turboshop_orders_add_order_note` -- Значение заметки, добавляемой в заказ
* `turboshop_orders_result_order_id` -- Значение внутреннего ID заказа, возвращаемое Яндексу 


Отладка
-------

Для отладки работы плагина необходимо установить константу `WP_DEBUG` в состояние `true` и передавать 
заказы с полем `fake` со значение `true`. Иначе такие заказы в режиме `WP_DEBUG == false` сразу же удаляются.


Переводы на другие языки
------------------------

Плагин изначально поставляется с русским языком локализации, но может быть переведен (локализован) на любой язык. 
Для этого необходимо использовать шаблон переводов [turboshop_orders.pot](lang/turboshop_orders.pot). 
Поместите файлы перевода в папку `lang` и плагин подключит их автоматически.


Обратная связь и сообщения об ошибках
-------------------------------------

Мы с благодарностью принимаем любые сообщения об ошибках, любые комментарии и предложения по развитию плагина на странице
[Issues](https://github.com/ivannikitin-com/turboshop-orders/issues) репозитория плагина.