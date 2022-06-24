# Краткая инструкция по блоку 1.6

Содержание:
1. [Установка WebPack](#id1)  
  1.1 [Клонируем WebPack](#id2)  
  1.2 [Проверка версии Node.js и установка зависимостей](#id3)  
  1.3 [Запускаем проект](#id4)  
2. [Установка и подключение normalize.css](#id5)  
  2.1 [Устанавливаем normalize.css при помощи менеджера пакетов](#id6)  
  2.2 [Подключаем normalize.css к проекту](#id7)  
3. [Подключение и настройка Swiper](#id8)  
  3.1 [Установка Swiper](#id9)  
  3.2 [Подключаем базовые стили Swiper](#id10)   
  3.3 [Стилизуем bullets](#id11)  
  3.4 [Инициализируем Swiper в JS файле](#id12)  
4. [Размещаем проект на GitHub](#id13)  
  4.1 [Создаем репозиторий для исходников](#id14)  
  4.2 [Пушим исходники на GitHub](#id15)  
  4.3 [Пушим product-сборку на GitHub](#id16)  
  4.4 [Подключаем GitHub Pages для product-сборки](#id17)

## <a name="id1">Установка WebPack</a> 
Перед тем, как начать работать с WebPack, требуется установить следующие компоненты:
1. [Node 14.18.3](https://nodejs.org/download/release/v14.18.3/)
2. [NVM/MacOC](https://tecadmin.net/install-nvm-macos-with-homebrew/)
3. [NVM/Windows](https://github.com/coreybutler/nvm-windows/releases) - установка от имени администратора
4. [GIT](https://www.atlassian.com/git/tutorials/install-git) - во время установки обязательно установите галочку напротив "New! Add a Git Bash Profile"
5. Также можно (но не обязательно) установить [Yarn](https://yarnpkg.com/)


#### <a name="id2">Клонируем WebPack</a> 
После установки необходимых компонентов, можно начинать клонирование WebPack с GitHub, для чего открываем Git Bash на своем ПК и вводим следующие команды:
1. Клонируем репозиторий:  
```git clone https://github.com/alex-karo/webpack-static-template block7```  
2. Далее переходим в папку проекта:  
```cd block7```  
3. При помощи следующей команды удаляем папку ".git":  
```rm -fr .git```
#### <a name="id3">Проверка версии Node.js и установка зависимостей</a> 
1. Проверяем версию Node.js командой:  
```node -v```  
Должно вывестись сообщение "v14.18.3".  Если у вас установлено несколько версий Node.js и выводится альтернативное сообщение, используем команду:  
```nvm use 14.18.3```
2. Если все предыдущие шаги выполнены верно, остается лишь установить зависимости для нашего проекта командой:  
```npm install``` -  если пользуемся NPM  
либо  
```yarn``` - если пользуемся yarn  
#### <a name="id4">Запускаем проект</a> 
Для удобной работы над проектом рекомендую использовать веб сервер с Live Reload:  
```npm run start``` - NPM  
```yarn start``` - YARN  
Вводим одну из этих команд для проверки, что все работает корректно.  
Если вы увидели стартовую страницу WebPack, можно двигаться дальше.  
## <a name="id5">Установка и подключение normalize.css</a> 
Перед тем, как продолжить, запускаем редактор кода, в котором вы работаете.  

#### <a name="id6">Устанавливаем normalize.css при помощи менеджера пакетов</a>
Поскольку мы работаем с менеджерами пакетов NPM или YARN, устанавливать normalize.css будем именно через них, для чего требуется открыть терминал и ввести одну из следующих команд:  
```npm i normalize.css```  
```yarn add normalize-css```  

#### <a name="id7">Подключаем normalize.css к проекту</a>
Чтобы подключить normalize.css, требуется импортировать его в наш проект, для чего переходим в папку scss и добавляем следующую строчку в самое начало файла style.scss:  
```@import '../../node_modules/normalize.css/normalize.css';```  
Отлично! Мы подключили normalize.css, переходим к более сложному, а именно - Swiper
## <a name="id8">Подключение и настройка Swiper</a>
В данной главе мы подключим Swiper к проекту в соответствии с ТЗ. 
#### <a name="id9">Установка Swiper</a>
Swiper будем подключать также через NPM, либо YARN одной из следующих команд:  
```npm install swiper```  
```yarn add swiper```  
#### <a name="id10">Подключаем базовые стили Swiper</a>
Чтобы подключить стили, переходим в папку scss и добавляем строчку в начало файла style.scss:  
```@import '../../node_modules/swiper/swiper.scss';```  
Таким образом мы подключим только базовые стили Swiper, поэтому нам нужно отдельно стилизовать пагинацию.

#### <a name="id11">Стилизуем bullets</a>
bullets - это всем известные "точки" под изображениями, которым мы придадим красивое оформление, для чего добавим стили:  
```scss
.swiper {
  &-pagination {
    display: flex; //изменяем тип отображения на flex-контейнер
    justify-content: center; //центрируем bullets по горизонтали

    &-bullet {
      height: 12px; // устанавливаем высоту bullets на 12 px
      width: 12px;  // устанавливаем ширину bullets на 12 px
      background: #DDD;  // устанавливаем цвет неактивных bullets
      border-radius: 50%;  // делаем их круглыми
      margin: 0 6px;  // устанавливаем отступ по горизонтали в 6px

      &-active {
        background: #B5B6BC; //устанавливем цвет для активных bullets
      }
    }
  }
}
```  
Хорошо, необходимые стили подключены, но Swiper в нашем проекте существует лишь в перспективе, двигаемся дальше.
#### <a name="id12">Инициализируем Swiper в JS файле</a>
После настройки стилей, было бы неплохо иницизировать наш Swiper в проекте, для чего переходим в папку JS и открываем файл index.js, в котором пишем:  
```JS
import Swiper, { Pagination } from 'swiper' // импортируем Swiper в наш проект, а также один из его модулей "Pagination"
Swiper.use([Pagination]) // подключаем Pagination к Swiper

window.onload =  () => {  // ожидаем загрузку окна браузера
  if (window.matchMedia('(max-width: 767px)').matches) { // // свайпер у нас будет работать, если разрешение эерана не превышает 767px
    const swiper = new Swiper('.swiper', {  // инициализируем новый Swiper
      direction: 'horizontal', // устанавливаем напрвление Swiper
      loop: true,  // делаем Swiper зацикленным (Swiper самостоятельно добавит слайды в начало и конец .swiper-wrapper для создания иллюзии "бесконечности" слайдов)
      spaceBetween: 20 // отступ между слайдами в px
      slidesPerView: 'auto', // позволит устанавливать произвольную ширину слайдов, в противном случае - растянет на ширину контейнера .swiper-wrapper
      pagination: { // подключаем пагинацию
        el: '.swiper-pagination' // контейнер для пагинации
        clickable: true // добавляем параметр, если хотим сделать bullets кликабельными
      },
      init: true
    })
   }
  }
 }
 ```  
Теперь можно использовать swiper в проекте, дополнительная информация - [Swiper: Get Started](https://swiperjs.com/get-started)
## <a name="id13">Размещаем проект на GitHub</a>
В данной главе мы запушим проект на GitHub и подключим Github Pages.  

#### <a name="id14">Создаем репозиторий для исходников</a>
Прежде чем начать, необходимо создать репозиторий, для чего заходим в наш профиль GitHub и переходим в "Repositories", после чего нажимаем кнопку "New". Добавлять Readme файл и лицензии не нужно, при необходимости - можно сделать позже
#### <a name="id15">Пушим исходники на GitHub</a>
Первым делом, убедитесь, что в вашем проекте отсутствует папка ".git" (обычно она является скрытой). Если ее нет, можно переходить к следующим шагам:  
1. Открываем терминал
2. Первым делом необходимо перейти в папку проекта  
```cd путь-к-директории```  
Если вы открыли свой проект через редактор кода, достаточно поставить "." вместо "путь-к-директории"  
3. Далее определяем текущую директорию, как директорию Git-репозитория:  
```git init```  
4. Добавляем файлы в новый локальный Git-репозиторий:  
```git add .```  
5. Коммитим файлы из нашего локального Git-репозитория:  
```git commit -m "My commit"```  
6. Указываем на новый локальныйы Git-репозиторий:  
```git remote -v```  
7. Проверяем новый удаленный репозиторий:  
```git remote add origin ссылка_на_репозиторий```  
ссылка_на_репозиторий - это ссылка на репозиторий с GitHub, с которым мы работаем.  
8. Отправляем изменения локального репозитория на GitHub:  
```git push origin master```
#### <a name="id16">Пушим product-сборку на GitHub</a>
Для того, чтобы WebPack скомпилировал наш проект, необходимо запустить команду:  
```npm run build```  
либо  
``` yarn build```  
Далее создаем еще один репозиторий на GitHub с названием "название_репозитория.github.io".  
После чего необходимо снова открыть терминал и перейти в папку "dist", которую скомпилировал WebPack:  
```cd ./dist```  
Теперь повторяем шаги 3-9 выше.
#### <a name="id17">Подключаем Github Pages для product-сборки</a>
Вы успешно загрузили свой проект в репозиторий GitHub, теперь необходимо получить ссылку на рабочий сайт. Самый простой способ сделать это:
1. Перейти в репозиторий ("название_репозитория.github.io")  
2. Перейти к настройкам (Settings)  
3. В настройках ищем вкладку "Pages"  
4. На данной вкладке ищем заголовок "Source" и заполняем два окошка:  
  4.1.  Branch - Branch:master  
  4.2.  Папка - root  
5. Если все сделано правильно, то после того, как вы нажмете на кнопку "save", появится ссылка на рабочий html-документ в верхней части вкладки Pages  
Если 4 шаг выполнить не удается, попробуйте вернуться к нему через некоторое время.
