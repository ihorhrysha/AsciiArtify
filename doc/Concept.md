## Порівняльна характеристика інструментів розгортання Kubernetes для локальної розробки


### Вступ

Для локальної розробки Kubernetes кластерів існує кілька популярних інструментів, серед яких Minikube, kind (Kubernetes IN Docker) та k3d. Вони забезпечують можливість швидко та ефективно створювати локальні Kubernetes кластери для тестування та розробки. Ці інструменти дозволяють розробникам та DevOps інженерам перевіряти свої додатки в умовах, наближених до реальних, без необхідності використовувати великі ресурси або витрачати час на налаштування повноцінних кластерів у хмарі.


### Характеристики

| Характеристика / Параметр | Minikube | kind | k3d |
|---------------------------|----------|------|-----|
| **Підтримувані ОС та архітектури** | Windows, macOS, Linux; x86_64, ARM | Windows, macOS, Linux; x86_64 | Windows, macOS, Linux; x86_64, ARM |
| **Автоматизація** | Підтримка CI/CD систем, автоматизація через CLI | Добра інтеграція з CI/CD системами (GitHub Actions, Jenkins) | Підтримка CI/CD систем (GitLab CI, Jenkins) |
| **Додаткові функції** | Вбудовані інструменти для моніторингу (cAdvisor), підтримка різних драйверів контейнерів | Легке створення багатокластерних середовищ, підтримка нестандартних конфігурацій кластерів | Легке налаштування багатокластерних середовищ, висока продуктивність завдяки використанню k3s |


### Переваги та недоліки

| Переваги / Недоліки | Minikube | kind | k3d |
|---------------------|----------|------|-----|
| **Переваги** | Простота використання та налаштування; підтримка багатьох драйверів віртуалізації; вбудовані інструменти для моніторингу | Легкість та швидкість розгортання; можливість тестування складних конфігурацій кластерів; висока стабільність роботи | Легкість та швидкість розгортання; підтримка lightweight-версії Kubernetes; можливість розгортання на пристроях з низькими ресурсами |
| **Недоліки** | Великі вимоги до ресурсів; проблеми зі стабільністю на різних ОС; труднощі з налаштуванням на старих версіях ОС | Залежність від Docker (ліцензійні ризики); відсутність вбудованих інструментів для моніторингу; обмежена підтримка нестандартних архітектур | Відсутність деяких функцій повноцінного Kubernetes; залежність від Docker (ліцензійні ризики); можливі проблеми з масштабованістю |


### Висновки

- **Minikube** є хорошим вибором для тих, хто потребує потужних вбудованих інструментів для моніторингу та підтримки різних драйверів віртуалізації. Проте, варто враховувати його великі вимоги до ресурсів.
- **kind** чудово підходить для швидкого та стабільного розгортання Kubernetes кластерів у середовищах розробки та тестування, але може мати проблеми з ліцензійними ризиками Docker.
- **k3d** є найкращим вибором для розгортання на пристроях з обмеженими ресурсами та для тих, хто хоче використовувати lightweight-версію Kubernetes. Проте, слід бути обережним щодо ліцензійних питань Docker.

### Демонстрація

Для демонстрації розгортання застосунку «Hello World» використаємо **k3d** як найбільш рекомендований інструмент для стартапів, що потребують легкості та швидкості розгортання.

1. (Опціонально, можна використати плагін VSCode)Встановлюємо k3d:
   ```sh
   curl -s https://raw.githubusercontent.com/rancher/k3d/main/install.sh | bash
   ```

2. (Опціонально, можна використати плагін VSCode) Створюємо новий кластер:
   ```sh
   k3d cluster create demo
   ```

3. Розгортаємо застосунок «Hello World» та створюемо сервіс для доступу до нього:
   ```sh
   kubectl create deployment hello-world --image=gcr.io/google-samples/node-hello:1.0
   kubectl expose deployment hello-world --type=LoadBalancer --port=8080
   ```

4. Отримуємо IP адреси для доступу до застосунку по порту 8080:
   ```sh
   kubectl get services hello-world
   ```

Приклад виконання команд та результати можна побачити на відео:
[![asciicast](https://asciinema.org/a/7uVthWOucu1EugPldKym7shUJ.svg)](https://asciinema.org/a/7uVthWOucu1EugPldKym7shUJ)