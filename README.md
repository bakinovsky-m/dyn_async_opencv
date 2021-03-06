# Тестовое задание для Cognitive Pilot
Требуется разработать набор динамически загружаемых библиотек (.dll/.so/.dylib), реализующих асинхронные вызовы некоторых функций OpenCV, и тестовое приложение, реализующее динамическую загрузку библиотек и использование каждой функции

### Требования
* C++, стандарт 11 и выше
* OpenCV 3.4.5
* Каждая функция должна быть упакована в собственную библиотеку, при этом интерфейс у библиотек должен быть одинаковый
* Будет плюсом, если параметры cv-функций будут не захардкожены
* Решение должно быть представлено в виде единого cmake-проекта
#### Список функций
* GaussianBlur
* erode/dilate

Вариант реализации/использования на вызывающей стороне
```cpp
// загружаем картинку
Mat img = cv::imread("img.png");
// загружаем dll с обработчиком
CVWrapper blur("blur.so")

// запускаем асинхронную обработку
auto handle = blur.processAsync(img);
std::this_thread::sleep_for(std::chrono::milliseconds(10));

Mat res = blur.waitForResult(handle);

cv::imwrite("blurred.png");
```

Финальная реализация интерфейса динамической библиотеки, а так же клиентской обертки для работы с функциями из нее остается за кандидатом.
Так же следует обратить внимание на потокобезопасность при вызове processAsync \ waitForResult.

Готовое решение необходимо защитить вживую или по скайпу
