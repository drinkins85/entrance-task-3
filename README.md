# Задание 3

ServiceWorker может управлять файлами в своей и вложенных директориях.
Для того чтобы в его scope попали файлы директории vendor, его нужно переместить на уровень выше



Ответы на вопросы:

# Вопрос №1: зачем нужен этот вызов?
        .then(() => self.skipWaiting())
  -	Вызовет событие 'activate' для нового SW при уже работающим старом
    Нужен для обновления SW без перезагрузки страницы

# Вопрос №2: зачем нужен этот вызов?
        self.clients.claim();
  -	Активирует SW для всех клиентов в его scope
	Нужен для обновления SW без перезагрузки страницы

# Вопрос №3: для всех ли случаев подойдёт такое построение ключа?
	const cacheKey = url.origin + url.pathname;
  - Не подойдет при использовании CDN

# Вопрос №4: зачем нужна эта цепочка вызовов?
            return Promise.all(
                names.filter(name => name !== CACHE_VERSION)
                    .map(name => {
                        console.log('[ServiceWorker] Deleting obsolete cache:', name);
                        return caches.delete(name);
                    })
            );
  -	Выбираем массив старых кэшей (name !== CACHE_VERSION), перебираем и удаляем их:
	(return caches.delete(name) - возвращает resolve, при успешном удалении)

# Вопрос №5: для чего нужно клонирование?
    cache.put(cacheKey, response.clone());
  - Объекты Response могут использоваться лишь один раз