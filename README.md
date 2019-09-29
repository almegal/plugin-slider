# slider-plugin
Тестовое задание для FSD
### Содержание:
- Быстрый старт- 
- Основная диаграмма и описание архитектуры
- Подробное описание:
  - Модель
  - Вид
  - Презентер
- Описание панели конфигурации


### Быстрый старт
Для клонирования репозитория на машину используйте команду:
```
git clone https://github.com/almegal/plugin-slider
```

Для установки зависимостей используйте:
```
npm install
```

Чтобы установить devDependencies :
```
npm install --only=dev
```

Для запуска используется: 
```
npm run dev
```

Для запуска тестов:
```
npm test
```

### Основная диаграмма и описание архитектуры

![diagramma](https://github.com/almegal/plugin-slider/blob/master/uml/slider-plugin.png)

Пользователь взаимодействует с видом, а сам вид оповещает презентер/контроллер о том, что произошло какое то событие. Контроллер определяет какое событие произошло и передает управление соответствующему методу модели. Далее, модель выполняет вызванный метод и изменяет состояние и передает управление обратно контроллеру. Котнроллер, получив управление, передает новые данные в вид.

Model и View не знают друг о друге и об Presenter. Presenter в свою очередь знает о Model и View и управляет ими посредством api.

Для инициализации слайдера используйте следующий код:
```
$('#some_id').slider({
	min: 0,
	max: 100,
	step: 10,
	currentValue: 40,
});
```

Конфигурация слайдера реализована через интерфейс IOptions:
```typescript
interface IOptions {
	currentValue?: number;
	min?: number;
	max?: number;
	step?: number;
	orient?: string;
	showStep?: boolean;
	interval?: false | <Array>IInterval;
	showBubbles?: boolean;
}
interface IInterval {
	from: number;
	to: number;
}
```


Вы можете не указывать никаких конфигураций:
```
$('#some_id').slider({})
```

В таком случае слайдер установит значения по-умолчанию:
```typesccript
const defaultProps: IOptions {
	currentValue: 40,
	min: 0,
	max: 100,
	step: 10,
	orient: 'horizontal',
	showStep: true,
	interval: false,
	showBubbles: false
}
```


### Подробное описание

#### Модель

![diagramma model](https://github.com/almegal/plugin-slider/blob/master/uml/model.png)

#### Вид
#### Презентер

### Описание панели конфигурации