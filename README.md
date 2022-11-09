**public class JvmComprehension {<br />
&nbsp;&nbsp;&nbsp;&nbsp;public static void main(String[] args) {<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;		int i = 1; // 1<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;		Object o = new Object(); // 2<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;		Integer ii = 2; // 3<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;		printAll(o, i, ii); // 4<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;		System.out.println("finished"); // 7<br />
&nbsp;&nbsp;&nbsp;&nbsp;	}<br />
&nbsp;&nbsp;&nbsp;&nbsp;	private static void printAll(Object o, int i, Integer ii) {<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;		Integer uselessVar = 700; // 5<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;		System.out.println(o.toString() + i + ii); // 6<br />
&nbsp;&nbsp;&nbsp;&nbsp;	}**<br />
}<br />

1) public static void main(String[] args) { - Загрузчик классов ClassLoader загружает class-файлы JvmComprehension и System.out.println()
2) Bootstrap class loader (базовый, первичный загрузчик) — загружает классы из bootstrap classpath.
3) Связывание, линковка (linking) — выполнение верификации(Verify), подготовки(Prepare) и, необязательного, разрешения(Resolve)
4) Инициализация (initialization)
5) Выполняются инициализатор static printAll()
6) Как только мы вызываем метод main, в стеке JvmComprehension для нее создается стековый кадр(stack frame), пустая куча(heap)c Metaspace

1. Ссылка на int i = 1 добавляется в стек JvmComprehension
2. Object o добавляется в heap, ссылка в стэк
3. В стэк добавляется сслыка на Integer ii = 2
4. В стэк добавляется ссылка на printAll(o, i, ii) - cвязываются с кучей
5. В стэк добавляется ссылка на uselessVar = 700 связанный с кучей Integer
6. В стэк создается фрейм с ссылкой o.toString(), i, ii.
7. В стэк создается фрейм с ссылкой на finished<br /><br />
JVM находятся в оперативной памяти. Во время выполнения с помощью загрузчика классов файлы классов заносятся в ОЗУ. Код BYTE проверяется на любые нарушения безопасности.
Затем механизм выполнения преобразует Байт-код в машинный код Native. В этом участвует и JIT. Он интерпретирует часть Байт-кода, который имеет аналогичные функции одновременно.
Параллельно с этим работает Garbage Collection который собирает больше не используемые объекты из heap(кучи)
