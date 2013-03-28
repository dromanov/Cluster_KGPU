Высокопроизводительный гибридный кластер КГПУ
=============================================

Репозиторий содержит набор материалов и примеров для использования на кластере КГПУ. Используемая форма хостинга
(`git`-репозиторий) позволяет следующее:
  * любой участник в любой момент может получить весь комплект в открытом (описанном) формате;
  * делать копии проекта для самостоятельного развития;
  * использовать `wiki` для добавления/исправления/получения информации;
  * использовать bug tracker для разрешения проблем.

Как выполнить программу на `MPI`
--------------------------------

1. Войдите на кластер.
2. Выполните команду `module avail` для определения списка доступных модулей.
3. Подключите желаемую версию `MPI`, выполнив, например, `module load openmpi/gcc`.
4. Проверьте наличие компилятора, выполнив `mpicc`.
5. Компилируйте проект.
6. Запускайте его на выполнение непосредственно (`mpirun -n 4 ./a.out`) или с помощью 
   планировщика (будет описано отдельно).

Как визуализировать серию 1D графиков
-------------------------------------

1. Создайте серию текстовых файлов с данными в две колонки.

      ```c
         for (int i = 0 ; i < N ; ++i) {
             char filename[100];
             sprintf(filename, "file_%04d.txt", i);
             FILE *fp = fopen(filename, "wt");
             for (double x = 0.0 ; x <= 10 ; x += 0.1) {
                 fprintf(fp, "%.2lelf %le\n", x, sin(x));
             }
             fclose(fp);
         }
      ```

    Скомпилируйте и выполните программу.

2. Создайте серию рисунков, выполнив из командной строки

      ```bash
        for f in file*.txt ; do echo $f ; cat $f | graph -T png ; done
      ```

3. Просматривайте свои кадры в любой программе, объединяйте их в видео-файл, - наслаждайтесь.

**WARNING:** `plotutils` на основном кластере в настоящий момент только устанавливается.
