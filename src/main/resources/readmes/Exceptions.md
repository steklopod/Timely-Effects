## Исключения (Exceptions)

Когда асинхронные вычисления вызывают необработанные исключения, фьючерсы, связанные с этими вычислениями, терпят неудачу.
 Неудавшиеся фьючерсы сохраняют экземпляр `Throwable` вместо значения результата. Фьючерсы предоставляют неудачный метод 
 прогноза, который позволяет этому `Throwable` рассматриваться как ценность успеха другого `Future`. Следующие особые 
 исключения обрабатываются по-разному:

1. `scala.runtime.NonLocalReturnControl[_]` - это исключение содержит значение, связанное с возвратом. Как правило, 
возвратные конструкции в телах методов переводятся в броски с этим исключением. Вместо сохранения этого исключения 
связанное значение сохраняется в будущем или в обещании.

2. `ExecutionException` - сохраняется, когда вычисление завершается сбоем из-за необработанного `InterruptedException`,
 `Error` или `scala.util.control.ControlThrowable`. В этом случае `ExecutionException` имеет необработанное исключение в 
 качестве причины. Обоснованием этого является предотвращение распространения критических и связанных с контролем потоков 
 исключений, которые обычно не обрабатываются клиентским кодом и в то же время сообщают клиенту, в котором в будущем не 
 удалось выполнить вычисление.

Фатальные исключения (как определено `NonFatal`) возвращаются в поток, выполняющий неудавшееся асинхронное вычисление. 
Это информирует код, управляющий исполняемыми потоками проблемы, и позволяет, если необходимо, быстро работать с ошибкой. 
См. `NonFatal` для более точного описания семантики.

_Если этот проект окажется полезным тебе - нажми на кнопочку **`★`** в правом верхнем углу._

[<= содержание](https://github.com/steklopod/Parallel-Programming/blob/master/readme.md)